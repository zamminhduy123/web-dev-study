# 0: Queueing request
Khi chúng ta tạo 1 request lên server, nó sẽ đi qua rất nhiều layer để xử lý, chẳng hạn như đi vào bộ cache để kiểm tra xem liệu có fresh data ở local không giúp giảm thời gian nhận resource, DNS lookup, init connection (handshakes, retries), ... Nhưng trước khi đến được phần xử lý đó. Request có thể bị queue bởi browser bới các lý do sau:

- There are higher priority request.
- There are already six TCP connections open for this origin, which is limit. Applies to HTTP/1.0 and HTTP/1.1 only.
- The browser is briefly allocating space in the disk cache.


# 1: LocalStorage (LS)
Là 1 web storage object, cho phép lưu dữ liệu ở client (Browser) dưới dạng key/value. Các api được cung cấp tương tự như 1 object có kiểu dữ liệu Map.
Window.localStorage ~= new Map<string, string>();

Vài đặc điểm chính của LS:
- Data trong LS được persist, không bị mất kể cả sau khi restart browser.
Được thiết kế để lưu trữ thông tin đơn giản, gọn nhẹ phía client. Data trong LS có thể dễ dàng xem và chỉnh sửa bằng JS code hoặc devtools (có lẽ đây là 1 trong những lý do sinh ra secureLocalstorage - i guess).
- HTTP header sẽ không thể xem/sửa dữ liệu này. Nghĩa là về cơ bản, nó nằm ngoài control của server (không như cookies).- Mỗi domain/protocol/port (tạm gọi là origin) sẽ có 1 LS object riêng. Chẳng hạn như ở chat.zalo.me thì không thể access vào LS của web.telegram.org. Nhưng nếu cùng origin thì dù ở 2 tab/window riêng biệt, update data ở tab này sẽ ngay lập tức visible ở tab kia.
Vì key-value phải là string, cố tình lưu 1 object vào sẽ cho ra kết quả [object Object]. Vậy nếu muốn lưu object thì phải làm thế nào: value = JSON.stringigy(object). LS.setItem(key,value);- Không thể truy cập từ web workers or service workers.
- Dung lượng dành cho LS là không cố định, hầu hết browser cho phép min = 5Megabites of data.- LS không chịu sự quản lý của QuotaManager, tuy nhiên khi thiếu space, có thể Browser vẫn sẽ free up, khiến data trong LS bị mất. Sẽ nói chi tiết hơn trong topic QuotaManager.
Có 1 điều khá thú vị nhưng ít được xài của LS là cơ chế fire event:
Mỗi khi data được update trong LS, 1 event sẽ được fire ra cho tất cả window objects cùng DM, ngoại trừ thằng trigger update.
Event này chứa thông tin về: Key, oldValue, newValue, url, storageArea (LS trigger event). Nghĩa là bạn có thể tạo 1 app chat cho 2 window giao tiếp với nhau chỉ với LS (hình minh hoạ).

# 3: Storage -Quota Manager
Tài liệu này đề cập đến chromium, các engine khác (quantum, WebKit, …) có thể không giống.
Mỗi origin sẽ được cấp 1 quota để dùng cho việc lưu trữ dữ liệu. Số lượng quota được cấp về cơ bản là không cố định, tùy thuộc vào tổng lượng disk space đang có. Riêng với app như Zalo, lâu lâu sẽ bị đem ra đấm vì lượng usage nhiều vl. Sau khi đấm xong sẽ làm giảm usage và user thấy mất message thì bắt đầu lên J2Team chửi: Dev Zalo làm cái app thua cả mấy đứa sinh viên =]] . Khi quota vượt giới hạn thì sẽ ném ra 1 lỗi QuotaExceededError. Nạn nhân của vụ clear data này có thể là Indexed DB, Cache API, WebSQL, …
Về cơ bản chromium khi lưu data cũng đã compress giúp giảm size đáng kể. Nhưng khi túng thiếu thì vẫn cứ đâm chém như thường, theo 1 vài quy luật như sau:
Thứ nhất: Chrome sẽ dựa trên total available disk space (TA) và os là gì. Sẽ ra được con số có thể xài để làm ‘pool’. tạm gọi là TP (total pool). Mỗi origin trong đó sẽ xài 1 phần của TP. Mỗi origin đã xài tạm gọi là OQ (origin quota).
TA: Tùy máy user. Giả bộ máy trống 10GB
TP: Thường là 80% TA =8GB
OQ: Thường là 75% TP = 5.6GB
- Lúc này nếu app Zalo đang sử dụng 6GB indexed DB thì không nói nhiều database corrupt.
- Ở chế độ ẩn danh, thường thì data ở dạng memory hơn là disk. TP ít nhất là 10% TA hoặc 300MB. OQ = 1/3 TP.đô Ae v
- Ae vô đây đọc thêm source để kiểm chứng: https://source.chromium.org/chromium/chromium/src/+/main:storage/browser/quota/quota_settings.cc;l=26
Thứ 2:  Khi 1 origin (OQ) quá mức quy định, data sẽ không thể lưu được nữa. Mn sẽ thấy là app Zalo bị chat không được, chậm, lag các kiểu. Data của nó phải được giải phóng để xài tiếp.
Thứ 3: Mặc định storage sẽ ở dạng best effort, data sẽ ngon lành cho đến khi browser run on low space (usage ≥TP). Lúc này origin nào ít truy cập gần đây nhất sẽ được đem ra đấm. Data dạng persistent sẽ tạm sống sót.
Thứ 4: Một khi origin nào được treo án tử, tất cả quota-managed data của nó sẽ bay màu (Indexed DB, Cache API, …)
Lưu ý:
- Local storage, Cookies, .. quản lý bởi Storage Partition, không phải Quota Manager như nãy giờ trình bày.
- Có 2 khái niệm về persistent. Khái niệm trình bày ở trên thì không hẳn là persistent cho lắm. Có loại nữa là PERSISTENT: Không giống như phần đã trình bày. Khi request PERSISTENT và được granted, data sẽ không bị xóa khi storage bị vô chế độ running low. Mà này cũng khai tử r: https://chromestatus.com/feature/5176235376246784?context=myfeatures
navigator.webkitPersistentStorage.requestQuota(
500*1024*1024, // 500MB
granted => console.log(granted ${granted} bytes),
error =>err
);
Thảo luận:
Bạn có biết vì sao lại chọn TP ~ 10% hoặc 300MB ở chế độ ẩn danh không?
Zalo đã làm những gì để giảm thiểu ảnh hưởng của những cuộc truy sát này?
# Short & Long Polling

Short: Send after some small amount of time (ex: 1000ms)

Long: Send then hold for amount of time then response, after receive data, immidietly send another request, else not.

# Socket

After connection established, a socket pipe is created - full duplex persistent

### PingPong

Both try to ping after interval, close if not receive

# Offline messaging

local save last ID -> request to server from that ID + 1 then update to local DB

authen with Socket establish

set cookie with origin socket so it comes along with cookie to authen

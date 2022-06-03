# Electron use HashRouter cause

Electron does not handle history and works with the synchronized URL, BrowseHistory does not work with electron, therefore you must use HashRouter that if you synchronize your URL with a UI that is (windows.location.hash).

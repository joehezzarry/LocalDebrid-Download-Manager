# LocalDebrid Capture - browser extension

Works in Chrome, Edge, Brave, Opera and other Chromium browsers (not Firefox). It needs the LocalDebrid app running on the same PC.

## What it does
* **Captures downloads** like IDM: when your browser starts a download (known file types, or anything over the size you set, or everything) it cancels the browser's copy and hands the link - with your cookies, referrer and user-agent - to LocalDebrid, which downloads it with several connections. Logged-in downloads work because the cookie is forwarded.
* **Right-click menu:** *Download with LocalDebrid*, *Resolve link*, *Download this media*, *Send this page* (finds files on it), *Music & Video: grab this page* (yt-dlp).
* **Video detector:** the toolbar badge counts videos/audio/streams found on the page; the popup lists them with a Download / Grab button.
* **Fails safe:** if LocalDebrid isn't running or the pairing code is wrong, nothing is intercepted - the browser downloads normally.

## Install
**From the Chrome Web Store** (once listed): open **Extension** in LocalDebrid -> **Add to Chrome** -> click **Allow** in LocalDebrid when it asks "Allow your browser to connect?" (it asks by itself right after the install; missed it? click the extension's icon -> **Connect automatically**).

**Manually (developer mode):**
1. Start LocalDebrid and open **Extension** in the sidebar.
2. Click **Copy chrome://extensions**, click **Open Chrome**, then in Chrome press Ctrl+L, Ctrl+V, Enter (Chrome does not let other programs open that page).
3. Switch on **Developer mode** (toggle, top-right). Click **Load unpacked** (top-left). In the window that opens, paste the folder path (`%LOCALAPPDATA%\LocalDebrid\extension`, shown on the Extension page with a **Copy path** button) into the address bar, press Enter and click **Select Folder** - choose the folder called `extension` itself, the one containing `manifest.json`.
4. LocalDebrid immediately asks **Allow your browser to connect?** - click **Allow**. The status on the Extension page turns green. (Missed it or it timed out? Click the LocalDebrid toolbar icon - puzzle-piece icon if hidden - then **Connect automatically**. A pairing code can be pasted instead.)

Chrome shows a "disable developer mode extensions" notice when it starts - that is normal for extensions loaded this way; the store install doesn't have it.

## Updates
The app keeps `%LOCALAPPDATA%\LocalDebrid\extension` equal to the extension bundled in the app. When LocalDebrid updates itself, the extension notices the newer version on its next check-in and reloads itself - nothing to do.

## Security model
* The extension talks **only** to `127.0.0.1` ports 8765-8774 (the app), never to any other server.
* Every request must carry the pairing code (random, stored on the PC). The code is handed to an extension only after you click **Allow** in the app (or you paste it yourself). A website - even one that guesses the port - cannot use it: the app refuses web origins and checks the Host header.
* The extension token can only *send links*; it cannot read your downloads, settings, license or anything else.
* `<all_urls>` exists to see media requests and referrers on any site; the optional `cookies` permission is requested only when you turn on "Send cookies" and exists solely to forward your session to the downloader.

## Browser stores
Chrome Web Store publishing is documented in [`CHROME_STORE.md`](CHROME_STORE.md) (all listing text and images are prepared in `docs/chrome-store/`). The privacy policy is [`PRIVACY.md`](../PRIVACY.md). Edge Add-ons (free, https://partner.microsoft.com/dashboard/microsoftedge) accepts the same zip.

# LocalDebrid Capture - browser extension

Works in Chrome, Edge, Brave, Opera and other Chromium browsers (not Firefox). It needs the LocalDebrid app running on the same PC.

## What it does
* **Captures downloads** like IDM: when your browser starts a download (known file types, or anything over the size you set, or everything) it cancels the browser's copy and hands the link - with your cookies, referrer and user-agent - to LocalDebrid, which downloads it with several connections. Logged-in downloads work because the cookie is forwarded.
* **Right-click menu:** *Download with LocalDebrid*, *Resolve link*, *Download this media*, *Send this page* (finds files on it), *Music & Video: grab this page* (yt-dlp).
* **Popup:** *Connected · version*, a **Capture downloads** switch, **Media on this page** (the video plus files the page plays) with one-click download, and **All links / All images / All videos** to send everything on the page to LocalDebrid. Settings are behind the gear icon.
* **Fails safe:** if LocalDebrid isn't running, nothing is intercepted - the browser downloads normally.

## How it connects
LocalDebrid registers a small **browser helper** (native messaging) for Chrome, Edge, Brave, Chromium and Vivaldi when it starts. The browser lets only the LocalDebrid extension use it; the helper hands the extension the app's connection details and starts the app if it is closed. On top of that, LocalDebrid 1.5.0+ recognises the official extension (its store ID) by itself. So there are no pairing codes, nothing to allow and no notifications. (Only an extension with a different ID, or an app older than 1.5.0, still asks once: *Allow your browser to connect?*)

## Video button
A **Download** button sits at the top-right of the video player (YouTube and most video sites). Click it: **Best quality** downloads at once; while you look, LocalDebrid lists the qualities the video offers (2160p, 1440p, 1080p, 720p... always MP4 with sound) with their sizes, plus **Audio only (MP3)**. LocalDebrid downloads it and notifies you when it's done.

## Install
**From the Chrome Web Store** ([LocalDebrid Capture](https://chromewebstore.google.com/detail/localdebrid-capture/lahldebcicjghaookmeolhchdfpelafa)): open **Extension** in LocalDebrid -> **Add to Chrome**. That's it - it connects by itself.

**Manually (developer mode):**
1. Start LocalDebrid and open **Extension** in the sidebar.
2. Click **Copy chrome://extensions**, click **Open Chrome**, then in Chrome press Ctrl+L, Ctrl+V, Enter (Chrome does not let other programs open that page).
3. Switch on **Developer mode** (toggle, top-right). Click **Load unpacked** (top-left). In the window that opens, paste the folder path (`%LOCALAPPDATA%\LocalDebrid\extension`, shown on the Extension page with a **Copy path** button) into the address bar, press Enter and click **Select Folder** - choose the folder called `extension` itself, the one containing `manifest.json`.
4. Done - the folder carries the official extension ID, so it connects by itself and the status on the Extension page turns green.

Chrome shows a "disable developer mode extensions" notice when it starts - that is normal for extensions loaded this way; the store install doesn't have it.

## Updates
The app keeps `%LOCALAPPDATA%\LocalDebrid\extension` equal to the extension bundled in the app. When LocalDebrid updates itself, the extension notices the newer version on its next check-in and reloads itself - nothing to do.

## Security model
* The extension talks **only** to `127.0.0.1` ports 8765-8774 (the app), never to any other server.
* Requests must come from the official extension (the browser sets its `chrome-extension://` origin; web pages can't fake it) or carry the pairing code (random, stored on the PC; handed to other extensions only after you click **Allow** in the app). A website - even one that guesses the port - cannot use it: the app refuses web origins and checks the Host header.
* The extension token can only *send links*; it cannot read your downloads, settings, license or anything else.
* `<all_urls>` exists to see media requests and referrers on any site; the optional `cookies` permission is requested only when you turn on "Send cookies" and exists solely to forward your session to the downloader.

## Browser stores
Chrome Web Store publishing is documented in [`CHROME_STORE.md`](CHROME_STORE.md) (all listing text and images are prepared in `docs/chrome-store/`). The privacy policy is [`PRIVACY.md`](../PRIVACY.md). Edge Add-ons (free, https://partner.microsoft.com/dashboard/microsoftedge) accepts the same zip.

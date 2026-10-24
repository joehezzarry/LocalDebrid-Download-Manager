# LocalDebrid Capture - browser extension

Works in Chrome, Edge, Brave, Opera and other Chromium browsers (not Firefox). It needs the LocalDebrid app running on the same PC.

## What it does
* **Captures downloads** like IDM: when your browser starts a download (known file types, or anything over the size you set, or everything) it cancels the browser's copy and hands the link - with your cookies, referrer and user-agent - to LocalDebrid, which downloads it with several connections. Logged-in downloads work because the cookie is forwarded.
* **Right-click menu:** *Download with LocalDebrid*, *Resolve link*, *Download this media*, *Send this page* (finds files on it), *Music & Video: grab this page* (yt-dlp).
* **Video detector:** the toolbar badge counts videos/audio/streams found on the page; the popup lists them with a Download / Grab button.
* **Fails safe:** if LocalDebrid isn't running or the pairing code is wrong, nothing is intercepted - the browser downloads normally.

## Install (friends)
1. Start LocalDebrid, open **Settings -> Browser**.
2. Browser extensions page (`chrome://extensions` or `edge://extensions`) -> turn on **Developer mode** -> **Load unpacked** -> pick the folder shown in Settings -> Browser (`%LOCALAPPDATA%\LocalDebrid\extension`).
3. Click the LocalDebrid toolbar icon, paste the **pairing code** from the same Settings page. The dot turns green: connected.

Chrome shows a "disable developer mode extensions" notice when it starts - that is normal for extensions loaded this way (see the store option below to get rid of it).

## Updates
The app keeps `%LOCALAPPDATA%\LocalDebrid\extension` equal to the extension bundled in the app. When LocalDebrid updates itself, the extension notices the newer version on its next check-in and reloads itself - nothing to do.

## Security model
* The extension talks **only** to `127.0.0.1` ports 8765-8774 (the app), never to any other server.
* Every request must carry the pairing code (random, stored on the PC, replaceable with "New code" in Settings). A website - even one that guesses the port - cannot use it: the app refuses web origins and checks the Host header.
* The extension token can only *send links*; it cannot read your downloads, settings, license or anything else.
* `cookies` + `<all_urls>` permissions exist solely to forward your browser session to the downloader for sites you download from.

## Optional: publish in a browser store (removes the developer-mode notice, installs in one click)
Needs your own developer account, so I can't do it for you:
* **Chrome Web Store** - $5 one-time fee, https://chrome.google.com/webstore/devconsole . Upload `dist_pro\LocalDebrid-Extension.zip`. Choose visibility **Unlisted** (only people with the link can install; not searchable). Review usually takes a few days. Store updates then replace the manual folder.
* **Edge Add-ons** - free, https://partner.microsoft.com/dashboard/microsoftedge . Same zip.

Suggested text for the listing:
* **Summary:** Send downloads and videos from your browser to the LocalDebrid app on your PC.
* **Single purpose:** Capture downloads/media links in the browser and send them to the LocalDebrid desktop app running on the same computer.
* **Permission justifications:** `downloads` - detect and hand over downloads; `contextMenus` - the right-click actions; `storage` - remember the pairing code and settings; `cookies` + host access `<all_urls>` - forward the user's own session cookies to the local downloader so logged-in downloads work, and detect media requests on pages; `webRequest` - read (not modify) response headers to spot video/audio files.
* **Privacy policy (short):** The extension does not collect, store remotely or transmit personal data. All data (pairing code, settings) stays in the browser; links and cookies are sent only to the LocalDebrid app on the same PC (127.0.0.1) and nowhere else. No analytics, no ads, no third parties.

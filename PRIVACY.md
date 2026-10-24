# Privacy policy — LocalDebrid and LocalDebrid Capture

_Last updated: 25 October 2026_

LocalDebrid is a download manager that runs on your own Windows PC. **LocalDebrid Capture** is its optional browser
extension. The short version: **your data stays on your computer. We run no servers, collect no analytics and sell nothing.**

## LocalDebrid Capture (the browser extension)

**What it does:** it notices downloads and videos in your browser and hands them to the LocalDebrid app running on the
same PC, so the app can download them.

**What it handles, and where it goes**
- The address of a download, video or page that you send (or that the extension captures as a browser download), its
  file name, the page you were on (referrer) and your browser's user-agent text.
- Optionally, **cookies for that site** — only if you allow the optional "cookies" permission, so that downloads from
  sites you are signed in to work.
- All of this is sent **only to `127.0.0.1` (the LocalDebrid app on your own PC)**, over a local connection protected by a
  pairing code you approve inside the app. It is never sent to the developer, to Google or to any other server.

**What it stores:** its settings and the pairing code, in your browser's extension storage on your PC, and — for the
current browser session only — a short list of videos detected on each open tab. Removing the extension removes all of it.

**What it does not do:** no analytics or telemetry, no advertising, no tracking, no reading of page content, no remote
code, no sharing or selling of data.

**Permissions, in plain words:** _downloads_ (to hand a download to the app), _contextMenus_ (the right-click
"Download with LocalDebrid" entries), _storage_ (your settings), _webRequest_ + access to websites (to notice video
and audio files loading on a page, and to pass the right referrer to the app), and optionally _cookies_.

## LocalDebrid (the app)

- Downloads, history and settings are stored on your PC.
- The app contacts only: the websites you ask it to download from; GitHub (to check for app updates and, for Pro keys,
  the licence revocation list — no personal data is sent); and Real-Debrid **only if you add your own token**
  (the token is stored on your PC and sent only to Real-Debrid).
- No account is needed and nothing is uploaded to the developer.

## Your choices
Remove the extension or uninstall the app at any time; delete the data folder `%LOCALAPPDATA%\LocalDebrid` to erase the rest.

## Contact
Questions about this policy: the repository owner, https://github.com/joehezzarry

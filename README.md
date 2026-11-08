# Flamecraft Duals — GitHub Pages build

Unofficial fan-made digital adaptation. Pass-and-play on one device, or online between two devices with a room code.
This build is 100% static, so it runs on GitHub Pages. (The `api.php` version is for PHP hosts; do not upload it here.)

## Publish on GitHub Pages
1. Create a new public repository on GitHub (e.g. `flamecraft-duals`).
2. Upload `index.html` to the repository root (Add file → Upload files → Commit).
3. Repository → Settings → Pages → "Build and deployment": Source = "Deploy from a branch", Branch = `main`, folder = `/ (root)` → Save.
4. After a minute the game is live at `https://<your-username>.github.io/<repo-name>/`.

## How online play works
- Player 1 clicks "Create room" and shares the 6-character code. Player 2 clicks "Join room" and enters it.
- Browsers connect directly to each other (WebRTC via PeerJS). The free public PeerJS broker is only used to introduce them; no game data is stored anywhere except in the two browsers.
- Each browser saves the game locally, so reloading a tab resumes the game. Keep the tab open during play (phones: stay in the browser).

## Limits to know about
- The free PeerJS broker has no uptime guarantee. To avoid depending on it, host your own PeerServer and set `PEER_SERVER` near the top of the networking section in `index.html`.
- Default connections use STUN only. If both players are behind strict networks (some mobile carriers, work or school Wi-Fi), a direct connection can fail; add a TURN server to `ICE_SERVERS` in `index.html` if that happens.
- PeerJS is loaded from cdnjs (version pinned to 1.5.5). To self-host it, save `peerjs.min.js` next to `index.html`; it is used automatically if the CDN is unreachable.

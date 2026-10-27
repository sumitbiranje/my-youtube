# Tune Box

A liquid-glass YouTube music player for GitHub Pages. Playback uses the official YouTube IFrame Player API. There is no backend and no build step.

## Features

- Liquid-glass interface: translucent blurred panels, a backdrop that takes its colour from the current song's artwork, and highlights that follow your pointer
- Paste a YouTube video or playlist link, or search by name
- Queue with shuffle, repeat (off, all, one), play next, reorder, remove, and a one-tap queue shuffle
- Liked songs and play history
- Saved playlists in your browser, with JSON export and import
- Share your queue as a link
- Sleep timer (15, 30, 45, 60 minutes, or after the current song) and playback speed
- Accent colour, blur and glass strength settings
- Mini player that appears when you scroll past the video
- Installable as an app on phones and desktops
- Media-key and lock-screen controls

Keyboard shortcuts: Space (play or pause), N and P (next, previous), arrow keys (seek and volume), M (mute), L (like), S (shuffle), R (repeat), / (search).

## Deploy on GitHub Pages

1. Put `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png` and `icon-512.png` in the root of the `main` branch.
2. Open Settings, then Pages. Under Build and deployment, choose "Deploy from a branch", then `main` and `/ (root)`.
3. After a minute the site is live at `https://<your-username>.github.io/<repo-name>/`.

## Search and playlist import (optional)

Pasting a video link works without any setup. Search and playlist import need a YouTube Data API v3 key:

1. In Google Cloud Console, create a project and enable "YouTube Data API v3".
2. Create an API key and restrict it to your site's address (HTTP referrers), for example `https://<your-username>.github.io/*`.
3. Paste the key into the Settings tab of the app. It is stored only in your browser.

The default quota allows roughly 100 searches per day, since each search costs 100 units.

## Notes

- The player uses the YouTube embed, so your browser still connects to YouTube. This app does not hide that.
- Some videos disable embedding. The app skips them automatically.
- Saved data uses keys that start with `tunebox:`, so it doesn't touch other pages on the same `github.io` address. "Delete" in Settings removes only those keys.
- Never commit your API key to the repository.

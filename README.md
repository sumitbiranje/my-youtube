# Tune Box

A full-screen, liquid-glass YouTube music player for GitHub Pages. Playback uses the official YouTube IFrame Player API. There is no backend and no build step.

## Layout

- **Desktop (1024px and wider):** glass sidebar, a song list in the middle, and the video with player controls on the right.
- **Phones and tablets:** the video stays pinned at the top, a glass player bar and tab bar float at the bottom, and full controls open in a sheet. The video stays visible at all times.
- **Phones held sideways:** video and tab bar on the left, the list and player bar on the right.

## Liquid glass

- Clear glass with light blur (6px by default) on navigation and controls only. Songs and lists sit on their own layer underneath, so they stay sharp.
- In Chrome and Edge, a lens effect bends whatever scrolls behind the glass at its edges. Other browsers show the clear glass without it.
- A rim light and a highlight that follows your pointer.
- The backdrop takes its colour from the current song's artwork.
- Settings let you change the accent colour, blur, tint and refraction. A "Lighter effects" mode turns on automatically on low-end devices. Reduced transparency and reduced motion settings are respected.

## Features

- Paste a YouTube video or playlist link, or search by name
- Queue with shuffle, repeat (off, all, one), play next, reorder and remove
- Liked songs, play history and saved playlists, with JSON export and import
- Share your queue as a link
- Sleep timer (15 to 60 minutes, or after the current song) and playback speed
- Section links you can bookmark (for example `#/liked`), and the back button works
- Installable as an app on phones and desktops, with media-key and lock-screen controls

Keyboard shortcuts: Space (play or pause), N and P (next, previous), arrow keys (seek and volume), M (mute), L (like), S (shuffle), R (repeat), / (search), Esc (close player controls).

## Deploy on GitHub Pages

1. Put `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png` and `icon-512.png` in the root of the `main` branch.
2. Open Settings, then Pages. Under Build and deployment, choose "Deploy from a branch", then `main` and `/ (root)`.
3. After a minute the site is live at `https://<your-username>.github.io/<repo-name>/`.

## Search and playlist import (optional)

Pasting a video link works without any setup. Search and playlist import need a YouTube Data API v3 key:

1. In Google Cloud Console, create a project and enable "YouTube Data API v3".
2. Create an API key and restrict it to your site's address (HTTP referrers), for example `https://<your-username>.github.io/*`.
3. Paste the key into the Settings section of the app. It is stored only in your browser.

The default quota allows roughly 100 searches per day, since each search costs 100 units.

## Notes

- The player uses the YouTube embed, so your browser still connects to YouTube. This app does not hide that.
- Some videos disable embedding. The app skips them automatically.
- Saved data uses keys that start with `tunebox:`, so it doesn't touch other pages on the same `github.io` address. "Delete saved data" in Settings removes only those keys.
- Never commit your API key to the repository.

## Credits

Design decisions (colour tokens, touch-target, motion and accessibility rules) were guided by [UI UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) (MIT License, Copyright (c) 2024 Next Level Builder). No code from that project is included here.

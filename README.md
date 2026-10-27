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

## Ambient glow

Light from the video spills around the player, similar to YouTube's ambient mode. YouTube's own version reads live video frames, which a web page can't do with an embedded player. Tune Box uses the still frames YouTube publishes for each video instead: the cover, then frames from about 25%, 50% and 75% through. It cross-fades between them as the song plays and tints the page with the video's main colour. Turn it off under Settings, then Look.

**Live ambient (optional, off by default):** for a glow that follows every scene, turn on "Live ambient" in Settings, then Look. It plays a second, muted copy of the video inside the blurred glow and keeps it in step with the main player (pause, seek, speed and song changes). It uses about twice the data and more battery, so it suits computers and recent phones. It stays off in Lighter effects mode, and if a device won't play two videos at once, Tune Box switches back to the still frames on its own.
- Settings let you change the accent colour, blur, tint and refraction. A "Lighter effects" mode turns on automatically on low-end devices. Reduced transparency and reduced motion settings are respected.

## Features

- Paste a YouTube video or playlist link, or search by name
- Queue with shuffle, repeat (off, all, one), play next, reorder and remove
- **Up next:** YouTube's own Mix for the current song appears under your queue. With Autoplay on, it keeps playing from there when the queue ends. No API key needed; if a song has no Mix, it falls back to more songs by the same artist (needs an API key or sign-in).
- **Previous and Next like YouTube:** Previous goes back to the song you actually heard before (after shuffle or a song picked from anywhere), Next retraces your steps after going back, and shuffle plays every queued song once before repeating.
- Liked songs, play history and saved playlists, with JSON export and import
- Import your liked videos and playlists from your YouTube account (see below)
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

## Connect your YouTube account (optional)

Signing in lets Tune Box import your liked videos, play or copy your YouTube playlists, and search without an API key. It asks Google for read-only YouTube access. The sign-in token stays in memory, is never saved, and expires after about an hour, after which Tune Box asks Google again.

Set it up once, in the same Google Cloud project as your API key:

1. Open APIs & Services, then OAuth consent screen. Choose External, fill in the app name and your email, and add the scope `https://www.googleapis.com/auth/youtube.readonly`.
2. Leave the app in Testing, and add your own Google account under Test users.
3. Open Credentials, then Create credentials, then OAuth client ID. Choose "Web application" and add `https://<your-username>.github.io` under Authorized JavaScript origins (no path, no trailing slash). No redirect URI is needed.
4. Copy the client ID (it ends in `.apps.googleusercontent.com`). In Tune Box, open Settings, then YouTube account, paste it, choose "Save client ID", then "Connect YouTube account".

Google shows an "unverified app" warning because the app is in Testing. That's expected for a personal app: choose Continue. Allow pop-ups for your site if the sign-in window doesn't open.

After connecting:

- **Liked songs:** choose "Import from YouTube". By default only music videos are imported; switch off "Import music videos only" in Settings to bring in everything. Songs you like in YouTube Music usually appear in your YouTube likes too.
- **Playlists:** choose "Load from YouTube" to list your playlists, then play one, add it to the queue, or save a copy in Tune Box.

YouTube Music's automatic playlists (like "Liked music" or mixes) aren't available through the YouTube API, so they can't be imported.

## Notes

- The player uses the YouTube embed, so your browser still connects to YouTube. This app does not hide that.
- Some videos disable embedding. The app skips them automatically.
- The YouTube API no longer returns related videos, so Up next reads the song's Mix through a hidden helper player that is loaded but never played. Live ambient plays a blurred second player. Both are unofficial uses of YouTube's embed and may stop working if YouTube changes it, and blurring a player isn't allowed under YouTube's embed rules. They're meant for personal use.
- Saved data uses keys that start with `tunebox:`, so it doesn't touch other pages on the same `github.io` address. "Delete saved data" in Settings removes only those keys.
- Never commit your API key to the repository.

## Credits

Design decisions (colour tokens, touch-target, motion and accessibility rules) were guided by [UI UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) (MIT License, Copyright (c) 2024 Next Level Builder). No code from that project is included here.

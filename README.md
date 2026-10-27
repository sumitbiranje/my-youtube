# Tune Box

A single-file YouTube music player for GitHub Pages. Playback uses the official YouTube IFrame Player API. There is no backend and no build step.

## Features

- Paste a YouTube video or playlist link, or search by name
- Queue with shuffle, repeat (off / all / one), reorder and remove
- Saved playlists in your browser, with JSON export and import
- Media-key and lock-screen controls (Media Session API)
- Keyboard shortcuts: Space (play/pause), N (next), P (previous)
- `?add_song=<YouTube link>` queues a song when the page opens

## Deploy on GitHub Pages

1. Create a repository and add `index.html` to the root of the `main` branch.
2. Open Settings, then Pages. Under Build and deployment, choose "Deploy from a branch", then `main` and `/ (root)`.
3. After a minute your site is live at `https://<your-username>.github.io/<repo-name>/`.

## Search and playlist import (optional)

Pasting a video link works without any setup. Search and playlist import need a YouTube Data API v3 key:

1. In Google Cloud Console, create a project and enable "YouTube Data API v3".
2. Create an API key and restrict it to your site's address (HTTP referrers), for example `https://<your-username>.github.io/*`.
3. Paste the key into the Settings tab of the app. It is stored only in your browser's local storage.

The default quota allows roughly 100 searches per day, since each search costs 100 units.

## Notes

- The player uses the YouTube embed, so your browser still connects to YouTube. This app does not hide that.
- Some videos disable embedding. The app skips them automatically.
- Because the key is entered in the browser, never commit it to the repository.

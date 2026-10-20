# 💖 A little CE Pop Quiz

A small, hand-made quiz + proposal page. Pure static HTML/CSS/JS — no build step, no dependencies.

## Files

| File | What it is |
|------|------------|
| `index.html` | The entire page — markup, styles, and script all in one file (~33 KB) |
| `song.mp3` | The ~80 second clip that plays on the "You said yes!" screen (~1.1 MB) |
| `.nojekyll` | Empty marker so GitHub Pages serves the folder as-is instead of running it through Jekyll |

> **`song.mp3` must stay next to `index.html`.** The page loads it with a *relative* path
> (`audio: "song.mp3"`), so as long as both files sit in the same folder it works — whether
> you open it locally, or serve it from GitHub Pages. You do **not** need to embed the audio
> into the HTML as a base64 blob.

## Run it locally

Double-click `index.html`, or serve the folder:

```powershell
python -m http.server 8000
# then open http://localhost:8000
```

## Publish free with GitHub Pages

1. Create a repo at <https://github.com/new> (name it e.g. `proposal`).
2. Upload `index.html`, `song.mp3` and `.nojekyll` to the repo root.
3. **Settings → Pages → Source: `Deploy from a branch` → Branch: `main` / Folder: `/ (root)` → Save.**
4. Your site goes live at `https://<your-username>.github.io/<repo-name>/` in about a minute.

GitHub Pages has no file-size problem at this scale, and it serves `.mp3` with the correct
`audio/mpeg` MIME type, so `<audio>` playback works normally.

## Personalize

Open `index.html` and edit the block at the top of the `<script>`:

```js
var HER  = "Miss Lee";   // her name
var ME   = "Vince";      // your name
var SONG = {title:"Pwede Ka Ba", artist:"Frank Ely", spotify:"", audio:"song.mp3", clipSeconds:80};
var REPLY = {sms:"", email:""};   // e.g. sms:"+639171234567"
var LINES = [ /* the lines that type out one by one */ ];
var DATES = [ /* the first-date options */ ];
```

Set `REPLY.sms` or `REPLY.email` to enable the one-tap "Send my pick 💌" button on the
final screen. Leave them blank and the page just tells her to message you instead.

## Notes

- Audio is gated behind a user interaction (browsers block autoplay), so the song starts
  on the "Yes 💖" tap.
- Haptics use `navigator.vibrate()`, which only fires on Android — iOS ignores it.
- `prefers-reduced-motion` is respected for the CSS animations.

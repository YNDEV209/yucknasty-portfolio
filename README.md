# Yuck Nasty — Portfolio

Single-page dark/gritty portfolio site. Deploys as a static site to Vercel.

## Structure

- `index.html` — the entire site (HTML + CSS + JS, with all thumbnails and 24 VJ clip preview loops embedded as base64)
- `Visualizers/` — three full music visualizer MP4s (web-encoded H.264)
- `vercel.json` — caching headers for long-lived media

## Local preview

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

## Deploying updates

After editing `index.html`:

```bash
git add -A
git commit -m "Update copy / styling"
git push
```

Vercel picks up the push and redeploys automatically (usually within 30 seconds).

## Editing

All content is in `index.html`:

- **Client list** — look for `INDEX / 03` in the HTML (around the index strip section)
- **Contact email** — search for `yucknasty209@gmail.com`
- **VJ clip titles** — inside the `const clips = [...]` JavaScript array
- **Visualizer videos** — the three `<video>` tags in the `#visualizers` section

## Re-encoding video

To re-compress a visualizer for web:

```bash
ffmpeg -i input.mp4 \
  -c:v libx264 -preset fast -crf 28 \
  -maxrate 4200k -bufsize 8400k \
  -pix_fmt yuv420p -movflags +faststart \
  -c:a aac -b:a 128k \
  output.mp4
```

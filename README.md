# Sugrowth Public Website

Static public website for `sugrowth.ca`.

## Branches

- `main`: repository baseline.
- `site`: production website branch.
- `site-test`: staging and iteration branch.

## Local Preview

The site is plain HTML/CSS/JS. You can preview it by serving the repo root:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

## Deploy

Use Cloudflare Pages or GitHub Pages with the repo root as the published directory. See `DEPLOYMENT.md` for domain and email setup notes.

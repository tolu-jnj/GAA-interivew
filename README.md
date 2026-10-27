# GAA Lead Digital Analyst – Interview Prep App

A single-page app (HTML + CSS + JS, no external libraries or external network calls). It loads canonical question data from same-origin JSON files.
Notes, confidence ratings and "ready" checkboxes save in each viewer's own browser (localStorage). Nothing is sent to a server.

## Files
| File | Purpose |
|---|---|
| `index.html` | Existing single-page app shell and interactions |
| `questions.json` | Canonical Answer Bank data |
| `PANEL_QUESTIONS.json` | Questions to Ask data |
| `PATCH_QUESTIONS.json` | Additive question updates; merge by stable `id` |
| `app.py` | Python standard-library web server (port 8888) |
| `app.sh` | Domino App launch script |

## Test locally
1. `python app.py`
2. Open http://localhost:8888
3. Check tabs, answer reveal, search and all three filters, both timers, panel-question selections, whiteboard notes, checklist state, and persistence after refresh.

## Deployment target
The existing Domino app remains the internal deployment. It uses the standard-library Python server and must remain restricted to the project owner or explicitly named users. GitHub Pages is a separate, public static deployment approved for the current interview-prep content; do not add restricted material to its files.

The app makes same-origin requests only for `questions.json` and `PANEL_QUESTIONS.json`; it has no external runtime dependencies or server-side user storage. Notes, confidence ratings, selections, and checklist state remain in each browser's local storage.

## Deploy to GitHub Pages
1. In **Settings → Pages**, set the build and deployment source to **GitHub Actions**.
2. Push to `main`; the workflow publishes `index.html`, `questions.json`, `PANEL_QUESTIONS.json`, and optional assets. It does not publish the Domino server or launcher.
3. Open https://tolu-jnj.github.io/GAA-interivew/ after the workflow succeeds.

## Deploy to Domino
1. Create a new Domino project (e.g. `gaa-interview-prep`). Set visibility to **Private**.
2. Upload `index.html`, `questions.json`, `PANEL_QUESTIONS.json`, `app.py`, and `app.sh` to the project root. `questions.json` and `PANEL_QUESTIONS.json` must be served from the same origin as the app.
3. Go to **Deployments → App** (or **Publish → App** on older versions).
4. Pick any standard Python environment and the smallest hardware tier. No packages needed.
5. Set the launch file to `app.sh`, then **Publish/Start**.
6. Set app permissions to **only you** (or named invitees). Do not make it visible to everyone.
7. Open the app URL and run the same checks as the local test.

## Troubleshooting
- **App never starts / 502**: check the logs show `Serving ... on 0.0.0.0:8888`. If your Domino version uses a different port, set the `PORT` env var or edit `app.py`.
- **Blank page**: confirm `index.html` sits next to `app.py` in the project root.
- **Notes don't persist**: the browser may be blocking storage for that domain. The app still works; it just won't remember notes.

## Data handling
Keep the Domino app private or restricted to named users. Reconfirm content approval before adding new sensitive material.

## Content maintenance
- `questions.json` is the canonical Answer Bank dataset. Each question has a stable `id`; merge updates by `id`, never by question text.
- Existing question records keep their `legacyStorageIndex`. Do not change or reuse it: it maps to the existing `lda_noteN`, `lda_confN`, and `lda_readyN` browser keys.
- `PATCH_QUESTIONS.json` contains additive/update records for the canonical bank. Merge by `id`, then validate JSON and ID uniqueness.
- `PANEL_QUESTIONS.json` is the source for the Questions to Ask tab.
- Panel Intel, Whiteboard, and Night-Before are curated app content. Keep panel themes labeled as role-based preparation inferences, not confirmed questions.

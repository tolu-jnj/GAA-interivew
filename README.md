# GAA Lead Digital Analyst – Interview Prep App

A single-page, self-contained app (HTML + CSS + JS, no external libraries, no network calls).
Notes, confidence ratings and "ready" checkboxes save in each viewer's own browser (localStorage). Nothing is sent to a server.

## Files
| File | Purpose |
|---|---|
| `index.html` | The whole app |
| `questions.json` | The question/answer bank as data (for editing or reuse) |
| `app.py` | Python standard-library web server (port 8888) |
| `app.sh` | Domino App launch script |

## Test locally (2 minutes)
1. `python app.py`
2. Open http://localhost:8888
3. Check: tabs switch, "Show answer" expands, search/filter works, both timers run, a note survives a page refresh.

(Or just double-click `index.html`. It works without a server.)

## Deploy to GitHub Pages
1. Push this repository to GitHub on the `main` branch.
2. In **Settings → Pages**, set the build and deployment source to **GitHub Actions**.
3. The workflow deploys `index.html` and, if present, the `assets/` directory on every push to `main`. You can also start it from **Actions → Deploy interview prep to GitHub Pages → Run workflow**.
4. After the workflow succeeds, open https://tolu-jnj.github.io/GAA-interivew/ and verify the app interactions.

The app has no server-side storage or external network calls. Interview notes, confidence ratings, and ready checkboxes stay in that browser's local storage.

## Deploy to Domino
1. Create a new Domino project (e.g. `gaa-interview-prep`). Set visibility to **Private**.
2. Upload `index.html`, `app.py`, `app.sh` (and optionally `questions.json`, `README.md`) to the project root.
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
The project owner has approved the current interview-prep content for GitHub Pages deployment. Reconfirm that approval before adding new sensitive material.

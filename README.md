# Expedia RE Internship Log — aerosol-action

A tiny static site that tracks your daily internship progress and doubles as a
shareable read-only page for your manager. No backend — GitHub itself is the
database.

## How it works

- `data/log.json` holds every day's entry (status, what you did, blockers,
  who you talked to, what you learned).
- `index.html` is the whole app. It reads `data/log.json` straight from
  GitHub to show the timeline. Anyone with the link sees this — no login.
- To **write** an entry, you unlock editing with a GitHub token (kept only in
  your own browser's local storage). Saving commits straight to
  `data/log.json` in this repo.
- Chris just opens the site. He never needs a token — he's always in
  view-only mode, always looking at the latest committed data.

## One-time setup (~5 minutes)

1. **Create a new GitHub repo** (public, so Pages + reads work without auth).
   Name it whatever you want, e.g. `aerosol-action-log`.

2. **Upload these three files** keeping the folder structure:
   - `index.html`
   - `data/log.json`
   - `README.md` (optional, just for your own reference)

3. **Edit `index.html`** — near the top of the `<script>` block, set:
   ```js
   const GITHUB_OWNER = "your-github-username";
   const GITHUB_REPO  = "aerosol-action-log"; // whatever you named the repo
   ```
   Commit that change.

4. **Enable GitHub Pages**: repo → Settings → Pages → Source: "Deploy from a
   branch" → Branch: `main`, folder: `/ (root)` → Save. Wait a minute or two;
   GitHub will give you a URL like:
   `https://your-github-username.github.io/aerosol-action-log/`

5. **Create a token so you can save entries**: GitHub → Settings (your
   account, not the repo) → Developer settings → Personal access tokens →
   Fine-grained tokens → Generate new token.
   - Repository access: **Only select repositories** → pick this one repo.
   - Permissions: **Contents → Read and write**. Leave everything else as
     "No access."
   - Generate, copy the token (starts with `github_pat_`).

6. **Open your deployed site**, tap the ⚙ in the bottom right, paste the
   token, save. Editing is now unlocked on this device only.

7. **Send Chris the plain URL** from step 4. He opens it and sees the
   timeline, always up to date, with zero setup on his end.

## Notes

- Only paste your token into a device you trust — anyone with it could write
  to this repo. Don't share the token itself, just the site URL.
- If you ever want to revoke access, delete the token from GitHub's token
  settings page, or tap ⚙ → "remove token / view-only mode" on your device.
- All history is just git history — nothing is ever silently lost.

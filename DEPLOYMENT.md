# Deployment process

## 1. Create the GitHub repository
1. Go to github.com → **New repository**.
2. Name it, e.g. `sahayak-vernacular-maths` — keep it **Public** if you
   want free Streamlit Cloud hosting, or **Private** if you'll deploy
   another way.
3. Do **not** initialize with a README (you already have one) — leave
   "Add a README" unchecked.
4. Click **Create repository** and copy the URL it gives you, e.g.
   `https://github.com/<your-username>/sahayak-vernacular-maths.git`

## 2. Push this project to it
From inside this project folder on your Mac:
```bash
git init
git add .
git commit -m "Initial commit: Sahayak vernacular maths assistant"
git branch -M main
git remote add origin https://github.com/<your-username>/sahayak-vernacular-maths.git
git push -u origin main
```
If asked to log in, use a GitHub Personal Access Token as the password
(GitHub Settings → Developer settings → Personal access tokens).

**Before pushing:** double-check `.streamlit/secrets.toml` is NOT
staged (`git status` should not list it — `.gitignore` already excludes
it). Only `secrets.toml.example` should be tracked.

## 3. Deploy on Streamlit Community Cloud (free)
1. Go to share.streamlit.io and sign in with GitHub.
2. Click **New app**, pick your repo, branch `main`, and set the main
   file path to `app.py`.
3. Before clicking Deploy, open **Advanced settings → Secrets** and
   paste in the contents of your real `secrets.toml` (Sarvam + Bhashini
   keys). This is how the app gets its keys in the cloud — you never
   commit the real file to GitHub.
4. Click **Deploy**. The app will build and give you a public URL like
   `https://sahayak-vernacular-maths.streamlit.app`.
5. If you update the dataset Excel file, it needs to be committed to
   the repo too (or loaded from cloud storage) so the deployed app can
   read it — Streamlit Cloud only sees what's in the GitHub repo.

## 4. Updating the live app later
Any time you push new commits to `main`, Streamlit Cloud auto-redeploys:
```bash
git add .
git commit -m "Describe your change"
git push
```

## 5. Getting your Bhashini keys wired up
You mentioned you already have your Bhashini **udyat** (User ID) and
**inference** (Ulca-Api-Key) keys. Put them in Streamlit secrets as:
```
BHASHINI_USER_ID = "..."
BHASHINI_API_KEY = "..."
```
`bhashini.py` in this repo uses them to call Bhashini's translation and
TTS pipelines for Santali. If Bhashini changes its model IDs for
Santali, you may need to adjust the `serviceId` lookup in
`bhashini.py` — check your Bhashini dashboard for the current pipeline
config.

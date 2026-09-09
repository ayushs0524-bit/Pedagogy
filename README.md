# Sahayak — Vernacular Maths Assistant (SIH26042 prototype)

AI-powered Hindi → Santali mathematics learning assistant for Class 3,
built for the Jharkhand mother-tongue primary education pilot.

## What's in this repo
- `app.py` — the Streamlit application (UI + Sarvam AI logic)
- `bhashini.py` — Bhashini (ULCA) client for Hindi→Santali translation and
  Santali text-to-speech (Sarvam's TTS voice does not cover Santali yet)
- `requirements.txt` — Python dependencies
- `Hindi_Santali_Maths_Dataset_Starter.xlsx` — local curriculum dataset
  (add your copy to the project root; see Notes)
- `.streamlit/secrets.toml.example` — template for your API keys

## Run locally
1. Clone the repo and `cd` into it.
2. Create a virtual environment (recommended):
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Copy the secrets template and fill in your real keys:
   ```bash
   cp .streamlit/secrets.toml.example .streamlit/secrets.toml
   ```
   Then edit `.streamlit/secrets.toml` with your Sarvam key and your
   Bhashini `BHASHINI_USER_ID` (udyat key) / `BHASHINI_API_KEY`
   (inference key).
5. Put `Hindi_Santali_Maths_Dataset_Starter.xlsx` in the project root.
6. Start the app:
   ```bash
   streamlit run app.py
   ```

## Deploying
See `DEPLOYMENT.md` for the full step-by-step process: creating the
GitHub repo, pushing this code, and deploying on Streamlit Community
Cloud.

## Notes
- This is a prototype. The dataset's native-speaker validation is
  still in progress — do not present the full dataset as validated.
- No API keys are committed to this repo. `.streamlit/secrets.toml` is
  git-ignored; only `secrets.toml.example` (no real keys) is tracked.
- Sarvam Bulbul v3 currently has no Santali voice, so Hindi audio is
  generated via Sarvam and Santali audio via Bhashini's TTS pipeline.
  If Bhashini keys are not configured, the Santali voice section is
  hidden and only Hindi audio plays.

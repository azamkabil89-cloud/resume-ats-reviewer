# ATS Resume Analyzer

A Streamlit app that compares a resume with a job description, estimates a match score, and suggests improvements. Gemini Flash provides AI feedback when a Gemini API key is configured. Without a key, the app uses a basic keyword-presence estimate.

## Features

- Upload PDF, DOCX, or TXT resumes (up to 5 MB)
- Compare a resume with a pasted job description
- View an estimated score, matched/missing keywords, strengths, and improvement tips
- Download the analysis as JSON
- Basic keyword fallback when Gemini is not configured

## Files

- `app.py` — Streamlit application
- `requirements.txt` — Python dependencies
- `README.md` — setup and deployment guide

## Run locally

1. Install Python 3.10 or newer.
2. Open a terminal in this folder.
3. Create and activate a virtual environment (recommended):

   **Windows PowerShell**
   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

4. Install dependencies:
   ```bash
   python -m pip install -r requirements.txt
   ```
5. (Recommended) Get a Gemini API key from Google AI Studio. Set it as an environment variable:

   **Windows PowerShell, current terminal only**
   ```powershell
   $env:GEMINI_API_KEY="YOUR_API_KEY_HERE"
   ```

   **macOS/Linux**
   ```bash
   export GEMINI_API_KEY="YOUR_API_KEY_HERE"
   ```

   Do not put your API key directly in `app.py`, GitHub, or any public repository.

6. Start the app:
   ```bash
   streamlit run app.py
   ```

If you do not configure a key, the app still runs with a basic keyword-match estimate; AI-generated feedback will not be available.

## Upload the files to GitHub using the website

1. Sign in at [GitHub](https://github.com/).
2. Select **+** (top right) → **New repository**.
3. Name it `ats-resume-analyzer`. Choose **Public** or **Private**, then click **Create repository**.
4. In the new repository, choose **Add file** → **Upload files**.
5. Upload `app.py`, `requirements.txt`, and `README.md` from this folder. Upload the files themselves, not a ZIP file.
6. Add a commit message such as `Add ATS resume analyzer app`, then click **Commit changes**.
7. Check that all three files appear in the repository root.

**Security:** Never upload `.env` files, API keys, passwords, or private resumes to GitHub.

## Deploy on Streamlit Community Cloud

1. Push the three files to GitHub using the steps above.
2. Visit [Streamlit Community Cloud](https://share.streamlit.io/) and sign in, usually with GitHub.
3. Click **Create app** (or **New app**), select your repository, branch (usually `main`), and main file path `app.py`.
4. Before deploying, open the app's **Advanced settings** / **Secrets** area (wording may change) and add:

   ```toml
   GEMINI_API_KEY = "YOUR_API_KEY_HERE"
   ```

   Keep the key in Streamlit secrets, not in a committed file.
5. Click **Deploy** and wait for the build to finish. If deployment fails, open the app's logs and check the first error, the Python version, and dependency installation.

## Important limitations

- ATS systems differ, so this is an estimate rather than an official or guaranteed score.
- Keyword matching alone cannot determine whether a candidate truly has a skill.
- Scanned/image-only PDFs may not contain extractable text; use OCR first.
- The app sends resume text to Google Gemini when AI analysis is enabled. Get appropriate consent and avoid uploading unnecessary sensitive data.

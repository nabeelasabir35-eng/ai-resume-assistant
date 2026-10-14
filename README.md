# ai-resume-assistant# 📄 AI Resume ATS Scorer

Upload a resume (PDF, DOCX or TXT) and get an **ATS score out of 100**, a score breakdown, prioritized improvements with example rewrites, and missing keywords. Optionally paste a job description to see how well your resume matches it. Built with **Streamlit** and **Google Gemini Flash**.

## Features

- Upload PDF, DOCX or TXT (max 5 MB)
- Overall ATS score plus a breakdown (formatting, keywords, experience, education, readability, and job-description match when provided)
- Prioritized improvements (High / Medium / Low) with concrete fixes
- Missing keyword suggestions
- Quick local checks: email, phone, LinkedIn/GitHub, key sections, length, metrics
- Downloadable Markdown report

> **Note:** The score is an AI-generated estimate, not the output of a real ATS. Use it as guidance. Real ATS products each score differently.

## Project structure

```
.
├── app.py             # Streamlit app
├── requirements.txt   # Python dependencies
└── README.md
```

## Run locally

1. **Get a free Gemini API key** at https://aistudio.google.com/apikey
2. **Create a virtual environment and install dependencies**
   ```bash
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. **Provide your API key** (any one of these):
   - Paste it in the app's sidebar, or
   - Set an environment variable:
     ```bash
     export GEMINI_API_KEY="your-key"      # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
     ```
   - Or create `.streamlit/secrets.toml`:
     ```toml
     GEMINI_API_KEY = "your-key"
     ```
4. **Start the app**
   ```bash
   streamlit run app.py
   ```

## Choosing the model

The sidebar has a **Model** field, defaulting to `gemini-flash-latest` (an alias for the newest Flash model). If you get a "model not found" error, check the current model names at https://ai.google.dev/gemini-api/docs/models and type one in.

## Push to GitHub

Create a **new empty repository** on GitHub first (no README, no .gitignore), then:

```bash
git init
printf "venv/\n__pycache__/\n.env\n.streamlit/secrets.toml\n" > .gitignore
git add .
git commit -m "Initial commit: AI Resume ATS Scorer"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

**Never commit your API key.** The `.gitignore` above keeps `secrets.toml` and `.env` out of the repo.

## Deploy on Streamlit Community Cloud (free)

1. Go to https://share.streamlit.io and sign in with GitHub.
2. Click **Create app** and choose **Deploy a public app from GitHub**.
3. Select your repository, branch `main`, and main file path `app.py`.
4. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**. After a minute or two you get a public `*.streamlit.app` URL.

To update the app later, just `git push`. Streamlit Cloud redeploys automatically.

## Troubleshooting

| Problem | Fix |
|---|---|
| "Very little text could be extracted" | Your resume is probably a scanned image. Export it as a text-based PDF or DOCX. |
| "API key looks invalid" | Re-copy the key from Google AI Studio; check there are no extra spaces. |
| "Rate limit or quota reached" | Wait a minute, or check your quota in Google AI Studio. |
| "Model was not found" | Change the model name in the sidebar. |
| `ModuleNotFoundError` on deploy | Make sure `requirements.txt` is in the repo root and committed. |

## Privacy

Resume text is sent to the Gemini API for analysis. The app does not store uploaded files. If you deploy it publicly, tell your users where their data goes.

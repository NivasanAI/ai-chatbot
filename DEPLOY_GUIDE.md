# 🚀 Deploy ExcelChat AI Online (Free)

## Overview
- **Backend** → Render.com (FastAPI) — gets a URL like `https://excелchat-ai.onrender.com`
- **Frontend** → GitHub Pages (HTML) — gets a URL like `https://yourusername.github.io/ai-chatbot`

---

## STEP 1 — Push code to GitHub

1. Go to https://github.com/new and create a new repository named `ai-chatbot`
2. Make it **Public**, click "Create repository"
3. Open Command Prompt and run:

```cmd
cd C:\Users\seeni\ai-chatbot
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/ai-chatbot.git
git push -u origin main
```

> Replace YOUR_USERNAME with your actual GitHub username

---

## STEP 2 — Deploy Backend on Render.com

1. Go to https://render.com and sign up (free) — use "Sign in with GitHub"
2. Click **"New +"** → **"Web Service"**
3. Connect your GitHub repo `ai-chatbot`
4. Fill in these settings:
   - **Name**: excелchat-ai
   - **Runtime**: Python 3
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `uvicorn main:app --host 0.0.0.0 --port $PORT`
   - **Root Directory**: `backend`
5. Scroll to **"Environment Variables"**, click "Add Variable":
   - Key: `ANTHROPIC_API_KEY`
   - Value: `your-api-key-here`
6. Click **"Create Web Service"**
7. Wait ~3 minutes. You'll get a URL like:
   `https://excелchat-ai.onrender.com`
8. **Copy this URL** — you need it for Step 3

---

## STEP 3 — Update Frontend with your Render URL

Open `frontend/index.html` and find this line (near the bottom in the script):

```javascript
const API_BASE = "http://localhost:8000";
```

Change it to your Render URL:

```javascript
const API_BASE = "https://excелchat-ai.onrender.com";
```

Save the file, then push to GitHub:

```cmd
git add .
git commit -m "Update API URL for production"
git push
```

---

## STEP 4 — Enable GitHub Pages (Frontend)

1. Go to your GitHub repo → **Settings** → **Pages** (left sidebar)
2. Under "Source", select **"Deploy from a branch"**
3. Branch: **main**, Folder: **/ (root)**  
   *(Note: index.html must be in the root of the repo, or use `/frontend` if supported)*
4. Click **Save**
5. After ~1 minute, your site is live at:
   `https://YOUR_USERNAME.github.io/ai-chatbot`

---

## ✅ Done! Your chatbot is now live

Share the GitHub Pages URL with anyone — they can use it from any device, anywhere!

---

## ⚠️ Important Notes

- **Render free tier sleeps** after 15 minutes of inactivity. First message after sleep takes ~30 seconds to wake up. This is normal on the free plan.
- **Excel file resets** on Render deploys (ephemeral storage). For permanent storage, consider upgrading to Render's paid plan or switching to a cloud database like Supabase (free).
- To **keep the bot awake**, you can use a free service like https://uptimerobot.com to ping your Render URL every 10 minutes.

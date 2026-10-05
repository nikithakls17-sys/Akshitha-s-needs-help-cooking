# Akshita's Kitchen

A friendly little web app that helps you cook nourishing food you actually love, built around your health conditions and whatever's already in your fridge.

## Who it's for

Akshita (and anyone like her) who manages health conditions such as **PCOS, thyroid, or insulin resistance** through food. She wants healthier, more nourishing versions of foods she enjoys, not diets or restriction. The app has **no calorie numbers anywhere**. It focuses on balance and adding good things, and keeps a warm, encouraging tone.

## What it does

| Tab | What it does |
|---|---|
| **Swap It** (the main feature, and the first screen) | Type any dish ("butter chicken with naan", "bubble tea") to get a lighter, more nourishing version: ingredient swaps (original → swap → why) and how to make it. |
| **My Fridge** | Add what you have as chips. "What can I make?" gives 3 recipes using mostly those items, marks what you're missing, and explains why each one is good for you. |
| **Day Plan** | One tap gives breakfast, lunch, snack and dinner for today, using your fridge items. |
| **Food Log** | Write what you ate in plain words. Each entry gets tagged for protein, fiber, veggies, whole grains and added sugar, and you can get a gentle summary of your day. |
| **My Profile** | Conditions, foods you love, foods you avoid or are allergic to, and diet style. Every AI request uses this. |

Everything is saved in your browser (localStorage). There's no backend and no account.

> Ideas only, not medical advice. Check with your doctor or dietitian for your condition.

## Run it

Just open `index.html` in Chrome, Edge, Firefox or Safari. There's no install and no build step.

### Option A: Gemma 4 via the Gemini API (free key)

1. Go to **https://aistudio.google.com** and sign in with a Google account.
2. Click **Get API key** → **Create API key**, then copy it. (Direct link: https://aistudio.google.com/apikey)
3. Open the app, click **Settings**, choose **Gemma (Gemini API)**, paste the key and Save.
4. The default model is `gemma-4-26b-a4b-it`. You can change it in Settings.

Your key is stored only in your own browser's localStorage, and the app sends it only to Google.

### Option B: Fully offline with Ollama

1. Install Ollama from **https://ollama.com**.
2. Download the model:
   ```
   ollama pull gemma3:4b
   ```
3. Make sure Ollama is running (the desktop app, or `ollama serve`).
4. In the app, open **Settings**, choose **Ollama (offline)** and Save. The defaults are `http://localhost:11434/api/chat` and `gemma3:4b`.

**If you see "Couldn't reach Ollama":** the browser may be blocking the request from a `file://` page. Quit Ollama, then start it with browser access allowed:

- Windows (PowerShell): `$env:OLLAMA_ORIGINS="*"; ollama serve`
- macOS / Linux: `OLLAMA_ORIGINS="*" ollama serve`

Another fix is to serve the folder locally, for example with `python -m http.server 8000`, and then open http://localhost:8000.

## Tech

One `index.html` file with inline CSS and JS. Fonts are Playfair Display and Poppins from Google Fonts; offline, it falls back to system serif and sans fonts. The model is asked to reply in JSON only. Responses are cleaned up (code fences stripped, then everything from the first `{` to the last `}`) and parsed, and if parsing fails you get a friendly error with a retry button.

# Probaho bot deployment pack

Files included:
- `probaho_bot_final.py` — sanitized version of your bot file
- `requirements.txt` — Python packages
- `.env.example` — environment variable template

## What I changed
- removed the hard-coded bot token from code and made `BOT_TOKEN` environment-first
- made `OWNER_ID`, `OWNER_CONTACT`, and `DB_PATH` environment-aware
- left the rest of your bot logic intact to avoid breaking the large single-file flow
- verified the patched file compiles with `python -m py_compile`

## Important security step
Your original uploaded file contains a live hard-coded Telegram bot token. Rotate that token in BotFather before deploying this pack.

## Minimum environment
Required:
- `BOT_TOKEN`
- `OWNER_ID`
- `GEMINI_API_KEY`

Recommended:
- `OWNER_CONTACT`
- `DB_PATH`
- `PORT`
- `PROBAHO_LOG_FILE`

Optional:
- GitHub backup variables if you want DB sync
- Gemini model override variables if you want custom model routing

## Install
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Run
```bash
export BOT_TOKEN="..."
export OWNER_ID="8535385246"
export GEMINI_API_KEY="..."
python probaho_bot_final.py
```

## Hosting notes
- Render / Railway / Oracle VM can run this file.
- For Render, keep `PORT=10000` unless your service needs another port.
- SQLite is local storage. If the instance filesystem is ephemeral, enable the GitHub backup variables or attach persistent storage.

## Reality check
This is a very large single-file bot with many historical patches and repeated function re-definitions. The last definitions win at runtime. The file is syntax-valid, and this pack fixes the highest-risk deployment issue first: exposed secrets and env setup. For a true long-term "error-less" production build, the next step would be splitting it into modules and adding tests.

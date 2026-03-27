Probaho OCR + PDF Quiz Patch

What changed
- Existing bot behavior stays the same.
- Added FREE OCR-first extraction from image and PDF in private chat.
- Image flow now tries local OCR first, then falls back to old Gemini image flow if GEMINI_API_KEY exists.
- PDF flow is new: send PDF while /vision_on is enabled, MCQs are extracted into buffer, then use /done.

How it works now
1) Start bot
2) In private chat, enable extraction with /vision_on
3) Send an image or PDF
4) Bot extracts MCQs into your buffer
5) Use /done to export CSV + JSON
6) All old commands continue as before

Environment variables
- BOT_TOKEN: required
- OWNER_ID: required
- OWNER_CONTACT: optional
- DB_PATH: optional
- PORT: optional
- GEMINI_API_KEY: optional, only for old Gemini fallback
- OCR_LANGS: default eng+ben
- OCR_PAGE_LIMIT: default 35
- OCR_MIN_QUESTION_LEN: default 8
- OCR_DEBUG: 0/1
- TESSERACT_CMD: optional absolute path to tesseract binary

Python packages
pip install -r requirements.txt

System packages you need on the server
Ubuntu/Debian:
  sudo apt update
  sudo apt install -y tesseract-ocr tesseract-ocr-ben tesseract-ocr-eng

Run
  export BOT_TOKEN="..."
  export OWNER_ID="..."
  python probaho_bot_ocr_pdf_ready.py

Important notes
- Your original file contains a hard-coded bot token. Rotate that token in BotFather before deployment.
- PDF extraction uses PyMuPDF text first, then OCR if needed.
- OCR quality depends on scan quality. Clean, high-contrast scans work best.
- For large PDFs, OCR_PAGE_LIMIT controls maximum pages processed.

Telegram usage
- /vision_on -> enable image/pdf extraction
- Send image or PDF in private chat
- /done -> export CSV + JSON
- /vision_off -> disable extraction

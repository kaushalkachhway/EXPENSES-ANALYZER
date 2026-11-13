# AI-Powered Bank Statement & Expense Analyzer

Turns messy bank statements (PDF, CSV, receipt photos) into clean, categorized transactions with anomaly flags.

**Status:** Milestone 1 (core parser) complete. See roadmap below.

## Features (Milestone 1)
- Parses CSV, text PDFs (pdfplumber) and scanned PDFs/images (Tesseract OCR fallback)
- Extracts date, description, amount, debit/credit
- Privacy-first redaction of account/card numbers, phones, emails, PAN
- Merchant normalization (`UPI-SWIGGY-982341` -> `Swiggy`) + rule-based categories
- Dedup hashing (date + amount + type + description)
- Detects recurring bills, price hikes, duplicate charges, large one-off purchases

## Quick start
```bash
pip install -r requirements.txt
python statement_parser.py samples/sample.csv
python statement_parser.py my_statement.pdf --json out.json
```
OCR needs the Tesseract binary (`sudo apt install tesseract-ocr` / `brew install tesseract`) and poppler for `pdf2image`.

## Roadmap
- [x] M1: Core parser
- [ ] M2: PostgreSQL schema + FastAPI upload/list routes
- [ ] M3: Hybrid categorizer (rules first, LLM for unknown merchants, JSON schema output)
- [ ] M4: Next.js + Tailwind + Recharts dashboard, manual category overrides
- [ ] Stretch: natural-language queries via read-only SQL

## Privacy
Redaction runs before any text could be sent to an external API. Do not commit real statements.

# 📧 Auto Mail from Google Sheet

> **n8n automation** — Reads buyer list from Google Sheet, generates personalized email using AI, sends via Gmail automatically. Zero manual work.

---

## What This Does

```
Google Sheet Row → AI writes personalized email → Gmail sends → Sheet updated with Sent status
```

---

## Features

- ✅ Reads each buyer row from Google Sheet
- ✅ AI generates unique personalized email per buyer
- ✅ Sends via your Gmail account
- ✅ Tracks: Sent / Failed / Bounced in Sheet
- ✅ Respects daily sending limits (50/day Gmail free)
- ✅ Adds delay between emails (avoid spam)
- ✅ Logs sent time, subject in Sheet

---

## Google Sheet Columns Required

```
A: Email_Status         (Pending / Sent / Failed)
B: Row_Number
C: Buyer_Name
D: Company_Name
E: Country
F: Email_Address
G: Product_Interest
H: Your_Product_Name
I: Email_Subject        (auto-filled after send)
J: Sent_At              (auto-filled after send)
K: Open_Tracked         (optional)
L: Notes
```

---

## Email Template (AI Generated)

Each email is unique — AI customizes based on:
- Buyer's company name
- Buyer's country
- Product interest
- Your company name & product

**Example Output:**
```
Subject: Export Inquiry — [Your Product] for [Company Name]

Dear [Buyer Name],

I came across [Company Name] and noticed your interest in [Product Category].
We specialize in exporting [Your Product] to [Country] and would love to...
```

---

## Setup

### Step 1 — Gmail Setup in n8n
1. n8n → Credentials → Add → Gmail OAuth2
2. Authorize with your Gmail

### Step 2 — Import Workflow
1. n8n → New Workflow → Import from file
2. Select `auto_mail_workflow.json`

### Step 3 — Replace Placeholders

| Placeholder | Replace With |
|------------|-------------|
| `YOUR_SHEET_ID` | Google Sheet ID |
| `YOUR_CLAUDE_KEY` | Claude or Groq API key |
| `YOUR_COMPANY_NAME` | Your export company name |
| `YOUR_PRODUCT` | Your main export product |
| `YOUR_FROM_NAME` | Your name |

### Step 4 — Set Send Limit
In the workflow, default is **20 emails/day** — change as needed.

---

## Sending Limits

| Method | Daily Limit | Cost |
|--------|------------|------|
| Gmail free | 500/day | Free |
| Gmail API | 1 billion/day | Free |
| SendGrid | 100/day | Free |

---

## Folder Structure

```
project2_auto_mail/
├── README.md
├── auto_mail_workflow.json
└── email_templates/
    └── export_outreach_template.txt
```

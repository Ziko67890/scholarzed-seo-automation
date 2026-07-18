# 🚀 ScholarZed AI SEO Content Automation

> **5 days to build. 15 minutes to run.**
> A fully automated SEO content pipeline that takes a keyword and publishes a complete, SEO-optimised article to WordPress — with zero manual work.

![n8n](https://img.shields.io/badge/Built%20with-n8n-orange?style=flat-square)
![GPT-4o](https://img.shields.io/badge/AI-GPT--4o-412991?style=flat-square)
![WordPress](https://img.shields.io/badge/CMS-WordPress-21759B?style=flat-square)
![Google Sheets](https://img.shields.io/badge/Tracking-Google%20Sheets-34A853?style=flat-square)
![Telegram](https://img.shields.io/badge/Notifications-Telegram-26A5E4?style=flat-square)

---

## 📌 What It Does

Type a keyword → get a fully published SEO article in 15 minutes.

The system handles everything automatically:

- 🔍 **Researches** top competitor pages for the keyword
- ✍️ **Writes** a long-form article in journalism style
- 🖼️ **Generates & uploads** 3 images from Unsplash to WordPress
- 📊 **Optimises** SEO title, meta description, slug and focus keyphrase
- 🏗️ **Builds** FAQ schema (JSON-LD structured data)
- ✅ **Quality checks** the article before publishing
- 🌐 **Publishes** the article live on WordPress
- 📋 **Logs** every job to Google Sheets with status, finish time and WordPress URL
- 📲 **Sends** a Telegram notification when the article is live
- 🚨 **Handles errors** — catches failures, logs them and sends an alert

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **n8n** | Workflow automation engine |
| **GPT-4o** | AI writing, research, QA, image prompts |
| **SerpAPI** | Google search results for competitor research |
| **Jina AI** | Web scraping competitor pages |
| **Unsplash API** | Fetching royalty-free images |
| **WordPress REST API** | Publishing articles and uploading media |
| **RankMath API** | Setting SEO meta on published posts |
| **Google Sheets** | Job tracking and status logging |
| **Telegram Bot API** | Success and error notifications |
| **Railway** | n8n deployment and hosting |
| **Netlify** | Hosting the keyword submission form |

---

## 🏗️ Architecture

```
[HTML Form / Webhook]
        ↓
MODULE 1 — TRIGGER
  Webhook → Extract Keywords → Loop → Log to Google Sheets
        ↓
MODULE 2 — RESEARCH
  SerpAPI → Extract URLs → Jina Scraper → Clean Content
  → Research Analyst Agent → Content Gap Analyzer
  → Fetch Existing Posts (internal linking)
        ↓
MODULE 3 — WRITING
  SEO Writer → Fact Checker → Human Rewriter
        ↓
MODULE 4 — SEO OPTIMIZATION
  SEO Optimizer → Schema Builder (FAQ JSON-LD)
        ↓
MODULE 5 — IMAGE GENERATION
  Image Prompt → Unsplash API → Download → WordPress Upload
  → Collect Media IDs (featured + 2 inpost images)
        ↓
MODULE 6 — QUALITY ASSURANCE
  QA Auditor → IF Node (pass/fail) → SEO Editor → Merge
        ↓
MODULE 7 — WORDPRESS PUBLISHING
  Prepare WP Data → Markdown to HTML → Create Post
  → Set RankMath Meta → Set Categories & Tags → Publish
        ↓
MODULE 8 — GOOGLE SHEET UPDATE
  Update Row → Status: Completed, Finish Time, WordPress URL
        ↓
MODULE 9 — TELEGRAM NOTIFICATION
  Send article title, keyword, link, images count, date
        ↓
[SEO - Error Handler Workflow]
  Error Trigger → Extract Error Info → Log to Sheet → Telegram Alert
```

---

## 📁 Repository Structure

```
scholarzed-seo-automation/
│
├── workflows/
│   ├── ai-seo-automation.json        # Main n8n workflow (9 modules)
│   └── seo-error-handler.json        # Error handling workflow
│
├── form/
│   └── scholarzed-seo-form.html      # Keyword submission form (hosted on Netlify)
│
├── screenshots/
│   ├── 01-form.png                   # Keyword input form
│   ├── 02-n8n-canvas.png             # Full workflow canvas
│   ├── 03-executions.png             # Execution history
│   ├── 04-google-sheet.png           # Job tracking sheet
│   ├── 05-telegram.png               # Telegram notifications
│   └── 06-wordpress-article.png      # Published article
│
└── README.md
```

---

## ⚙️ How to Set It Up

### Prerequisites
- n8n instance (self-hosted or Railway)
- WordPress site with REST API enabled
- RankMath SEO plugin installed on WordPress
- API keys for: OpenAI, SerpAPI, Jina AI, Unsplash, Telegram Bot

### Step 1 — Import Workflows
1. Open your n8n instance
2. Click **Import** → upload `ai-seo-automation.json`
3. Import `seo-error-handler.json` as a separate workflow
4. In main workflow Settings → set **Error Workflow** to `SEO - Error Handler`

### Step 2 — Configure Credentials
Add these credentials in n8n:
- `OpenAI API` — GPT-4o access
- `SerpAPI` — Google search results
- `WordPress API` — site URL + username + application password
- `Google Sheets OAuth2` — spreadsheet access
- `Telegram API` — bot token

### Step 3 — Set Up Google Sheet
Create a Google Sheet named **SEO Automation Jobs** with these columns:
```
Job ID | Keyword | Status | Start Time | Finish Time | WordPress URL | Processing Time | Error
```

### Step 4 — Configure the Form
1. Open `scholarzed-seo-form.html`
2. Replace `YOUR_WEBHOOK_URL_HERE` with your n8n webhook URL
3. Host on Netlify (drag and drop at netlify.com/drop)

### Step 5 — Activate
1. Set main workflow to **Active**
2. Set error handler workflow to **Active**
3. Open the form, type a keyword and click Generate

---

## 📊 Performance

| Metric | Value |
|---|---|
| Average processing time | 4–6 minutes per article |
| Images per article | 3 (featured + 2 inpost) |
| Average article length | 2,000–4,000 words |
| SEO elements set | Title, slug, meta, keyphrase, schema, categories, tags |

---

## 💰 Running Costs

| Service | Cost |
|---|---|
| SerpAPI | Free (250 searches/month) → $50/month for scale |
| OpenAI GPT-4o | ~$0.50–$2.00 per article |
| Unsplash API | Free |
| Jina AI | Free tier |
| n8n (Railway) | ~$5/month |
| Netlify (form) | Free |

---

## 🔮 Possible Extensions

- [ ] Scheduled batch runs (publish X articles per day automatically)
- [ ] Dashboard UI for monitoring all jobs
- [ ] Support for multiple WordPress sites
- [ ] WhatsApp notification support
- [ ] Automatic internal link injection based on existing posts

---

## 👨‍💻 Built By

**Isaac** — AI Automation Specialist & Full-Stack Developer

- 🌐 [Upwork Profile](https://www.upwork.com/freelancers/~01c9fa038a4a7a3f5a)
- 💼 Available for AI automation projects

---

## 📄 License

This project is for portfolio and demonstration purposes.
Feel free to fork and adapt for your own use case.

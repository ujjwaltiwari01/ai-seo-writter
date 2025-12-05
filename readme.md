
# 🚀 AI SEO Writer – Content Optimization Automation Template

> **Automate content updates, boost rankings, and stop doing repetitive SEO work manually.**  
> Built with 💚 using **n8n**, **LLMs**, **Google Sheets**, **BigQuery**, and **Google Drive**.

---

## ✨ Quick Pitch

Tired of manually:
- Checking Google Search Console for each URL? 😵‍💫  
- Copy-pasting data into messy spreadsheets? 😩  
- Rewriting content again and again for SEO? ⏳  

**This template turns all of that into an automated system** that:

✅ Finds keyword opportunities 🔍  
✅ Analyzes your content 🧠  
✅ Generates AI-powered rewrite suggestions ✍️  
✅ Logs performance over time in Google Sheets 📊  
✅ Creates a clean HTML report stored in Google Drive 📂  

Plug in a URL → Run the workflow → Get a **ready-to-use optimization report**. 😮‍💨

---

## 🧭 Table of Contents

1. [Overview](#-overview)
2. [Key Features](#-key-features)
3. [How the Workflow Works](#-how-the-workflow-works)
4. [System Architecture](#-system-architecture)
5. [Tech Stack](#-tech-stack)
6. [Prerequisites](#-prerequisites)
7. [Setup & Installation](#-setup--installation)
8. [Configuration](#-configuration)
9. [Using the Template Step-by-Step](#-using-the-template-step-by-step)
10. [Workflow Breakdown (Node by Node)](#-workflow-breakdown-node-by-node)
11. [Example Outputs](#-example-outputs)
12. [Customization Ideas](#-customization-ideas)
13. [Best Practices for SEO Workflows](#-best-practices-for-seo-workflows)
14. [Troubleshooting](#-troubleshooting)
15. [Roadmap](#-roadmap)
16. [Contributing](#-contributing)
17. [License](#-license)

---

## 🔍 Overview

This **AI-powered content optimization template** for **n8n** automates SEO improvements for blog posts and landing pages.

Instead of manually checking data and writing updates, this workflow:

- Reads **performance data** (e.g., from BigQuery / GSC exports) 📈  
- Analyzes your **article content** via crawling 🕷️  
- Uses an **LLM** (like OpenAI / Gemini) to generate **smart rewrite suggestions** 🤖  
- Logs everything inside **Google Sheets** for history tracking 📊  
- Generates a **beautiful HTML report** with suggestions and saves it to **Google Drive** 🗂️  

This is perfect for **bloggers, SEOs, agencies, and content teams** who want to scale content updates without sacrificing quality.

---

## 🧩 Key Features

| 💡 Feature | 🧠 What It Does | 📦 Output |
|-----------|-----------------|-----------|
| 🔑 Keyword Analysis | Uses SQL on BigQuery data (or any imported GSC dataset) to find valuable keywords | A tab in Google Sheets with target keywords & metrics |
| ✍️ AI Content Suggestions | Generates rewrite suggestions for titles, meta descriptions, and paragraphs | HTML report + structured content blocks |
| 📊 Historical Tracking | Creates/updates a Google Sheet per URL; new sheet tab per run | Full optimization history over time |
| 🕸 Content Crawling | Uses `crawl4ai` (or equivalent) to scrape and parse article content | Clean, structured content for LLM input |
| 📑 SEO Report Generation | Builds a detailed HTML report with sections, highlights, and recommended changes | Downloadable/previewable report in Google Drive |
| 🔗 URL-Based Organization | Names files/sheets using article slug + date | Easy mapping between URLs and their history |

---

## ⚙️ How the Workflow Works

At a high level, the workflow follows this loop:

1. **Input**: You submit an article URL (and optionally its slug/title).  
2. **Data Fetching**: The workflow queries your SEO performance data (e.g., clicks, impressions, positions).  
3. **Content Crawling**: The article is crawled and broken into structured sections (headings, paragraphs, etc.).  
4. **Analysis & Optimization**: The LLM combines SEO data + article content to generate actionable suggestions.  
5. **Reporting**: The workflow creates or updates a Google Sheet, logs the run, and builds an HTML optimization report.  
6. **Storage**: The HTML report is uploaded to Google Drive and linked to the sheet entry.  

Result: A **single place** to see **what to change, why to change it, and how it performed over time**. 🧠📊

---

## 🏗 System Architecture

```text
User Input (URL, Slug)
        ↓
   n8n Workflow
        ↓
┌─────────────────────────────┬─────────────────────────────┐
│   Data Layer                │   Content Layer             │
│  - BigQuery / GSC export   │  - crawl4ai / HTTP Request  │
│  - Sheets (logs / keywords)│  - Article HTML → text      │
└──────────────┬──────────────┴──────────────┬──────────────┘
               ↓                             ↓
          Analysis Engine (LLM)
               ↓
     AI-Powered Optimization Suggestions
               ↓
┌─────────────────────────────┬─────────────────────────────┐
│  Google Sheets (history)   │  Google Drive (HTML report) │
└─────────────────────────────┴─────────────────────────────┘
````

---

## 🧱 Tech Stack

| Layer        | Tool                               | Purpose                               |
| ------------ | ---------------------------------- | ------------------------------------- |
| Automation   | **n8n**                            | Orchestrates the entire workflow      |
| Data         | **BigQuery / GSC export**          | Stores performance & query data       |
| Storage      | **Google Sheets**                  | Holds history/logs + keyword insights |
| Reports      | **Google Drive**                   | Stores generated HTML reports         |
| Crawling     | **crawl4ai** (or any HTTP crawler) | Extracts article text & structure     |
| Intelligence | **OpenAI / Gemini / any LLM**      | Generates rewrite & SEO suggestions   |

> 🔁 You can swap individual parts (e.g., LLM provider, database, or storage) as needed.

---

## ✅ Prerequisites

Before you start, make sure you have:

* A running **n8n** instance (self-hosted or cloud) 🌐
* Access to **BigQuery** or any database/export that contains your SEO performance data 📊
* A **Google Cloud Project** with:

  * Google Sheets API enabled 🟩
  * Google Drive API enabled 📁
* **API credentials** for:

  * Google Sheets
  * Google Drive
  * Your LLM provider (OpenAI / Gemini / etc.)
* Basic familiarity with n8n credentials & node configuration 🔐

---

## 🛠 Setup & Installation

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/ujjwaltiwari01/ai-seo-writter.git
cd ai-seo-writter
```

### 2️⃣ Import Template into n8n

1. Open your **n8n dashboard**.
2. Click **Workflows → Import from file / clipboard**.
3. Paste the JSON or upload the exported template.
4. Save the workflow.

### 3️⃣ Configure Credentials in n8n

You'll typically need these credentials set up:

| Credential       | Used For                                     |
| ---------------- | -------------------------------------------- |
| Google Sheets    | Writing & reading keyword / performance data |
| Google Drive     | Uploading the HTML report                    |
| BigQuery (or DB) | Running SEO performance SQL queries          |
| OpenAI / Gemini  | Generating AI optimization suggestions       |

Set them up under **Settings → Credentials** in n8n, then map them inside the corresponding nodes.

---

## 🧩 Configuration

### 🔐 Environment Variables (Suggested)

You can manage these in your n8n environment or use direct credential config:

| Variable           | Description                                           |
| ------------------ | ----------------------------------------------------- |
| `LLM_API_KEY`      | API key for your LLM (OpenAI/Gemini/etc.)             |
| `GDRIVE_FOLDER_ID` | Google Drive folder where reports are stored          |
| `DEFAULT_SHEET_ID` | Optional: main Google Sheet ID for logging            |
| `PROJECT_DOMAIN`   | Domain used in analysis prompts (e.g., `example.com`) |

> 🔁 You can hardcode these values in the nodes if you prefer, but environment variables make it easier to move between environments.

---

## 🚀 Using the Template Step-by-Step

1. **Open the workflow in n8n**.
2. Locate the **start/form node** where the URL is passed.
3. Provide:

   * `article_url` – The full URL of the article.
   * `slug` – A unique slug or ID for that article.
4. Execute the workflow.
5. After it completes, check:

   * ✅ Google Sheets → New row/sheet with performance + keyword data.
   * ✅ Google Drive → New HTML report with rewrite suggestions.
   * ✅ Logs → Ensure nodes ran successfully.

You can now open the HTML report in the browser and apply the suggestions directly to your CMS. 🧑‍💻

---

## 🧱 Workflow Breakdown (Node by Node)

> Note: The exact node names may vary depending on your implementation, but the structure usually follows this logic.

### 🧩 1. Input / Trigger Node

* **Type**: Manual Trigger / Webhook / Form Input
* **Purpose**: Accepts `article_url`, `slug`, and optional metadata.

### 🧩 2. SEO Data Fetch (BigQuery / DB Node)

* Runs a SQL query similar to:

```sql
SELECT
  query,
  clicks,
  impressions,
  ctr,
  position
FROM `your_project.your_dataset.your_table`
WHERE page = @article_url
ORDER BY clicks DESC
LIMIT 100;
```

* Output is then cleaned and sent to Google Sheets + LLM.

### 🧩 3. Google Sheets Node (Write Keywords)

* **Action**: Append or update rows.
* **Purpose**: Keep a **log of keywords & performance** for that URL.

### 🧩 4. Crawler Node (crawl4ai / HTTP)

* Fetches the HTML content for `article_url`.
* Extracts:

  * Title
  * Headings (H1, H2, H3…)
  * Paragraphs
  * Word count
  * Links

### 🧩 5. LLM Node (AI Suggestions)

* Combines:

  * SEO performance data 🔢
  * Extracted content 📝

* Asks the model for:

  * Better **title suggestions**
  * Improved **meta description**
  * **Rewrite suggestions** for paragraphs
  * **Keyword placement ideas**

Example prompt fragment:

```text
You are an expert SEO content strategist.
Given this article content and performance data, suggest:
1. An improved SEO title.
2. A high-CTR meta description.
3. Content rewrite suggestions for key sections.
4. A list of primary & secondary keywords to include.
```

### 🧩 6. HTML Report Builder (Code / Template Node)

* Formats AI output into a **structured HTML file** with:

  * ✅ Title suggestions
  * ✅ Meta descriptions
  * ✅ Before/After rewrite blocks
  * ✅ Keyword tables
  * ✅ Action checklist

### 🧩 7. Google Drive Node (Upload Report)

* Uploads the generated HTML file to a target folder.
* Returns a shareable link (if configured) that you can log in Sheets.

### 🧩 8. Google Sheets Node (Log Run)

* Adds an entry with:

  * `slug`
  * `article_url`
  * Run date/time
  * SEO snapshot
  * Drive report link

This gives you a **time-series history per article**.

---

## 📸 Screenshot

![n8n-ai-seo-writer](./n8n-automation-ai-seo-writer-with-gsc-data.png)

> The screenshot above shows a visual overview of the n8n workflow (nodes, data flow, and integrations).

---

## 🧾 Example Outputs

### 🏷 Title Suggestions (Example)

```text
Original: Blogging Tips for Beginners
Improved: Blogging Tips for Beginners: 15 SEO Strategies to Grow Traffic Fast
```

### 🪄 Meta Description (Example)

```text
Boost your blog traffic with these beginner-friendly SEO blogging tips. Learn how to optimize your posts, find high-intent keywords, and rank higher on Google.
```

### ✍️ Content Rewrite (Before / After)

| Type         | Text                                                                                                                                                       |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🟥 Original  | "This article will tell you some ways to write better blogs."                                                                                              |
| 🟩 Optimized | "In this guide, you'll learn practical, SEO-backed techniques to write blog posts that attract more readers, improve rankings, and keep visitors engaged." |

---

## 🎨 Customization Ideas

Want to level this up even more? Here are ideas:

* 🔁 **Auto-schedule runs** for your top 100 URLs weekly or monthly.
* 🔔 Send **Slack / email notifications** when a new report is generated.
* 🧪 Run **A/B content variants** and track performance by variant tag.
* 🌍 Localize content for different regions using the same workflow.
* 🧵 Integrate directly with your CMS (WordPress / Webflow / etc.) via API.

---

## 📚 Best Practices for SEO Workflows

* Start with your **top traffic pages** first.
* Don’t rewrite everything at once – **focus on intent gaps** and **missing queries**.
* Track performance **2–4 weeks after updates** before making another big change.
* Save all reports – they help explain decisions to clients & teams.

---

## 🛠 Troubleshooting

| Issue               | Possible Cause                     | Fix                                             |
| ------------------- | ---------------------------------- | ----------------------------------------------- |
| No data from SQL    | URL mismatch or filters too strict | Check exact URL in your BigQuery / data source  |
| Sheet not updating  | Wrong Sheet ID or tab name         | Verify IDs & ranges in Google Sheets node       |
| Report not in Drive | Wrong folder ID / permissions      | Confirm `GDRIVE_FOLDER_ID` and sharing settings |
| LLM errors          | Invalid API key or model name      | Check credentials and model configuration       |

> Check the **n8n execution logs** – they are your best friend when debugging. 🐛

---

## 🗺 Roadmap

Planned improvements:

* [ ] Multi-language optimization support 🌍
* [ ] Direct CMS integrations (WordPress, Webflow, Ghost) 🔌
* [ ] Support for custom metrics (engagement time, conversions) 📈
* [ ] Pre-built prompt library for different content types 📚

---

## 🤝 Contributing

Contributions, ideas, and improvements are **very welcome**! 🙌

You can:

* Open an **issue** for bugs or feature requests 🐞
* Submit a **pull request** with improvements 🔧
* Share how you’re using this in your own SEO stack 💬

Please follow standard GitHub flow:

1. Fork the repo
2. Create a feature branch
3. Commit changes with clear messages
4. Open a PR 🎉

---

## 📄 License

This project is licensed under the **MIT License**.
You’re free to use, modify, and integrate it into your own workflows.

---

> Built to help you **work smarter**, not harder – and make SEO feel a little more fun. 😄

🚀 Happy automating & happy ranking!

```
```


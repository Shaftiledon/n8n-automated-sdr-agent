# n8n-automated-sdr-agent

# 🤖 Autonomous AI SDR Agent (n8n + GPT-4o + Slack)

![n8n](https://img.shields.io/badge/Orchestration-n8n-orange?style=flat&logo=n8n)
![OpenAI](https://img.shields.io/badge/AI-GPT--4o-green?style=flat&logo=openai)
![Slack](https://img.shields.io/badge/Interface-Slack_Block_Kit-blue?style=flat&logo=slack)
![Status](https://img.shields.io/badge/Status-Active-success)

## 📋 Overview

This project is an **autonomous sales research and outreach agent** built with **n8n**. It automates the most time-consuming parts of the sales cycle: researching leads, finding relevant news hooks, and drafting hyper-personalized emails.

Unlike standard "auto-generated" spam, this agent includes a **Human-in-the-Loop (HITL)** approval system. It performs deep research and presents a draft to the user via a **Slack Dashboard**. The user can "Approve" or "Reject" the draft with a single click, triggering the final sync to the CRM.

**[🎥 Watch the 2-Minute Demo Here](INSERT_YOUR_LOOM_LINK_HERE)**

---

## ⚡ Key Features

* **Live Web Scraping:** Extracts clean text from prospect websites using HTML-to-Markdown conversion.
* **Real-Time News Enrichment:** Queries Google News (via SerpApi) to find recent events for relevant email "hooks."
* **Context-Aware Copywriting:** Uses GPT-4o to synthesize website data + news data into a unique email.
* **Slack "Mission Control":** Sends interactive cards to Slack with **Approve/Reject** buttons.
* **CRM Sync:** Automatically updates lead status and drafts in **Airtable** based on human feedback.

---

## 🛠 Tech Stack & Integrations

| Component | Tool/Service | Purpose |
| :--- | :--- | :--- |
| **Orchestration** | [n8n](https://n8n.io/) | Workflow automation and logic handling. |
| **LLM** | OpenAI (GPT-4o) | Analyzing company data and writing copy. |
| **Search** | SerpApi | Real-time Google News lookup. |
| **Database** | Airtable | Storing leads, status, and drafts. |
| **Interface** | Slack API | Notification and interactive approval buttons. |

---

## 🔄 Workflow Architecture

1.  **Trigger:** Watches Airtable for new records (Status: "New").
2.  **Scrape:** HTTP Request fetches website HTML → Converted to Markdown.
3.  **Enrich:** HTTP Request to SerpApi searches `"{Company Name} latest news"`.
4.  **Analyze & Draft:**
    * *Node 1:* Summarizes company mission & ICP.
    * *Node 2:* Writes email connecting Value Prop to News Item.
5.  **Human Review:** Sends a **Block Kit** message to Slack.
    * *Wait for Response:* Workflow pauses until a button is clicked.
6.  **Action:**
    * **If Approved:** Updates Airtable status to "Approved" & saves draft.
    * **If Rejected:** Updates Airtable status to "Rejected".

---

## 🚀 How to Run

### Prerequisites
* An instance of [n8n](https://n8n.io/) (Cloud or Self-Hosted).
* API Keys for: OpenAI, SerpApi, Airtable.
* A Slack App with `chat:write` permissions.

### Installation Steps

1.  **Clone the Repo:**
    ```bash
    git clone [https://github.com/yourusername/ai-sdr-agent.git](https://github.com/yourusername/ai-sdr-agent.git)
    ```
2.  **Import Workflow:**
    * Open n8n.
    * Go to **Workflows** > **Import from File**.
    * Select `workflow.json` from this repository.
3.  **Configure Credentials:**
    * Update the specific nodes (OpenAI, Slack, Airtable) with your own credentials in n8n.
4.  **Setup Slack App:**
    * Create an app at [api.slack.com](https://api.slack.com/apps).
    * Enable **Interactivity** to handle button clicks.
    * Copy the **Bot User OAuth Token** into n8n.
5.  **Activate:**
    * Toggle the workflow to **Active**.

---

## 📸 Screenshots

### 1. The Workflow Logic
*(Add a screenshot of your n8n graph here)*

### 2. The Slack Approval Dashboard
*(Add a screenshot of the Slack card with buttons here)*

---

## 💡 Future Improvements
* **Gmail Integration:** Automatically send the email upon "Approve" click.
* **Multi-Modal Analysis:** Use Vision API to analyze the prospect's landing page design.
* **LinkedIn Scraper:** Integrate Apollo or Proxycurl for individual person data.

---

## 📄 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

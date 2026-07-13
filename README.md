#  EthioTender Automation Engine (n8n)

A fully automated, backend-only workflow built in **n8n** that aggregates, processes, and distributes Ethiopian tender opportunities. It eliminates the need for a frontend by delivering structured, AI-analyzed tender data directly to users via Telegram and Email.

## The Problem
Tender opportunities in Ethiopia are scattered across various websites, PDFs, and newspapers. Businesses waste hours manually checking these sources. Building a full-stack app is often overkill when the core value is simply getting the right information to the right person at the right time.

##  The Solution
Instead of a heavy web application, this project is a **lean, serverless automation engine**. 
- It automatically scrapes/fetches tender data from target sources.
- It uses AI to extract key details (Deadline, Budget, Category, Location).
- It filters the tenders based on user preferences.
- It instantly pushes highly relevant opportunities directly to the user's Telegram or Email.
- 
##  Demo & Live Links
- **🎬 Video Walkthrough:** https://drive.google.com/file/d/1IaaRid4B_e1ei3AEU9gN33tAuxE1jvP7/view?usp=drive_link

##  Workflow Architecture (The Steps)

This n8n workflow is composed of the following logical steps:

1. **Trigger / Ingestion:** 
   - Uses a **Schedule Trigger** (or Webhook) to run daily/hourly.
   - Uses **HTTP Request** nodes to fetch data from target Ethiopian tender portals or RSS feeds.
2. **Data Parsing & Normalization:**
   - Uses a **Code Node** (JavaScript) to parse HTML/JSON responses and extract raw text.
3. **AI Enrichment (The Brain):**
   - Passes the raw text to the **Groq API (Llama 3)** via the AI node.
   - The AI extracts structured JSON: `Title`, `Category`, `Deadline`, `Location`, and a `Short Summary`.
4. **Filtering & Matching:**
   - Uses an **IF Node** to check if the tender matches specific criteria (e.g., Category == "Construction" AND Location == "Addis Ababa").
5. **Notification & Delivery:**
   - If matched, it routes to a **Telegram Node** (or Email node) to send a beautifully formatted alert to the user.
   - If not matched, the workflow ends gracefully.

##  Tech Stack & Integrations

- **n8n:** The core orchestration engine handling logic, state, and routing.
- **Groq API (Llama 3):** Fast, cost-effective AI inference for text extraction and summarization.
- **Telegram Bot API:** The primary delivery mechanism for low-bandwidth, instant notifications.
- **JavaScript (Code Nodes):** Used for custom data manipulation, array mapping, and error handling.

##  How to Use This Workflow

### Prerequisites
- An active n8n instance (Self-hosted via Docker, Desktop, or n8n Cloud).
- A Groq API Key (Free tier available).
- A Telegram Bot Token (from @BotFather) and your Chat ID.

### Import & Run
1. **Download the Workflow:**
   Clone this repository and locate the `ethio-tender-workflow.json` file.
2. **Import to n8n:**
   - Open your n8n dashboard.
   - Click the three dots (menu) in the top right corner → **Import from File**.
   - Select `ethio-tender-workflow.json`.
3. **Configure Credentials:**
   - Open the **Groq/AI Node** and add your Groq API key.
   - Open the **Telegram Node** and add your Bot Token and Chat ID.
   - Update the **HTTP Request Node** URLs to your target tender sources.
4. **Activate:**
   - Toggle the workflow to **Active** in the top right corner.
   - The Schedule Trigger will now run automatically!



# Bug Bounty Duplicate Detection System

**Automated AI-Powered Bug Triage & Duplicate Detection for Discord**

This n8n workflow automates the intake, analysis, and deduplication of bug reports submitted via Discord. It uses Retrieval-Augmented Generation (RAG) to analyze, classify, and detect duplicate bug reports, ensuring efficient triage and reducing manual effort.

---

## 📌 Table of Contents
- [Features](#-features)
- [Workflow Overview](#-workflow-overview)
- [Deployment Scenarios](#-deployment-scenarios)
  - [Small Scale](#small-scale)
  - [Large Scale](#large-scale)
- [Setup Instructions](#-setup-instructions)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Monitoring & Maintenance](#-monitoring--maintenance)
- [Troubleshooting](#-troubleshooting)
- [Security](#-security)
- [Feedback & Improvements](#-feedback--improvements)
- [License](#-license)

---

## 🌟 Features
- **Automated Bug Intake:** Pulls bug reports from Discord in real-time.
- **AI-Powered Analysis:** Uses RAG to extract structured information (title, description, severity, affected components, etc.).
- **Duplicate Detection:** Semantic search to identify and flag duplicate bug reports.
- **Automated Responses:** Replies to users with confirmation or duplicate notifications.
- **Thread Management:** Creates and closes Discord threads as needed.
- **Data Persistence:** Stores bug reports in MongoDB and Google Sheets.
- **Error Handling:** Logs errors and alerts admins via Discord webhook.
- **Scalability:** Adaptable for both small teams and large-scale programs.

---

## 🔄 Workflow Overview
1. **Trigger:** New message in Discord channel.
2. **Filter:** Only process messages containing bug-related keywords.
3. **Sanitize & Extract:** Clean and structure bug report data.
4. **AI Analysis:** Use RAG to extract structured bug information.
5. **Duplicate Check:** Search vector store for similar bug reports.
6. **Route:** Handle duplicates or new bugs accordingly.
7. **Respond:** Post confirmation or duplicate notification in Discord.
8. **Store:** Save bug data to MongoDB, vector store, and Google Sheets.
9. **Error Handling:** Log errors and alert admins.

---

## 📦 Deployment Scenarios

### Small Scale
**Use Case:** Small teams, limited bug report volume, simple infrastructure.
**Key Features:**
- In-memory vector store.
- Lightweight embedding model (e.g., `all-MiniLM-L6-v2`).
- Single n8n instance.
- Basic logging and error handling.

**Setup:**
- Deploy on a single VM or n8n cloud instance.
- Use the default in-memory vector store.
- Monitor via Google Sheets and Discord alerts.

### Large Scale
**Use Case:** Large teams, high bug report volume, need for scalability and reliability.
**Key Features:**
- Persistent vector database (e.g., Weaviate, Pinecone).
- High-performance embedding model (e.g., `text-embedding-3-large`).
- Distributed workload with task queues (e.g., RabbitMQ, Kafka).
- Comprehensive monitoring (e.g., Prometheus, Grafana).
- Robust error handling and retries.

**Setup:**
- Deploy on a cluster or cloud with multiple n8n workers.
- Replace in-memory vector store with a dedicated vector database.
- Implement batch processing and caching.
- Set up monitoring and alerting.

---

## 🛠 Setup Instructions

### Prerequisites
- n8n instance (self-hosted or cloud).
- Discord bot with appropriate permissions.
- MongoDB instance.
- Google Sheets API access.
- (Optional) Vector database (Weaviate, Pinecone, etc.) for large scale.

### Installation
1. **Import Workflow:**
   - Import the provided JSON workflow into your n8n instance.

2. **Configure Credentials:**
   - Set up Discord API credentials.
   - Configure MongoDB connection.
   - Set up Google Sheets API credentials.
   - (Optional) Configure vector database credentials.

3. **Set Environment Variables:**
   ```
   DISCORD_GUILD_ID=your_guild_id
   DISCORD_CHANNEL_ID=your_channel_id
   DISCORD_ERROR_WEBHOOK_URL=your_webhook_url
   GOOGLE_SHEET_ID=your_sheet_id
   GOOGLE_SHEET_NAME=Bug Reports
   ```

4. **Activate Workflow:**
   - Enable the workflow in n8n.

---

## ⚙ Configuration

### Discord
- Ensure your bot has permissions to read messages, create threads, and send messages in the target channel.

### MongoDB
- Create a collection named `bug_reports`.

### Google Sheets
- Create a sheet named `Bug Reports` with the required columns (see workflow nodes for schema).

### Vector Store (Large Scale)
- Set up your chosen vector database and update the workflow nodes to use it.

### Thresholds
- Adjust the `SIMILARITY_THRESHOLD` in the "Check Duplicate Threshold" node as needed (default: 0.82).

---

## 🚀 Usage
- Users submit bug reports in the configured Discord channel.
- The bot automatically processes, analyzes, and responds to each report.
- Admins can monitor the Google Sheet for all bug reports and duplicates.

---

## 📊 Monitoring & Maintenance
- **Small Scale:** Monitor via Google Sheets and Discord alerts.
- **Large Scale:** Set up dashboards (Grafana, Datadog) for workflow metrics and error rates.
- **Regularly Review:**
  - False positives/negatives in duplicate detection.
  - Update the embedding model or thresholds as needed.

---

## ❓ Troubleshooting
- **Discord API Errors:** Check bot permissions and rate limits.
- **MongoDB/Google Sheets Issues:** Verify credentials and connection.
- **Duplicate Detection Issues:** Adjust the similarity threshold or embedding model.
- **General Errors:** Check n8n execution logs and the error logging sheet.

---

## 🔒 Security
- Store all credentials in environment variables or a secrets manager.
- Restrict access to the n8n instance and databases.
- Regularly audit permissions and access logs.

---

## 💬 Feedback & Improvements
- **User Feedback:** Encourage users to flag false positives/negatives.
- **Continuous Improvement:** Use feedback to refine the duplicate detection logic and AI prompts.

---

## 📄 License
This project is licensed under the [APACHE 2.0](LICENSE).
```

---

## **How to Use This README**
- **For Developers:** Follow the setup and configuration sections to deploy and customize the workflow.
- **For Admins:** Use the usage and monitoring sections to understand how to operate and maintain the system.
- **For Stakeholders:** The features and overview sections provide a high-level understanding of the system’s capabilities.

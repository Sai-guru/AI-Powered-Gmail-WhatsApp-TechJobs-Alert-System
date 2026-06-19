# 🚀 AI-Powered Gmail → WhatsApp Tech Job Alert System

An intelligent automation workflow that monitors unread Gmail messages, filters relevant recruiter emails using Llama 3.3 70B via Groq, and instantly delivers priority notifications to WhatsApp.

Built with **n8n**, **Groq**, **PostgreSQL**, **Evolution API**, and **Docker**.

---

# 🎥 Demo

<video src="assets/Kooha-2026-06-19-21-54-28.mp4" controls width="100%"></video>

> 📌 Replace `assets/demo.mp4` with your video file path once uploaded to the repo (commit it under an `assets/` folder so the relative path resolves).

---

## ✨ Features

* 📧 Monitors unread Gmail messages every minute
* 🧠 AI-powered email classification using Llama 3.3 70B
* 🎯 Filters only genuine tech opportunities
* 🗄️ Persistent memory using PostgreSQL
* 📲 Real-time WhatsApp notifications
* 🐳 Fully self-hosted infrastructure with Docker
* ⚡ Lightweight and extensible workflow

---

# 🏗 Architecture

```text
Gmail Trigger
      │
      ▼
Groq Llama 3.3 70B
      │
      ▼
AI Agent
      │
      ▼
IF Filter
      │
      ▼
Evolution API
      │
      ▼
WhatsApp
```

### Stack

| Component            | Technology           |
| --------------------- | --------------------- |
| Workflow Engine       | n8n                   |
| LLM                   | Groq + Llama 3.3 70B  |
| Memory                | PostgreSQL            |
| Messaging Gateway     | Evolution API         |
| Notification Channel  | WhatsApp              |
| Deployment            | Docker                |

---

# ⚙️ Setup

## 1. Start the Infrastructure

```bash
docker compose up -d
```

Verify:

```bash
docker ps
```

You should see:

```text
postgres
n8n
evolution-api-service
```

---

## 2. Create a WhatsApp Instance

```bash
curl -X POST \
"http://localhost:8080/instance/create" \
-H "apikey: your-global-api-key" \
-H "Content-Type: application/json" \
-d '{
  "instanceName":"my_priority_alerts",
  "qrcode":true
}'
```

---

## 3. Open Evolution Manager

```
http://localhost:8080/manager
```

Scan the QR code using WhatsApp.

---

## 4. Open n8n

```
http://localhost:5678
```

Import:

```
workflow.json
```

---

# 🔐 Configure Credentials

### Gmail Trigger

Connect your Gmail account using OAuth2.

### Groq Chat Model

Create a Groq API key and configure the credential.

### PostgreSQL Memory

```text
Host: postgres
Port: 5432
Database: n8n_memory
SSL: Off
```

---

# 🧠 AI Logic

The AI Agent analyzes incoming email snippets and returns:

```text
true
```

if the email contains recruiter communication or professional greetings addressed to Sai.

Otherwise:

```text
false
```

Only emails classified as `true` proceed to the notification stage.

---

# 📲 Evolution API HTTP Request Node

## URL

```text
http://evolution-api-service:8080/message/sendText/my_priority_alerts
```

## Headers

```text
apikey: <INSTANCE_API_KEY>
Content-Type: application/json
```

## JSON Body

```json
{
  "number": "<91-yournumber->@s.whatsapp.net",
  "textMessage": {
    "text": "🚨 NEW PRIORITY TECH JOB ALERT 🚨\n\nFrom: {{$('Gmail Trigger').item.json.From}}\nSubject: {{$('Gmail Trigger').item.json.Subject}}\n\n{{$('Gmail Trigger').item.json.snippet}}"
  }
}
```

---

# 📲 WhatsApp Alert Example

```
🚨 NEW PRIORITY TECH JOB ALERT 🚨

From: recruiter@company.com

Subject: Full Stack Engineer Opportunity

Hi Sai,

We were impressed with your profile and would like to discuss an open role...
```

---

# 🧪 Test

Send yourself an email(demo) :

### Subject

```
 Full Stack Engineer Opportunity
```

### Body

```
Hi Sai,

We were impressed with your profile and would like to discuss an open role...
```

The workflow will:

1. Detect the email.
2. Analyze it with Llama 3.3 70B.
3. Filter irrelevant emails.
4. Send a WhatsApp alert instantly.

---

# 🚀 Future Improvements

* AI-generated summaries
* Priority scoring
* Resume attachment analysis
* Telegram integration
* Slack notifications
* Multi-channel alerts
* RAG-powered memory
* Automatic recruiter reply generation

---

# 🛠 Tech Stack

* n8n
* Groq
* Llama 3.3 70B
* PostgreSQL
* Evolution API
* Docker
* Gmail API
* WhatsApp

---

## 👨‍💻 Author

[**Prigeesh**](https://github.com/Sai-guru)

Arch Linux • Groq • n8n • Docker • LLMs • PostgreSQL • Open Source
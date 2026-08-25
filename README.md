# AI Lead Qualification & Scoring Engine 🎯

> An AI-powered lead qualification and routing workflow that analyzes inbound project inquiries, assigns a lead score, classifies prospects as **Hot / Warm / Cold**, stores the result, and triggers the appropriate follow-up automatically.

[![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-orange?logo=n8n)](https://n8n.io/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--5--mini-black?logo=openai)](https://openai.com/)
[![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Data%20Storage-34A853?logo=googlesheets)](https://www.google.com/sheets/about/)
[![Gmail](https://img.shields.io/badge/Gmail-Automated%20Follow--up-EA4335?logo=gmail)](https://www.gmail.com/)

## 🎯 Problem It Solves

Businesses often receive many project inquiries but do not have a consistent way to identify which prospects deserve immediate attention. Manually reviewing every form submission, estimating buying intent, checking budget and timeline, assigning a lead category, updating a spreadsheet, and sending follow-up emails is slow and difficult to scale.

This project automates that process. A prospect submits a structured project-intake form with information such as company size, estimated budget, desired start date, required service, project description, and website. The workflow sends the lead data to an AI Agent, which returns a structured **score, category, and reason**. The result is then routed into Hot, Warm, or Cold paths for the appropriate follow-up. fileciteturn24file1L81-L123 fileciteturn24file4L461-L476

### In one sentence

**It turns raw inbound inquiries into prioritized, actionable sales leads without requiring a team member to manually qualify every submission.**

---

## 🌍 Real-World Use Cases

This workflow can be used by:

- **AI automation agencies** — prioritize companies requesting AI automation services.
- **Software agencies** — identify high-value web/app development prospects.
- **Consulting firms** — score prospects based on budget, urgency, company size, and requirements.
- **B2B service businesses** — automatically route high-intent inquiries to sales representatives.
- **Freelancers and small teams** — reduce time spent manually reviewing contact forms.
- **Sales teams** — create a consistent first-pass qualification process before human follow-up.

For a sales team, a Hot lead can trigger an immediate internal notification containing the AI score, category, reason, budget, timeline, service requested, and a recommended next action. fileciteturn24file0L33-L46

---

## 🔄 Workflow Architecture

```text
Prospect submits project form
            │
            ▼
     n8n Form Trigger
            │
            ▼
          Wait
            │
            ▼
        AI Agent
            │
      ┌─────┴─────┐
      │ OpenAI     │
      │ GPT-5-mini │
      └─────┬─────┘
            │
            ▼
 Structured Output Parser
            │
            ▼
         All Data
            │
            ▼
      Hot / Warm / Cold
       ┌────┼────┐
       ▼    ▼    ▼
     Hot  Warm  Cold
       │    │    │
       └────┼────┘
            ▼
      Google Sheets
      + Gmail follow-up
```

The supplied workflow connects the form trigger to an AI Agent, then to structured output, a routing switch, Google Sheets storage, and separate email paths for Hot, Warm, and Cold leads. fileciteturn23file2L174-L317

---

## 🧠 How the AI Qualification Works

The AI Agent receives key lead information including:

- Full name
- Company name
- Estimated budget
- Project timeline
- Requested service
- Project requirements

It is instructed to return structured JSON containing:

```json
{
  "score": 85,
  "category": "Hot",
  "reason": "High budget and urgent project"
}
```

The workflow uses a Structured Output Parser so downstream n8n nodes receive predictable fields instead of free-form AI text. fileciteturn24file4L461-L503

### Lead categories

| Category | Meaning | Typical action |
|---|---|---|
| 🔥 **Hot** | High-value / high-intent opportunity | Immediate sales follow-up |
| 🟡 **Warm** | Promising opportunity that needs review | Sales review and follow-up |
| ⚪ **Cold** | Low-priority or weak-fit opportunity | Automated acknowledgement / nurture |

The routing switch explicitly checks the AI-generated category and sends the lead down the corresponding Hot, Warm, or Cold path. fileciteturn24file5L601-L687

---

## 📋 Lead Intake Form

The n8n form collects business and project context before qualification, including company size, budget range, desired start date, service type, project description, company website, and consent to be contacted. fileciteturn24file1L85-L210

---

## 📧 Automated Follow-up

### 🔥 Hot Lead

A high-priority lead receives a personalized email, while the internal team receives an alert containing the lead details, AI score, category, reason, and recommended action such as contacting the lead within 24 hours and scheduling a discovery call. fileciteturn24file2L293-L302 fileciteturn24file0L33-L46

### 🟡 Warm Lead

Warm leads receive an acknowledgement and an internal review notification containing the lead's basic information and AI score/category. fileciteturn24file3L337-L367

### ⚪ Cold Lead

Cold leads receive a polite acknowledgement explaining that the request may not currently be the best fit, while the information can be retained for future opportunities. fileciteturn24file2L266-L290

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| **n8n** | Workflow orchestration |
| **OpenAI GPT-5-mini** | AI lead analysis and scoring |
| **Structured Output Parser** | Reliable machine-readable AI output |
| **Google Sheets** | Lead result storage |
| **Gmail** | Automated prospect and internal-team notifications |
| **n8n Form Trigger** | Lead intake |

The workflow configuration identifies `gpt-5-mini` as the OpenAI chat model and includes a Google Sheets node for storing qualification results. fileciteturn24file4L493-L514 fileciteturn24file8L997-L1010

---

## 📸 Project Screenshots

### 1. End-to-end n8n workflow + generated email

![Workflow and email result](screenshots/01-workflow-and-email.png)

### 2. Hot-lead notification

![Hot lead email](screenshots/02-hot-lead-email.png)

### 3. Google Sheets qualification results

![Google Sheets results](screenshots/03-google-sheets-results.png)

---

## 📁 Repository Structure

```text
AI-Lead-Qualification-Scoring-Engine/
├── README.md
├── n8n-workflow.json
├── screenshots/
│   ├── 01-workflow-and-email.png
│   ├── 02-hot-lead-email.png
│   └── 03-google-sheets-results.png
└── .gitignore
```

---

## 📦 Import the Workflow

1. Open **n8n**.
2. Create a new workflow.
3. Choose **Import from File**.
4. Select `n8n-workflow.json`.
5. Reconnect your own OpenAI, Google Sheets, and Gmail credentials.
6. Replace placeholder values with your own configuration.
7. Test with a sample lead before enabling production automation.

> The JSON in this repository is sanitized for public sharing. Credentials, credential IDs, personal email addresses, and instance-specific metadata have been replaced with placeholders.

---

## 🔐 Security

Never commit API keys, OAuth tokens, private credentials, webhook secrets, or personal production data to a public repository. Use n8n's credential manager or environment variables and replace sensitive values with placeholders before publishing workflow JSON.

---

## 🚀 Future Improvements

- Add CRM integration (HubSpot / Salesforce / Pipedrive)
- Add lead deduplication
- Add automated follow-up sequences for Warm and Cold leads
- Add lead-source attribution
- Add analytics dashboard for conversion by lead category
- Add human approval before high-value outreach
- Add retry and error-handling branches
- Add configurable scoring rules and thresholds
- Add automated tests for qualification edge cases

---

## 👨‍💻 Author

**Angkon Biswas**  
AI Automation Engineer | AI Agents | Workflow Automation

- GitHub: https://github.com/angkonbiswas

---

> **From inbound inquiry → AI qualification → prioritized sales action.** 🚀

# AI Lead Qualification & Scoring Engine 🎯

> An AI-powered lead qualification and routing workflow built with n8n, OpenAI, Google Sheets, and Gmail. It turns inbound project inquiries into prioritized **Hot / Warm / Cold** leads and automatically triggers the next action.

[![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-orange?logo=n8n)](https://n8n.io/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--5--mini-black?logo=openai)](https://openai.com/)
[![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Data%20Storage-34A853?logo=googlesheets)](https://www.google.com/sheets/about/)
[![Gmail](https://img.shields.io/badge/Gmail-Automated%20Follow--up-EA4335?logo=gmail)](https://www.gmail.com/)

## 🚀 Overview

Sales and service teams often receive many inbound inquiries but cannot manually review every lead with the same level of attention. This project automates the first qualification layer.

A prospect submits a structured project-intake form. The workflow sends the relevant business and project information to an AI Agent. The AI returns a structured **score, category, and reason**, after which n8n routes the lead to the appropriate path, stores the result in Google Sheets, sends a prospect-facing email, and can notify the internal team for follow-up.

### In one sentence

**It turns raw inbound inquiries into prioritized, actionable sales opportunities without requiring a team member to manually qualify every submission.**

---

## 🎯 The Real-World Problem It Solves

Without an automated qualification layer, teams may have to:

- Read every inquiry manually.
- Compare budget, company size, timeline, and project requirements.
- Decide which leads deserve immediate attention.
- Copy lead data into a spreadsheet or CRM.
- Write and send different follow-up messages.
- Notify the right salesperson or project specialist.
- Repeat the same process for every new inquiry.

This creates **slow response times, inconsistent qualification, repetitive work, and missed high-intent opportunities**.

This workflow addresses that operational bottleneck by creating a repeatable AI-assisted qualification and routing process.

---

## 🌍 Real-World Applications

This architecture is useful for many service-based businesses:

| Business | How it can be used |
|---|---|
| **AI Automation Agency** | Identify companies with urgent automation needs and stronger budgets. |
| **Software / Development Agency** | Prioritize web, app, or software project inquiries. |
| **Consulting Firm** | Qualify prospects using budget, company size, timeline, and requirements. |
| **B2B Service Company** | Route high-intent inquiries to sales representatives automatically. |
| **Freelancer / Small Agency** | Reduce time spent manually reviewing contact-form submissions. |
| **Sales Team** | Create a consistent first-pass qualification process before human follow-up. |

The same pattern can later be connected to a CRM, Slack/Teams, calendar booking, WhatsApp, or a full sales pipeline.

---

## 🔄 Workflow Architecture

```text
┌─────────────────────────────┐
│   Prospect submits form     │
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│      n8n Form Trigger       │
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│            Wait             │
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│          AI Agent           │
│        OpenAI GPT-5-mini    │
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│ Structured Output Parser    │
│ score / category / reason   │
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│       Google Sheets         │
│        All Data             │
└──────────────┬──────────────┘
               ▼
        ┌──────┼──────┐
        ▼      ▼      ▼
      🔥 Hot  🟡 Warm  ⚪ Cold
        │      │      │
        ▼      ▼      ▼
     Email   Email   Email
        │      │      │
        ▼      ▼      └──────────
   Team Alert  Team Review
```

---

## 🧠 AI Qualification

The AI Agent analyzes information collected from the intake form, including:

- Full name
- Business email
- Company name
- Position
- Company size
- Estimated budget
- Desired start timeline
- Requested service
- Project description
- Company website

The AI is instructed to return machine-readable JSON instead of free-form text:

```json
{
  "score": 85,
  "category": "Hot",
  "reason": "High budget and urgent project"
}
```

The Structured Output Parser makes the AI response predictable for downstream automation.

> **Important:** The example score above is the sample output defined in the original workflow. The project does not claim that every lead is scored using a fixed mathematical formula; the qualification is AI-driven.

---

## 🔥 Lead Routing

The workflow supports three categories:

| Category | Purpose | Typical business action |
|---|---|---|
| 🔥 **Hot** | High-priority opportunity | Immediate human follow-up |
| 🟡 **Warm** | Potential opportunity requiring review | Sales review and follow-up |
| ⚪ **Cold** | Lower-priority / weaker current fit | Automated acknowledgement or future nurture |

The n8n Switch node routes the AI-generated category into separate Hot, Warm, and Cold branches.

---

## 📋 Lead Intake Form

The form captures:

- **Full Name**
- **Business Email**
- **Company Name**
- **Your Position**
- **Company Size:** 1–10, 11–50, 51–200, 200+
- **Estimated Budget:** < $500, $500–$1,000, $1,000–$5,000, > $5,000
- **Start Timeline:** Immediately, Within 1 Month, Within 3 Months, Just Exploring
- **Service:** AI Chatbot, AI Agent, Workflow Automation, Other
- **Project Description**
- **Company Website**
- **Contact Consent**

---

## 📊 Data Storage

Qualification results are stored in Google Sheets with fields such as:

- Name
- Email
- Budget
- Score
- Category
- Reason

The workflow also maintains separate Hot, Warm, and Cold destinations so teams can quickly review leads by priority.

---

## 📧 Automated Communication

### 🔥 Hot Lead

The prospect receives a high-priority project-fit email. The internal team can receive a separate alert containing the lead's details, AI score, category, reason, budget, timeline, requested service, and suggested next actions.

### 🟡 Warm Lead

The prospect receives an acknowledgement, while the internal team receives a review notification with the lead's basic information and AI classification.

### ⚪ Cold Lead

The prospect receives a polite acknowledgement explaining that the project may not currently be the best fit while leaving the door open for future opportunities.

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| **n8n** | Workflow orchestration and routing |
| **OpenAI GPT-5-mini** | AI-based lead analysis |
| **Structured Output Parser** | Reliable JSON output |
| **Google Sheets** | Qualification result storage |
| **Gmail** | Prospect and internal notifications |
| **n8n Form Trigger** | Lead intake |

---

## 📁 Repository Structure

```text
AI-Lead-Qualification-Scoring-Engine/
├── README.md
├── n8n-workflow.json
├── examples/
│   ├── sample-lead.json
│   └── sample-ai-output.json
└── .gitignore
```

### Files

- [`n8n-workflow.json`](./n8n-workflow.json) — sanitized, importable workflow configuration derived from the project JSON export.
- [`examples/sample-lead.json`](./examples/sample-lead.json) — example form submission.
- [`examples/sample-ai-output.json`](./examples/sample-ai-output.json) — example structured AI qualification response.

---

## 📦 How to Import and Configure

1. Open **n8n**.
2. Create a new workflow.
3. Use **Import from File**.
4. Select `n8n-workflow.json`.
5. Connect your own OpenAI credential.
6. Connect your own Google Sheets credential and select the destination spreadsheet.
7. Connect your own Gmail credential.
8. Replace `YOUR_GOOGLE_SHEET_ID` with your spreadsheet configuration.
9. Replace `YOUR_INTERNAL_TEAM_EMAIL` with your internal notification address.
10. Test the workflow with the sample lead before enabling production use.

---

## 🔐 Security & Public Repository Safety

The repository intentionally does **not** publish production credentials or private account configuration.

Before sharing an n8n workflow publicly, never commit:

- API keys
- OAuth access/refresh tokens
- Passwords
- Private webhook secrets
- Production credential IDs
- Private customer data

Reconnect credentials inside your own n8n instance after importing the workflow.

---

## 📈 Business Impact

When deployed in a real sales process, this type of automation can help a team:

- Respond faster to high-intent prospects.
- Reduce repetitive manual qualification work.
- Standardize the first stage of lead evaluation.
- Keep qualification data organized.
- Separate urgent opportunities from lower-priority inquiries.
- Give salespeople more time for conversations and closing.

The system is designed as an **AI-assisted qualification layer**, not as a replacement for final human sales judgment.

---

## 🚀 Future Improvements

Potential production upgrades include:

- CRM integration with HubSpot, Salesforce, or Pipedrive.
- Lead deduplication.
- Configurable scoring rules and category thresholds.
- Automated multi-step nurture sequences.
- Slack or Microsoft Teams notifications.
- Calendar booking for Hot leads.
- Lead-source attribution.
- Analytics dashboard for category-to-conversion performance.
- Human approval before high-value outreach.
- Retry and error-handling branches.
- Automated tests for qualification edge cases.
- Persistent lead history and re-scoring when project requirements change.

---

## 👨‍💻 Author

**Angkon Biswas**  
AI Automation Engineer | AI Agents | Workflow Automation

- GitHub: [@angkonbiswas](https://github.com/angkonbiswas)

---

> **Inbound inquiry → AI qualification → priority routing → automated follow-up.** 🚀

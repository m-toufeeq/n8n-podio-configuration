# Real Estate AI Caller & Lead Automation (n8n)

A collection of n8n workflows designed to automate real estate lead follow-ups, AI voice calls, and CRM management. This system acts as an automated virtual assistant, bridging Podio (CRM), Retell AI (Voice AI), smrtPhone (Telephony), and Slack to ensure no lead falls through the cracks.

## 🚀 Features

* **Automated Outbound Calling:** Triggers Retell AI voice agents to call leads automatically when their status changes in Podio or when a new lead is created.
* **Intelligent Post-Call Analysis:** Ingests post-call webhooks from Retell AI, parses the conversation summary, determines lead motivation/urgency, and updates the Podio CRM with actionable notes.
* **Smart SMS Routing:** Utilizes smrtPhone to send automated SMS follow-ups based on lead interactions.
* **Team Notifications:** Alerts the team via Slack when a "Hot Lead" is identified by the AI agent.
* **Webhook Maintenance:** Includes a utility workflow to automatically validate and keep Podio webhooks alive.

## 🏗 Architecture & Integrations

* **Automation Engine:** [n8n](https://n8n.io/)
* **CRM:** Podio
* **Voice AI:** Retell AI
* **Telephony/SMS:** smrtPhone
* **Internal Comms:** Slack

## 📂 Workflows Included

1.  **`inbound-post-call-analysis.json`**
    * Receives data after an inbound call concludes.
    * Parses the transcript for property address, asking price, property condition, and seller urgency.
    * Updates the existing Podio item or creates a new hot lead.
    * Fires a Slack alert for the team.
2.  **`outbound-post-call-analysis.json`**
    * Similar to the inbound workflow, but maps the analysis back to the specific outbound lead initiated in Podio.
3.  **`outbound-agent-new-lead.json`**
    * Listens for new lead creation webhooks.
    * Triggers an immediate AI outbound call to pre-qualify the lead.
4.  **`outbound-call-updated-lead.json`**
    * Listens for specific status changes in Podio.
    * Sends a preliminary SMS message via smrtPhone.
    * Initiates an outbound Retell AI call dynamically populated with the seller's name and property details.
5.  **`keeps-podio-webhooks-alive.json`**
    * A scheduled utility task that sends POST requests to Podio's validation endpoints to prevent webhook expiration.

## ⚙️ Setup & Installation

1.  **Import Workflows:** Download the JSON files from this repository and import them directly into your n8n instance.
2.  **Configure Credentials:**
    * Set up your **Podio OAuth2 API** credentials in n8n.
    * Set up your **Retell API** credentials (Bearer token).
    * Set up your **smrtPhone** Header Auth credentials.
    * Set up your **Slack API** credentials.
3.  **Map Variables:** Update the workflows with your specific Podio App IDs, Workspace IDs, Retell AI Agent IDs, and Slack Channel IDs.
4.  **Activate:** Toggle the workflows to active.

## ⚠️ Disclaimer
Ensure you comply with all local telemarketing and AI disclosure laws (e.g., TCPA) when using automated dialing and AI voice agents.

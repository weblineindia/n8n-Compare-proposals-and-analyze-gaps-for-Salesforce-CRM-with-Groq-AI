# AI Proposal Comparison & Gap Analysis Workflow for Salesforce CRM

This workflow automatically analyzes newly uploaded proposals by comparing them with past winning proposals using AI. It extracts proposal content, identifies the client, fetches reference data from Google Sheets and generates actionable insights. These insights are saved in Salesforce and shared on Slack for team visibility.

### Quick Implementation Steps

- Connect Google Drive, Google Sheets, Salesforce, Slack and Groq AI credentials in your **[n8n account (self-hosted or cloud)](https://n8n.partnerlinks.io/om1efg2qgvwi)**.
- Set your Google Drive folder to monitor proposal uploads.
- Ensure your Google Sheet contains winning proposals with `status = Won`.
- Activate the workflow.
- Upload a proposal file to trigger analysis automatically.

---

## What It Does

This workflow automates the process of analyzing business proposals by leveraging AI and historical data.

When a new proposal file is uploaded to a specific Google Drive folder, the workflow downloads and extracts its content. It then identifies the client name using a simple pattern from the text. At the same time, the workflow fetches past winning proposals from a Google Sheets database filtered by status.

Both the current and past proposals are combined and sent to an AI model for comparison. The AI generates concise insights highlighting missing elements, weak positioning, pricing gaps and improvement suggestions.

Finally, the insights are formatted and stored in Salesforce as an Opportunity record. A notification is sent to Slack, ensuring the team is informed and can act quickly to improve proposal quality.

---

## Who It's For

- Sales teams managing multiple proposals
- Business development professionals
- Proposal review and strategy teams
- Organizations using Salesforce CRM
- Teams looking to improve win rates using AI

---

## Requirements

To use this workflow, you will need:

- **[n8n account (self-hosted or cloud)](https://n8n.partnerlinks.io/om1efg2qgvwi)**
- Google Drive account (with folder for proposals)
- Google Sheets account (with winning proposals data)
- Salesforce account (Opportunity access enabled)
- Slack workspace (channel for notifications)
- Groq API credentials (for AI model access)

## How It Works & Set Up

### 1. Setup Google Drive Trigger

- Configure **New Proposal Upload Trigger**.
- Select the folder where proposals will be uploaded.
- Event: `fileCreated`.

### 2. Download and Extract Proposal

- Use **Download Proposal** node to fetch the file.
- Use **Read Proposal Text** node to extract content.

### 3. Extract Client Information

- Use **Extract Client Info (Code node)**.
- Extract `clientName` using regex from the proposal text.
- Store the complete proposal as `currentProposal`.

### 4. Fetch Winning Proposals

- Configure **Get Winning Proposal Data (Knowledge Base)**.
- Connect your Google Sheet.
- Filter records where `status = Won`.

### 5. Combine Data

- Use **Combine Proposal Data (Merge node)**.
- Merge the current proposal and past winning proposals.

### 6. AI Analysis

- Use **AI Proposal Gap Analyzer**.
- Provide a prompt to compare proposals.
- Generate structured insights (8–10 bullet points).

### 7. Format Output

- Use **Format Analysis Output**.
- Map `clientName` and `analysisSummary`.

### 8. Save to Salesforce

- Use **Save Insights to Salesforce**.
- Create an Opportunity.
- Add AI insights to the Description field.

### 9. Prepare Final Output

- Use **Prepare Final Output (Merge node)**.

### 10. Add Delay (Optional Control)

- Use **Wait for Save** node (2-second delay).

### 11. Send Slack Notification

- Use **Send Notification to Slack**.
- Send a formatted message containing the proposal insights.

---

## How To Customize Nodes

- **Extract Client Info:** Modify the regex if your proposal format changes.
- **Google Sheets Node:** Change filters or add more reference columns.
- **AI Prompt:** Customize the output format or analysis depth.
- **Salesforce Node:** Change the Opportunity stage, fields or object type.
- **Slack Node:** Update the message format or destination channel.
- **Wait Node:** Adjust the delay time if needed.

---

## Add-ons

You can extend this workflow by adding:

- Email notifications using Gmail or Outlook
- Store proposal analysis history in Google Sheets
- Advanced error handling with IF nodes
- Multiple proposal comparison logic
- Dashboard integrations with Notion, Airtable or similar platforms

## Use Case Examples

- **Improving Proposal Quality Before Client Submission**  
  Compare new proposals with previous winning proposals to identify missing content, weak positioning and areas for improvement before sending them to clients.

- **Training New Sales Team Members**  
  Use historical winning proposals and AI-generated insights to help new sales representatives understand what makes successful proposals.

- **Automating Proposal Review Workflows**  
  Eliminate manual proposal reviews by automatically generating comparison reports and recommendations whenever a proposal is uploaded.

- **Identifying Common Gaps in Losing Proposals**  
  Analyze recurring weaknesses across proposals to improve proposal templates, messaging and pricing strategies.

- **Tracking Proposal Insights in Salesforce CRM**  
  Store AI-generated proposal analysis directly in Salesforce Opportunities for future reference and team collaboration.

*There can be many more use cases depending on how you extend this workflow.*

---

## Troubleshooting Guide

| Issue | Possible Cause | Solution |
| ------ | -------------- | -------- |
| No trigger on file upload | Incorrect Google Drive folder selected | Verify the Google Drive folder ID and ensure the trigger monitors the correct folder. |
| Client name not extracted | Proposal format does not match the expected pattern | Update the regex used in the **Extract Client Info** code node. |
| No data from Google Sheets | Filter mismatch (`status = Won`) | Verify the column name and ensure the status values exactly match `Won`. |
| AI output is empty | Missing prompt or incorrect merged input | Verify the merged data structure and AI prompt configuration. |
| Salesforce error | Invalid credentials or incorrect field mapping | Reconnect Salesforce credentials and verify the mapped fields. |
| Slack message not sent | Incorrect channel or authentication issue | Reconnect Slack credentials and verify the selected channel. |
| Workflow stops before Slack notification | Wait node is misconfigured | Ensure the workflow continues correctly after the **Wait for Save** node. |

---

## Need Help?

If you need help setting up, customizing or extending this workflow, our **n8n automation experts at WeblineIndia** are here to help.

We can assist you with:

- n8n workflow setup and deployment
- Google Drive, Google Sheets, Salesforce and Slack integrations
- AI-powered proposal comparison and gap analysis
- Custom Salesforce CRM automations
- Proposal review and approval workflows
- Dashboard and reporting integrations
- Enterprise-grade workflow optimization and scaling

👉 **Our experienced n8n developers can help you build, customize and scale AI-powered proposal automation tailored to your business requirements.**

**Contact WeblineIndia:** https://www.weblineindia.com/contact-us.html

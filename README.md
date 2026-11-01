*Intuz — Your automation partner, one workflow at a time.*

<p align="center">
  <picture>
    <img alt="Banner Image" src="https://github.com/user-attachments/assets/210f97fc-0fce-404a-b647-7dfe1302cd37" />
  </picture>
</p>

[Intuz](https://www.intuz.com) helps organizations orchestrate AI, automation, and enterprise systems through scalable workflows. Our repository showcases proven implementations across healthcare, operations, customer support, document processing, sales, and back-office functions, enabling teams to accelerate automation initiatives without starting from scratch.

[N8N Creator](https://n8n.io/creators/intuz/) · [AI Automation Company](https://www.intuz.com/company/) · [AI Development Company](https://www.intuz.com/company/) · [For Custom Workflow Automation](https://www.intuz.com/get-started/)

# Send tiered overdue invoice reminders with Xero, Gmail, Slack, and Google Sheets

## Quick overview

This workflow runs daily to pull unpaid invoices from Xero, calculates how overdue they are, sends tiered Gmail reminders and Slack alerts, and logs each invoice-tier reminder in Google Sheets to prevent duplicate follow-ups.

## How it works

1. Runs every day at 08:00 using a scheduled trigger.
2. Loads reminder thresholds (7/14/30 days) and then fetches unpaid invoices from Xero for the selected organisation.
3. Calculates each invoice’s days overdue, assigns it to a 7-, 14-, or 30-day tier, and prepares key fields like contact email, amount due, and a unique `invoiceId_tier` identifier.
4. Checks a Google Sheets log to see whether that `invoiceId_tier` reminder has already been sent and skips any that are already recorded.
5. For 7-day overdue invoices, sends a friendly reminder email to the customer via Gmail.
6. For 14-day overdue invoices, sends a firmer Gmail reminder and posts an internal Slack alert about the overdue invoice.
7. For 30-day overdue invoices, posts a Slack escalation message that includes a call task, then writes the processed `invoiceId_tier` entries back to Google Sheets.

## Setup

1. Add Xero OAuth credentials and set the correct Organisation/Tenant ID in the Xero node.
2. Add Gmail OAuth credentials and ensure your Xero contacts have an email address populated so reminders have a valid recipient.
3. Add Google Sheets OAuth credentials and point both Google Sheets nodes to a spreadsheet tab that includes an `invoiceId_tier` column for deduplication.
4. Add Slack credentials, set the target channel IDs in both Slack nodes, and invite the Slack app/bot to those channels.
5. Review and adjust the tier day thresholds and message text (email and Slack) to match your collections process before activating the workflow.

## Requirements

- ## Quick troubleshooting
- 403 AuthenticationUnsuccessful on Xero → usually Return All on, or wrong/expired org auth.
- Empty Calculate output → invoices not ≥ tier1 days overdue, or date parse issue (workflow already handles /Date(...)/ + DueDateString).
- Slack shows {{ $... }} text → message field missing leading =.
- No email → contactEmail null (Xero contact has no email).

## FAQ

**What does this workflow do?**  
It pulls unpaid invoices from Xero daily, calculates overdue tiers, sends tiered Gmail reminders and Slack alerts, and logs reminders in Google Sheets to avoid duplicates.

**How are reminders tiered in this workflow?**  
Invoices are categorized into 7-, 14-, or 30-day overdue tiers, with different email and Slack notifications sent for each tier.

**What integrations are required to set up this workflow?**  
You need OAuth credentials for Xero, Gmail, Google Sheets, and Slack, and must configure organization IDs, spreadsheet tabs, and Slack channels accordingly.

## Related n8n templates from Intuz

- [In-build Admin Panel and basic APIs for mobile app from Intuz](https://github.com/Intuz-production/Backend-API-NodeJs)
- [FCM Push Notification for PHP](https://github.com/Intuz-production/FCM-Push-Notification-PHP)
- [When an Airtable deal is approved for invoicing, sync the customer in QuickBooks and Stripe, generate the invoice and payment link, and write everything back to Airtable — no manual sales-to-cash handoffs.](https://github.com/Intuz-production/QuickBooks-Invoice-Payment-Automation)

[See all of Intuz's free n8n templates](https://www.intuz.com/n8n-workflow-automation-templates/)

## Connect with us

Intuz is a USA-based AI & workflow automation company with 16+ years of experience building custom AI-enabled workflow automations for SMBs and Enterprises, specializing in agentic AI, LLM integrations, and CRM/ERP sync across Healthcare, FinTech, eCommerce, Manufacturing, and Real Estate.

* **Website:** [https://www.intuz.com](https://www.intuz.com)
* **Email:** [getstarted@intuz.com](mailto:getstarted@intuz.com)
* **LinkedIn:** https://www.linkedin.com/company/intuz/
* **Get Started:** https://n8n.partnerlinks.io/intuz

## For Custom Workflow Automation

[Click here - Get Started](https://www.intuz.com/get-started/)

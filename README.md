# Webflow → Slack Lead Automation (Make.com)

## Overview
This project is a production-ready Make.com automation that processes Webflow form submissions and delivers real-time Slack notifications with built-in validation, fallback routing, and error handling.

The workflow ensures that sales teams receive clean, actionable lead alerts, while technical teams are notified immediately if submissions are incomplete or systems fail.

---

## What This Automation Does

**Trigger**
- Receives Webflow form submissions via a Make.com custom webhook

**Validation**
- Checks required fields:
  - Name
  - Email
  - Site Name

**Routing Logic**
- ✅ **Valid submissions** → Posted to a sales Slack channel
- ⚠️ **Incomplete submissions** → Routed to a system alerts Slack channel with diagnostics

**Error Handling**
- Retries Slack API calls automatically in case of transient failures
- Breaks execution after repeated failures
- Stores incomplete executions for later inspection

---

## Slack Notifications

### Valid Lead Alert
Includes:
- Name
- Email (clickable)
- Company (if provided)
- Phone (if provided)
- Message (with graceful fallback if empty)
- Submission timestamp
- Source form and site context

### Incomplete Submission Alert
Includes:
- Clear list of missing required fields
- Raw payload received for debugging
- Client / site identification
- Actionable guidance for fixing the form configuration

---

## Error Handling Strategy

This automation distinguishes between **business logic errors** and **technical failures**:

- **Business logic issues** (missing required fields)  
  → Routed intentionally to a fallback Slack alert

- **Technical failures** (Slack API errors, connectivity issues)  
  → Retried automatically (3 attempts, 2-minute intervals)  
  → If retries fail, the execution is marked as incomplete and stored for review

- **Incomplete executions** are stored for audit and replay

This layered approach prevents silent failures and protects downstream systems.

---

## Technologies Used
- Make.com (Scenarios, Routers, Error Handlers)
- Webflow (Form submissions)
- Slack API (Message delivery)
- JSON webhooks
- Conditional logic and formatting functions

---

## Files Included

- `SCENARIO_1_blueprint__10_.json`  
  Sanitized Make.com scenario export (safe for sharing)

  **Note:** Make.com’s blueprint export does not always fully reflect router fallback paths in a human-readable way.  
  The live scenario contains two routes:
  - Valid data → sales alerts
  - Invalid data → system alerts  
  as documented in this README and verified via execution logs.

  - `README.md`  
  Project documentation

---

## Use Case Examples
- Agency lead notifications from Webflow sites
- Internal sales alerting systems
- Form monitoring and failure detection
- Client-facing automation demos

---

## Notes
- All identifiers, URLs, and data have been sanitized.
- This project is intended as a portfolio demonstration of automation design, validation, and reliability patterns.

## Contact

Questions or collaboration?

This project was built as part of an Upwork automation engineering portfolio.  
Feel free to reach out via Upwork or GitHub for questions, feedback, or collaboration opportunities.

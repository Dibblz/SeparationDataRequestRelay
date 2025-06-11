# SeparationDataRequestRelay

# MES 3.4 – Separation Data Request Relay

## Overview

This Power Automate **Cloud Flow** handles incomplete separation tickets in ServiceNow by detecting related Outlook emails, initiating a Microsoft Form request to the agent's manager, and forwarding the completed form response for automated ticket completion.

## Functionality

- Monitors a specific Outlook folder for new emails tied to separation tickets.
- Extracts relevant ticket and manager data from the email content.
- Sends a Microsoft Form link to the agent’s manager requesting the missing separation details.
- Waits for the form submission.
- Forwards the completed form data to a designated intake address, triggering a downstream automation that updates the ticket.

## Prerequisites

- Power Automate Cloud access with required connectors enabled:
  - **Outlook** (email and folder monitoring)
  - **Microsoft Forms** (response collection)
  - **Office 365 Mail** (to send/forward)
- Redirect rule set up in Outlook to move relevant ServiceNow ticket emails into a monitored folder.
- Pre-created Microsoft Form with defined fields for required separation data.
- Downstream process (separate flow or script) that monitors the inbox receiving the form results and updates the original ticket.

## How to Run

> This flow is **triggered automatically** when a new email appears in the designated Outlook folder.

Once triggered, it will:
1. Parse the incoming email for agent and manager information.
2. Compose and send a form link to the manager.
3. Wait for the form to be completed.
4. Email the form response to the designated processing inbox.

No manual launch or intervention is required.

## Notes

- Ensure the Microsoft Form is publicly accessible or configured to allow authenticated internal users only, depending on your org’s policy.
- Form structure must match what the downstream automation expects.
- If the manager's email is missing or the incoming ticket email is malformed, the flow may silently fail unless error handling is explicitly added.
- The flow is designed for **attended or unattended execution**, but monitoring is recommended in early rollout.


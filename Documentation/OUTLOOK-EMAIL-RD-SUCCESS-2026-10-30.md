# R&D Milestone — Microsoft 365 Outlook Email Sending

**Date:** 2026-10-30  
**Status:** Confirmed interactive send; production automation NOT validated  
**Scope:** Isolated OneDrive R&D prototype only  
**Repository:** `mshilcrat/hasc-reminder-portal`  
**Hosted URL:** https://mshilcrat.github.io/hasc-reminder-portal/

## Outcome

The user tested the Outlook connection test from the hosted R&D project and provided a screenshot showing the test message received in Outlook. The email subject was **HASC OS Outlook connection test** and the body stated: **This is a test message from the HASC OneDrive R&D portal. No HASC OS records were accessed.**

This confirms an interactive test message was received. The screenshot alone does not independently prove the exact Graph response code or tenant-side audit trail.

## Verified implementation (repository `index.html`)

- Existing Microsoft application client ID is supplied in the portal UI.
- MSAL Browser authenticates a HASC Center account interactively.
- The test requests delegated Microsoft Graph `Mail.Send` permission.
- A `POST` request goes to `https://graph.microsoft.com/v1.0/me/sendMail`.
- Request includes a subject, plain-text body, recipient and `saveToSentItems: true`.
- Response status and Graph error text are displayed in the R&D UI.
- No passwords, application secrets or access tokens should be embedded in source code.
- Hosted HTTPS is required for the current Microsoft authentication flow; opening a local `file://` HTML copy is insufficient.

## Reproduce the test

1. Open the existing R&D URL.
2. Use the already approved Microsoft application registration and client ID.
3. Connect/sign in with the HASC account.
4. Enter a test recipient and click **Send Test Email**.
5. Confirm the Graph request is accepted, check Outlook Sent Items, and confirm receipt in the target inbox.
6. If it fails, capture the HTTP status, Graph error code, and request ID without exposing tokens or secrets.

## What is NOT yet established

- Unattended/background sending without an interactive signed-in user.
- Tenant-approved application-level `Mail.Send` permissions and mailbox scoping.
- Reliable scheduling, retries, quotas, delivery/bounce handling, or a production audit trail.
- HIPAA approval or security assessment for notification contents.
- Any connection to HASC OS, FRIDAY, MAIN or production Supabase.

## Security and deployment boundaries

The OneDrive R&D prototype is a proof of concept, completely separate from HASC OS. Do not connect to HASC OS, Supabase, or production data without explicit authorization. Send only non-sensitive test messages. Keep tenant authorization, least-privilege mailbox permissions, organizational mail policies, and protected health information handling under IT/security review.

## Next technical milestone

Demonstrate a single approved **unattended** email from a secure server-side process, using Microsoft Graph and narrowly scoped permission to send from the designated HASC mailbox. Validate the exact configuration with IT before integrating any notification workflow.

## Source and verification

- Repository `index.html`, main branch, blob SHA `e3dc30c9c230804cd97a836ce3891eca9ba9b1d8` at documentation time.
- User-provided Outlook screenshot, 2026-10-30, showing the received test email.

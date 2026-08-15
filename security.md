# Security Policy

## About This App

This is a field data collection tool, built as a static web app 
(GitHub Pages) with a Google Apps Script / Google Sheets backend. 
It is not a public software package with versioned releases as it's 
a living single-file app maintained for APPA staff,
ATC staff, and trained A.T. Club volunteers.

## Data Handled

- Field assessment data: species, defect/risk scores, GPS coordinates,
  determinations, and free-text notes.
- Field photographs, uploaded to a Google Drive folder tied to the backend
  Google Sheet.
- No personally identifiable information (PII) about members of the public is
  intentionally collected. Inspector/surveyor names and initials entered in
  the app are the only personal data involved, and are limited to staff and
  volunteers performing the assessment.

## Known Architecture Limitations

Please read this section before treating anything below as a "vulnerability" —
these are known, accepted tradeoffs for a small internal tool, not bugs:

- **The `SHARED_TOKEN` in the app's `CONFIG` block is not a secret.** It ships
  in the page's client-side source and is visible to anyone who views source
  on the deployed site. It exists to keep casual/accidental writes off the
  shared Google Sheet, not to provide real access control. Do not rely on it
  to restrict access to sensitive data, and do not reuse it as a password
  anywhere else.
- **The Google Apps Script Web App endpoint is public.** Anyone with the
  deployment URL and the shared token can read or write entries. Treat the
  URL and token with the same care as a shared document link.
- **The Pl@ntNet API key is also client-visible.** It is a free-tier key with
  no sensitive scope; if it's ever abused or rate-limited, generate a new one
  in the Apps Script backend and redeploy.
- **There is no user authentication.** The app does not verify who is
  submitting data — it trusts anyone with the app URL and token. This is a
  deliberate simplicity tradeoff for a small field team, not an oversight.

## Reporting a Security Concern

If you find something that goes beyond the known limitations above — for
example, a way to access data without the token, a way to write to the
backend that bypasses validation in a harmful way, or exposure of data that
shouldn't be public — please report it directly rather than opening a public
GitHub issue:

**Contact:** Casey Reese, creese333@gmail.com

Please include:
- What you found and how you found it
- Steps to reproduce, if applicable
- Any data exposure you observed (please don't include real field data or
  photos in your report — a description is enough)

## Response

This is a small internal tool maintained by one person alongside other
duties, so please allow a reasonable amount of time for a response. Genuine
data-exposure issues will be prioritized over cosmetic or low-impact reports.

## Scope

This policy covers the app's frontend (this repository) and its Google Apps
Script / Google Sheets / Google Drive backend. It does not cover Google's own
infrastructure, GitHub Pages hosting infrastructure, or third-party services
(Pl@ntNet, OpenStreetMap tile servers) this app calls — please report issues
with those services to their respective maintainers.

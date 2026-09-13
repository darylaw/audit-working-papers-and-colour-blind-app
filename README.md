# Audit Working Papers and Colour Blind App


This is the single GitHub entry point for the two projects in this submission.


| Project | Working demo | Source code |
| --- | --- | --- |
| Audit Working Papers | [Open updated audit demo](https://audit-working-papers-personal.darylaw307200.chatgpt.site) — ChatGPT sign-in; choose IFRS / SFRS(I) or US GAAP before importing | [Download complete audit source ZIP](https://github.com/darylaw/audit-working-papers-and-colour-blind-app/raw/refs/heads/main/audit-working-papers-submission.zip) |
| Colour Blind App (Hue) | [Open colour blind app demo](https://hue-personal.darylaw307200.chatgpt.site/) | [Colour blind app source repository](https://github.com/AwDaryl/hue) |


The projects are separate applications. Audit schedules stay within the audit app's browser session and are never sent to Hue or AI. Hue has its own optional photo-analysis flow and privacy terms; do not use it for client audit documents.


The complete audit source, tests, and 99 fictitious PBC spreadsheets are packaged in `audit-working-papers-submission.zip` in this repository. Extract the ZIP before using the paths and commands below. Hue's source is maintained in the linked repository. Each project's README explains how to run it and records its verification limits.


---
# Audit Working Papers


A browser-based working-papers platform for Singapore statutory audits. Import a PBC spreadsheet, inspect its source, review cleaning and column mapping, run deterministic tests, document auditor judgements, and export an Excel audit file.


**[Open the live demo](https://audit-working-papers-personal.darylaw307200.chatgpt.site)** — sign in with a ChatGPT account and choose the reporting framework at the front. Use fictitious data only while the remaining accuracy and browser-verification work is completed.


## Try it


1. Open the demo, or download and extract `audit-working-papers-submission.zip` and double-click its `app/audit-working-papers.html`. The standalone file needs no installation, server, or network.
2. Click **Fill demo details**.
3. Pick a section and use its downloadable sample, or select a matching file from `synthetic-data/out/client-a/`.
4. Review the source, cleaned listing, mapping, working papers, and exceptions.
5. Export each section before reloading, closing, or ending the session. All engagement data is memory-only.


Every supplied client, person, supplier and figure is synthetic. No confidential audit files are included.


## What it covers


21 sections: trial balance, planning/materiality, fixed assets, intangible assets, impairment, inventory, receivables/ECL, other receivables/prepayments, cash, payables, accruals, provisions, borrowings, leases, taxation, equity, revenue, expenses, payroll, going concern and related parties.


The engine detects varied headings, cleans messy schedules, maps typed fields, and raises exceptions graded against materiality. Working-paper exports include source data, cleaned records, mappings, cleaning logs, corrections, audit trails, auditor input columns and live Excel formulas. Figures and exceptions are deterministic; no AI makes a calculation or approves a conclusion.


## Confidentiality design


- Parsing, cleaning, mapping, calculations and Excel generation run in the browser.

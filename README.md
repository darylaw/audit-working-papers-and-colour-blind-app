# Audit Working Papers

A browser-based working-papers platform for Singapore statutory audits. Import a PBC spreadsheet, inspect its source, review cleaning and column mapping, run deterministic tests, document auditor judgements, and export an Excel audit file.

**[Open the live demo](https://audit-working-papers-personal.darylaw307200.chatgpt.site)** — sign in with a ChatGPT account. Use fictitious data only while the remaining accuracy and browser-verification work is completed.

## Try it

1. Open the demo or double-click `app/audit-working-papers.html`. The standalone file needs no installation, server, or network.
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
- The application has no audit-data upload endpoint or AI calls. Hosted routes accept GET/HEAD only.
- Engagements, mapping profiles, schedules and notes stay in tab memory. Legacy browser-saved audit entries are removed.
- Ending a session clears app tabs on the same origin; page lifecycle cleanup prevents restoring the old working screen.
- Spreadsheet text is rendered as text, with only a small formatting vocabulary. No HTML parser insertion sinks remain in application rendering.
- Content Security Policy permits only the exact bundled script hashes and blocks network connections, form submissions, active frames, objects, workers and remote images.
- Fonts and dependencies are bundled. No analytics or third-party scripts are added by the application.

Authentication and hosting are provided by Sites. Those platform services are distinct from client-side audit processing. See [SECURITY.md](SECURITY.md) for verification limits.

## Run the checks

Requires Node.js and Python 3; the app itself has no package installation step.

```sh
python app/build.py
node app/test/run-all.js
node app/test/test-offline.js
node app/test/test-confidentiality.js
```

The regression suite records **6,136 passed, 0 failed, 0 crashed across 27 files**, including **83 targeted confidentiality checks**. Dedicated offline/privacy checks record **28 passed, 0 failed**. The 99 synthetic spreadsheets under `synthetic-data/out/` are shipped so the suite can run immediately.

The optional synthetic generator uses Python `openpyxl` and regenerates the fixture pack:

```sh
python synthetic-data/generator/build.py
```

## Architecture

Vanilla JavaScript, no framework, with a Python concatenation build producing one self-contained HTML file. `core.js` handles import, mapping, typed records and tests. `spec.js` renders declarative working papers and worksheet rows. Section modules live in `app/src/modules/`; PPE is the hand-built reference. `xlsxstyle.js` writes styled OOXML locally.

For a separate Sites deployment, register your own Site and create `.openai/hosting.json` with its project ID before running `npm run build:site`. Credentials and the original Site's deployment configuration are excluded from this repository.

## Known limitations

A separate ten-industry stress pack exposed accuracy defects that are not yet fixed: two PPE column-mapping cases, a native Excel date shifting by one day, and flat related-party rows merging counterparties. Passing the established suite does not mean every possible input is correct. Confirm mappings and review all output.

Desktop Excel repair/recalculation checks and complete live network capture remain outstanding. Generated working papers require evidence, professional judgement, exception resolution and review. No ACRA inspection pass is claimed. SFRS(I)/IFRS is the reporting framework; this is a testing demonstration, not a substitute for an audit.

Third-party vendored components retain their own licence terms, including SheetJS and the Montserrat fonts.

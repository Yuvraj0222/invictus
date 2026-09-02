# FairShare

FairShare is a browser-based bill splitter for groups travelling together. It records who paid, who participated, and exactly how much each person should cover.

## Run locally

npm install
npm run dev

Open the local Vite URL in a browser.

## Included behavior

- Equal split with deterministic cent remainder handling.
- Custom percentage split with exact 100% validation and cent-safe allocation.
- Payer and participants are independent, so a payer can be outside the split.
- Filtered expenses drive the visible totals, balances, and settle-up plan consistently.
- Expenses can be edited or deleted; people can be added and safely removed when unreferenced.
- Data persists under the fairshare-data-v1 local-storage key. If the key is absent or malformed, the original demo dataset is restored.
- No backend or third-party data service is required.

## Verification scenarios

The important business rules are covered in the implementation using integer cents. The manual QA checklist for the assignment is recorded in BUGS.md.

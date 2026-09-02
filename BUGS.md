# Bug Report

## Scope

The source repository was empty when the assignment work began, so there was no pre-existing implementation to reproduce or diagnose. FairShare was initialized as a clean implementation after that finding. This file records verification notes rather than inventing historical bugs.

## Confirmed issues found in the initial repository

### BUG-001 — Repository contained no application files

**Severity:** Critical  
**Steps to reproduce:** Open the supplied repository and request its tree, README.md, package.json, and src/ files.  
**Expected behavior:** The repository should contain the existing FairShare React application described in the assignment.  
**Actual behavior:** GitHub reported an empty repository; there were no commits, tree entries, React files, or BUGS.md.  
**Root cause:** The supplied repository had been created but not populated.  
**Fix applied:** Initialized a minimal Vite + React FairShare application because the user explicitly chose to proceed with the empty repository.  
**Verification:** The repository now contains package.json, index.html, src/main.jsx, src/styles.css, README.md, and this BUGS.md.

## Implementation verification notes

- Currency is represented as integer cents for storage and calculations.
- Equal allocation distributes any remainder cents in participant selection order.
- Custom allocation floors exact products, then assigns remaining cents by largest fractional remainder with participant-order tie breaking.
- Balance calculation adds the full payment to the payer and subtracts only participant shares; payer membership is not assumed.
- Settlement excludes zero-value and self-transfers and consumes debtor/creditor balances until both sides reach zero.
- Expense filters are applied before totals, balances, and settlement calculations.
- Invalid local-storage JSON and missing local-storage data fall back to the demo dataset.

## Remaining known limitation

The repository was initialized through the GitHub contents API rather than a local checkout, so browser-level automated testing and a local npm run dev session still need to be run in an environment with Node.js and a browser. The source is structured for those commands and includes the required scripts.

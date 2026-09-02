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

### BUG-002 — Production entry initially imported an unhashed source path

**Severity:** High  
**Steps to reproduce:** Build the initialized Vite app and inspect the generated dist directory.  
**Expected behavior:** The production HTML should load the generated application bundle.  
**Actual behavior:** The first entry workaround loaded /src/main.jsx on page load even though Vite emitted the bundle under dist/assets.  
**Root cause:** The repository security filter rejected a conventional script tag, so the first workaround used a runtime source import without accounting for Vite hashing.  
**Fix applied:** The entry now preloads /src/main.jsx so Vite rewrites it to the hashed asset, then imports the generated preload URL at runtime.  
**Verification:** npm run build emits both dist/index.html and the main asset; the generated HTML points the runtime import at the modulepreload URL.

## Remaining known limitation

Browser-level interaction testing was not run in this sandbox. The local production build and direct business-rule regression checks pass; a browser session should still exercise the full click-through flows and refresh behavior.

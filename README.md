# Green Horizon — Egg Farming Profitability Ledger

A standalone web app version of the Green Horizon growth model: a month-by-month
ledger for an egg-laying flock, covering purchases, mortality, laying curve,
feed, labor, housing, loan amortization (with an optional grace period), and
a per-bird profitability calculator.

It runs entirely in the browser — no server, no backend, no build step.
Every number recalculates live as you edit the Assumptions panel or type
chick purchases into the ledger. Your data is saved to the browser's local
storage on this device only; nothing is uploaded anywhere.

## What's in this folder

- `index.html` — the whole app (HTML, CSS, and JavaScript in one file)
- `manifest.json`, `icon.svg`, `service-worker.js` — makes it installable as
  a Progressive Web App (works offline, can be "added to home screen" on
  a phone), same pattern as your other Green Horizon apps

## Deploy to GitHub Pages (same steps as your other Green Horizon apps)

1. Create a new repository on GitHub (e.g. `green-horizon-ledger`), or reuse
   an existing one.
2. Upload all the files in this folder to the repository root (or push them
   with git — see below).
3. In the repo, go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**, pick the `main`
   branch and `/ (root)` folder, then save.
5. GitHub will give you a URL like
   `https://<your-username>.github.io/<repo-name>/` — that's your live app,
   usually live within a minute or two.

### Using git from the command line

```bash
cd green-horizon-app
git init
git add .
git commit -m "Green Horizon profitability ledger"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then follow steps 3-5 above to turn on Pages.

## Using the app

- **Left panel** — every input from the Excel workbook's Assumptions tab:
  loan terms, bird timing, mortality, feed/egg prices, labor, housing, and
  the 15-month laying curve (collapsed by default — click to expand).
- **Ledger table** — one row per month. The only editable column is
  **Bought**; type in a number for any month to record a chick purchase.
  Everything else is calculated.
- **Months to project** (top right) — how many months the ledger and charts
  cover. Raise it to see further into the future.
- **Export CSV** — downloads the full ledger for use in Excel, Google
  Sheets, or anywhere else.
- **Reset to defaults** — wipes your changes and starts over.

## Notes on the model

This mirrors the Excel workbook's logic exactly (verified line-by-line
against it): mortality is applied once, when a batch reaches laying age;
housing and other bracket-based costs use last month's flock size to avoid
a circular calculation; the loan is a real amortizing loan with monthly
interest accrual, an optional grace period, and your choice of payment
frequency; the laying curve is age-based, not a flat percentage.

If you change assumptions dramatically (for example, a much older or
younger age at first lay), the "rearing months" and "productive months"
figures may need adjusting by hand to match — they aren't auto-derived from
the age-in-weeks fields, the same as in the original spreadsheet.

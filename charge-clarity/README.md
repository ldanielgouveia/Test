# Charge Clarity

A one-page dashboard for your Chase checking and credit card activity. It sorts every charge into categories, finds subscriptions and recurring bills (including price increases and ones that stopped), and explains each fee and interest charge along with how to avoid it.

## Use it

1. On chase.com (desktop), open an account → download icon above the transactions → **Spreadsheet (Excel, CSV)** → pick a date range → Download. Do this for each account.
2. Open `index.html` in a browser (or the published artifact link) and select **Import Chase CSV**, or drop the files onto the page.

Everything runs in your browser. Files are never uploaded; the parsed transactions are kept in that browser's local storage so they're there next time. **Remove my data** clears them.

## What it reads

- Checking/savings exports: `Details, Posting Date, Description, Amount, Type, Balance, Check or Slip #`
- Credit card exports: `Transaction Date, Post Date, Description, Category, Type, Amount, Memo`

Payments from checking to a card, and transfers between your own accounts, are left out of "Spent" so nothing is counted twice. Re-importing overlapping date ranges skips duplicates.

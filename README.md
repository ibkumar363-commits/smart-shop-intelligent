# Smart Shop Intelligent

A free, single-file point-of-sale web app for small businesses. Owners register their business and shops, cashiers serve customers and print receipts, and every sale is recorded for the owner by payment status. It runs in any modern browser, needs no server, and keeps working without internet.

> **Status:** working prototype. Data is stored on the device, not online. Read [Limitations](#limitations) before using it for a real business.

## Features

### Owner / manager
- **Register a business**: business name, owner name, phone, number of shops, a password of **14+ characters**, and your own recovery question.
- **Business ID**: each business gets a unique ID (for example `GREENMARTS-4K7Q`) that cashiers use to log in.
- **Transaction history** in three tabs: **Paid**, **Partial** and **Credit**. Filter by shop, customer name, invoice number or date.
- **Record later payments**: if the amount equals the balance the sale moves to Paid; a smaller amount keeps it Partial.
- **Inventory**: items with stock quantity, price per carton and price per piece. Edit or delete at any time.
- **Cashier accounts**: create cashier logins, assign each to a shop, view passwords (so a forgotten one can be given back), delete accounts.
- **Shops**: add as many shops as needed and give each a name.
- **Export**: download transactions for any period as **CSV** or **Excel (.xlsx)**, filtered by status or shop.
- **Settings**: edit business details, upload your own logo, choose a logo style (3D, flat or outline), change password.
- **Password recovery** using the question the owner wrote at registration.

### Cashier
- Log in with the **Business ID** and a personal password.
- **Find items**: search inventory by name, choose carton or piece and quantity.
- **Automatic fields**: invoice number, current date, cashier name (Served By) and the shop assigned by the owner.
- **Leave for later**: park an unfinished sale, serve another customer, resume afterwards.
- **Returning customers**: entering the same name and phone number reuses that customer's earlier invoice number.
- **Print receipt** with business name, logo, status banner (Paid in full, Partial payment or On credit), items, totals and balance due. Customer address and customer signature are not included.
- Each printed sale is recorded immediately in the owner's history.

## Quick start

1. Download `index.html` (or `SmartShopIntelligent.html`).
2. Open it in Chrome, Edge, Firefox or Safari. No installation or build step.
3. Choose **Register your business** and follow the form.
4. Copy your **Business ID**, add inventory, then create cashier accounts.
5. Cashiers open the same file in the same browser and choose **Cashier login**.

To publish it online, host the single file on any static host (GitHub Pages, Netlify, and similar). Remember that data still stays in each visitor's own browser.

## How it works

```
Register business  →  Add shops and inventory  →  Create cashiers
        ↓
Cashier logs in (Business ID + password)
        ↓
New transaction → find items → customer name and phone → choose status → print
        ↓
Sale appears in the owner's history under Paid, Partial or Credit
```

## Tech

- One self-contained `index.html`: plain HTML, CSS and vanilla JavaScript. No framework, no build tooling.
- Storage: the browser's `localStorage`, with keys prefixed `ssi:` (businesses, per-business data, uploaded logo). Each business's data is stored separately under its own ID.
- Excel export uses [SheetJS](https://sheetjs.com/) (`xlsx@0.18.5`) loaded from cdnjs. CSV export needs no external library.
- Printing uses the browser's print dialog, so receipts can also be saved as PDF.

## Project structure

```
.
├── index.html     the whole application
└── README.md
```

## Limitations

- **Data lives on one device.** Records are saved in the browser where the app is used. A second phone or computer will not see them, and clearing browser data erases them. Use **Export Data** weekly and keep copies outside the device.
- **No import or restore** feature yet.
- **Stock is not reduced automatically** when a sale is made. The owner updates quantities in Inventory.
- **Finished sales cannot be edited or voided.**
- **Excel (.xlsx) export** needs internet the first time to load the library. CSV works offline. Downloads may not work inside embedded previews; open the file in a normal browser tab.
- Not designed for several staff to work on the same records from different devices.

## Security notes

This app is built for convenience on a trusted shop device. It is not bank-grade security.

- Passwords are stored as **plain text** in browser storage. Cashier passwords are shown to the owner on purpose.
- There is **no login lockout**, so repeated guessing is not blocked.
- Anyone who can open the browser's developer tools on the device can read stored data.
- Exports contain customer names, phone numbers and balances. Treat them as personal data.

Recommended practice: lock the device, give cashiers their own device or browser profile, use a long unique owner password, write the recovery answer down somewhere safe, log out after every shift, and review the history daily.

## Roadmap

- [ ] Hash owner and cashier passwords
- [ ] Lock logins after repeated wrong attempts
- [ ] Reduce stock automatically on each sale, with low-stock warnings
- [ ] Void and refund with a reason, plus an audit log of cancelled sales
- [ ] Backup and restore to a single file
- [ ] Online version with real accounts that sync across phones and shops

## Contributing

Issues and pull requests are welcome. Because the whole app is one file, keep changes focused, test the owner and cashier flows in a browser, and avoid adding build tooling.

## License

Add the license of your choice here (for example MIT) and include a `LICENSE` file in the repository.

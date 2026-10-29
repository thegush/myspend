# MySpend — iPhone Expense Tracker (Starter)

A local-first, mobile-friendly expense tracker built as a Progressive Web App (PWA).

## Included
- Add/edit/delete expenses
- Categories, merchant, date, payer, payment method, notes
- Receipt photo attachment (manual total entry; no OCR yet)
- Monthly dashboard and budget
- Search/filter transaction history
- Month-by-month reports
- JSON export/import including receipt images
- Local browser storage using IndexedDB
- Basic offline cache after first successful load on an HTTPS host

## Important sharing limitation
This version does not automatically synchronize two phones. To share:
1. On the phone with the latest ledger, open Reports → Export backup.
2. Send the JSON file privately (AirDrop is convenient for nearby Apple devices).
3. On the other phone, open MySpend → Reports → Import backup.
4. Import merges transactions by ID, keeping the latest version when the same transaction exists on both devices.

Backups merge transactions by stable IDs, but this is not live sync. If the same transaction is edited independently on both phones, the most recently updated copy wins.

## How to use it on an iPhone
The app needs to be served over HTTPS for reliable PWA installation and offline service-worker support. Do not simply open the HTML as a file if you want an installable PWA.

1. Upload `index.html`, `manifest.json`, and `sw.js` to an HTTPS static host you control.
2. Open the HTTPS URL in Safari on the iPhone.
3. Tap Share → Add to Home Screen.
4. Launch MySpend from the Home Screen.
5. Set the budget and names under Settings.
6. Export a JSON backup regularly and keep it somewhere private.

A static host serves the app files; expense records remain in the browser's local IndexedDB and are not sent to the host by this app.

## Run locally for development
From this folder, run a local static server, for example:
`python3 -m http.server 8000`
Then open `http://localhost:8000`. For an iPhone, use an HTTPS host instead of plain HTTP.

## Known limitations / next improvements
- No automatic bank import
- Receipt images are attached, but OCR is not implemented
- No automatic synchronization or conflict-aware merge
- Local browser data may be cleared; backups are essential
- Browser storage is not encrypted by this app
- Currency is currently EUR
- Category list is currently fixed in the code

## Suggested next milestones
1. Add OCR receipt parsing and user confirmation.
2. Add safe merge import using stable transaction IDs.
3. Add recurring expenses and category-specific budgets.
4. Add optional encrypted sync if you later want both phones updated automatically.

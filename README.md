# 🍷 Stuarts Premier Daily — Wine Shop

A single-file HTML web storefront for **Stuarts Premier Daily**, a fine wines & spirits shop in Stowmarket, Suffolk. The entire site — storefront, cart, checkout, admin panel, and order history — runs from one `.html` file with no server, no database, and no dependencies to install.

---

## 📁 File Structure

```
stuarts_wine_shop_final.html   ← The entire site (open this in a browser)
Wine Images/                   ← Product images folder (must sit alongside the HTML file)
  casillero-del-diablo-merlot.jpeg
  trivento-reserve-malbec.jpeg
  prosecco-vino-spumante.jpeg
  ... (one image per wine)
README.md                      ← This file
```

> ⚠️ The `Wine Images/` folder must be in the **same directory** as the HTML file, otherwise wine photos will fall back to emoji placeholders.

---

## 🚀 Getting Started

1. Place `stuarts_wine_shop_final.html` and the `Wine Images/` folder in the same directory.
2. Open `stuarts_wine_shop_final.html` in any modern browser (Chrome, Firefox, Edge, Safari).
3. No installation, build step, or internet connection required for core functionality.

> External fonts (Google Fonts) and the PDF library (html2pdf.js) load from CDN — an internet connection is needed for these to render correctly.

---

## 🛍️ Customer Features

### Storefront
- Browse **20 wines** across Red, White, Rosé, and Sparkling categories
- Filter by type and sort by price or vintage
- Search by wine name, grape, or region
- Paginated grid — 8 wines per page
- Click any wine card to open a full detail modal with tasting notes, serving temperature, ABV, and ratings
- Sale badge shown on discounted wines

### Cart & Checkout
- Add/remove items, adjust quantities from the cart drawer
- Real-time cart total with item count badge
- Checkout form with full **UK validation**:
  - Phone: must match a valid UK format (07xxx xxxxxx, +44, landlines)
  - Postcode: must be a valid UK postcode (e.g. `IP14 1AA`)
  - Address Line 1: must contain a house/flat number
  - Town/City: letters only
  - Name fields: letters, hyphens, apostrophes only
  - Email: standard format check
- Inline field-level error messages (not generic alerts)
- Age confirmation checkbox (18+, Challenge 25 policy)
- Terms & Conditions checkbox (separate from age check)
- **Payment method: Cash on Delivery only**

### Order Confirmation
- Full-page confirmation shown after a successful order
- Unique order number generated per order (format: `SPD-XXXXXX`)
- Shareable URL — the page URL updates to `#order=SPD-XXXXXX`; anyone with the link can view the confirmation
- Order details persisted to localStorage for URL recovery
- Download confirmation as a PDF
- Receipt modal also available via the admin panel

---

## 🔐 Admin Panel

### Accessing Admin Mode
Click the **lock icon** (🔒) in the bottom-right corner of the page.

| Field    | Value      |
|----------|------------|
| Username | `stuarts`  |
| Password | `admin1234`|

> ⚠️ Change these credentials before deploying publicly. They are stored in plain text in the HTML file — search for `ADMIN_USER` and `ADMIN_PASS`.

### Admin Features
- **Stock Manager** — update stock levels for each wine, mark items as out of stock
- **Sales History** — view all orders placed in the current browser session with order number, date, customer, items, and total
- **Low stock alerts** — wines with 2 or fewer units show a warning badge
- **Admin bar** — shown at the top of the page when logged in, with quick stats

---

## 🍪 Cookie Consent

A GDPR-compliant cookie consent banner appears on first visit. The user's choice (Accept / Decline) is saved to `localStorage` under the key `stuarts_cookie_consent` and the banner will not appear again on future visits or page refreshes.

To reset consent during testing: open browser DevTools → Application → Local Storage → delete the `stuarts_cookie_consent` key.

---

## 📋 Terms & Conditions

A full Terms & Conditions modal is accessible:
- From the cookie banner ("Cookie & Privacy Policy" link)
- From the checkout form ("Terms & Conditions" link)

Covers: age policy, payment, delivery, cancellations, pricing, responsible drinking, privacy, and contact details.

---

## 💾 Data Storage

All data is stored in the browser's `localStorage` — nothing is sent to a server.

| Key | Contents |
|-----|----------|
| `stuarts_cookie_consent` | `"accepted"` or `"declined"` |
| `stuarts_stock` | Stock levels per wine (JSON) |
| `stuarts_sales_history` | Array of all orders placed (JSON) |
| `stuarts_order_SPD-XXXXXX` | Individual order details for shareable URL recovery |

> Data is **per-browser** and **per-device**. Clearing browser storage will reset stock levels and order history.

---

## 📄 PDF Downloads

Two PDF download options are available, both powered by [html2pdf.js](https://github.com/eKoopmans/html2pdf.js) (loaded via CDN):

- **Receipt PDF** — downloadable from the receipt modal after an order, named `stuarts-receipt-SPD-XXXXXX.pdf`
- **Order Confirmation PDF** — downloadable from the confirmation page, named `stuarts-order-SPD-XXXXXX.pdf`

---

## 🎨 Design

| Detail | Value |
|--------|-------|
| Primary colour | `#4c0743` (deep purple) |
| Accent colour | `#f5a800` (gold/yellow) |
| Heading font | Cormorant Garamond (Google Fonts) |
| Body font | Jost (Google Fonts) |

---

## 🛠️ Customisation

### Adding or editing wines
Find the `const wines = [...]` array in the `<script>` section. Each wine object looks like:

```js
{
  name: "Casillero del Diablo Merlot",
  region: "Central Valley, Chile",
  vintage: 2022,
  type: "Red",                        // Red | White | Rosé | Sparkling
  price: "£9.99",
  priceNum: 9.99,
  rating: 4,                          // 1–5
  grape: "Merlot",
  abv: "13.5%",
  serve: "16–18 °C",
  emoji: "🍷",                        // fallback if image not found
  sale: false,                        // true shows a SALE badge
  img: "Wine Images/filename.jpeg",
  desc: "Tasting notes here."
}
```

### Changing admin credentials
Search for `ADMIN_USER` and `ADMIN_PASS` in the script section and update the values.

### Changing contact details
- **Phone number**: search for `01449 612259`
- **Address**: search for `Stowmarket` or `IP14 5AU`
- **Google Maps link**: search for the `maps/dir` URL in the nav

---

## 📞 Contact

**Stuarts Premier Daily**
2 Creeting Rd W, Stowmarket, IP14 5AU
☎ 01449 612259

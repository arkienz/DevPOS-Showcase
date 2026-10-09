# DevPOS: Point of Sale for Philippine Cafes

**An offline-first POS system for small coffee shops and cafes in the Philippines.**
It runs on Android tablets and Windows PCs from a single C# codebase.

> The source code is private because this is a commercial product. I'm happy to give
> reviewers read access or walk through the code on a call, so feel free to reach out.

---

## Why I built it

Small cafes in the Philippines need a POS that keeps working when the internet drops,
handles local rules like the 12% VAT, Senior Citizen/PWD discounts, and BIR receipt
wording, and runs on an affordable Android tablet. DevPOS is built for that. Every sale,
receipt, and report works with no internet at all.

## Features

### Selling
- Fast order screen with menu photos, categories, add-ons, and combo/meal sets
- Dine-in, take-out, and delivery orders, with table tracking and daily order numbers
- Split bills evenly, by item, or by amount, with mixed Cash / GCash / QR Ph payments
- **QR Ph payments** through PayMongo, with automatic payment confirmation
- Senior Citizen/PWD discounts, promos (including Buy X Take Y), manager discounts, and a loyalty points program
- Service charge (RA 11360) with automatic staff share calculation
- Voids and partial refunds, protected by an Owner PIN

### Printing and kitchen
- Receipts on 58mm ESC/POS thermal printers over **Bluetooth or USB**, with no driver needed
- BIR-aware receipt wording (Order Slip vs. Sales Invoice, EOPT Act)
- Separate bar and kitchen tickets, routed by item category
- **Kitchen and bar display screens over shop Wi-Fi**: a tablet or phone pairs with the
  counter using a 6-digit code and shows live orders over an encrypted connection

### Inventory and costs
- Ingredient-level stock that is deducted automatically on every sale, including add-ons,
  and returned on voids and refunds
- Recipe costing with suggested selling prices, based on profit after VAT
- Receiving, waste logging, stock counts, and full stock history
- Suppliers and a smart **reorder list** based on recent usage and delivery lead times
- Daily expenses, monthly fixed costs, and a **break-even** target per day

### Reports and management
- Customizable dashboard with drag-and-resize tiles, period comparisons, and sales trends
- X-Reading and Z-Reading (end-of-day), shift open/close with cash over/short
- Item profit reports, per-item sales goals, and delivery app commission tracking
- Staff profiles with performance stats and estimated pay
- In-app notification center for low stock, failed prints, voids, and late QR payments

### Security and data
- Offline-first: no internet needed for any core action
- Database encrypted on the device (AES-256, key stored in the OS secure storage)
- Password-protected encrypted backups and restore
- PIN keypad with guess limits and automatic re-lock
- Dark mode, adjustable text size, custom colors, and a dedicated phone layout

## Tech stack

| Area | Technology |
|---|---|
| App framework | .NET 10 MAUI Blazor Hybrid (C#, Razor components) |
| Platforms | Android, Windows |
| Database | SQLite with SQLite3 Multiple Ciphers encryption |
| UI | Blazor, Bootstrap 5.3, custom components |
| Payments | PayMongo API (QR Ph) |
| Printing | ESC/POS over Bluetooth SPP and raw USB |
| Networking | TCP/UDP discovery, ECDH key exchange, AES-256-GCM |
| Testing | xUnit, with tests for core business logic and the SQLite layer |
| Development | Visual Studio, GitHub, AI-assisted development with Claude Code |

## How it's built

- **Layered design:** business logic lives in a separate `Core` library with no UI
  code, so it can be tested on its own and reused later for a cloud sync service.
- **Dependency injection** throughout, with the data layer behind interfaces.
- **One source of truth for money:** shared helpers handle totals, VAT, refunds, and
  payment breakdowns, so every screen and report agrees.
- **A sale never fails because of a side task:** printer errors, stock issues, or
  notification problems are reported, never allowed to block checkout.

## About me

I'm **Mark Angelo Pasion**, a Senior Software Engineer from Malolos, Bulacan, with 10+
years of experience in C#, VB.NET, SQL Server, and SAP Business One integration.
DevPOS is one of my own products, designed and built end to end.

- GitHub: [@arkienz](https://github.com/arkienz)

# VELCÉRIA Store — Owner Guide

## Customer storefront
The customer-facing store is published separately from this private manager. Keep the two repositories separate.

## Sign in to the manager
Open the private Store Manager site and sign in with the existing owner account. Access is checked against the `store_admins` table; knowing the URL alone does not grant access.

## Add a product
1. Open **Products → Add product**.
2. Enter the product name, department/category, price and a clear description.
3. Upload a real photo of the exact item being sold (JPG, PNG, WebP or AVIF; up to 5 MB), or provide an HTTPS image URL.
4. Enter stock quantities for the available sizes. A product without an in-stock variant cannot be added to the bag.
5. Save, then confirm it appears on the customer storefront.

Use original product photos for sale listings. Do not use editorial campaign images as if they were photographs of stock customers will receive.

## Orders and delivery
- Checkout currently accepts **Cash on Delivery**.
- Orders in a configured delivery zone receive the saved delivery fee.
- Orders outside configured zones are still accepted and marked **Needs confirmation**. Contact the customer before confirming the delivery arrangement.
- In **Orders**, update the delivery state after the arrangement is confirmed. Update the order status as fulfilment progresses.
- Stock is reserved/decremented by the database checkout function; do not manually decrement stock again for the same order.

## Configure delivery zones
Open **Store settings → Delivery zones (JSON)**. Add one object per delivery area. Region and city matching is case-insensitive; city names must match the customer's city/town field.

Example:
```json
[
  {
    "name": "Accra Central",
    "region": "Greater Accra",
    "cities": ["Accra", "Osu", "Labone"],
    "fee": 25,
    "enabled": true
  },
  {
    "name": "Tema",
    "region": "Greater Accra",
    "cities": ["Tema"],
    "fee": 35,
    "enabled": true
  }
]
```

Replace example amounts and areas with the actual delivery rates before accepting orders. An empty list intentionally sends every order to manual delivery confirmation.

## Rebrand the store
In **Store settings**, change the business name, logo URL, tagline, primary/accent colours, homepage headline and introduction, currency, contact details and delivery zones. Logo URLs should point to a public square SVG or PNG. The storefront and manager read the same store settings.

## Payment configuration
Cash on Delivery is the only payment method currently wired into checkout. Other payment options must not be enabled until a real payment provider, callback verification and order reconciliation are implemented.

## Important before selling this system to another boutique
This installation is a **single-store deployment**, not a shared multi-tenant SaaS. For each new boutique, create a separate Supabase project and owner account, apply the database schema/functions, configure its storage bucket and RLS policies, and point that boutique's storefront and manager at its own project. Never give another boutique access to this store's Supabase project or database.

## Before going live
- Replace demo/editorial content with the boutique's real contact details and policies.
- Add real products, accurate prices, photos and stock.
- Configure actual delivery zones and fees.
- Test one low-risk end-to-end order with the owner before public promotion.
- Confirm the store's name and logo are available for commercial use before launch.

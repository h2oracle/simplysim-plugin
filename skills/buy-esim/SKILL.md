---
name: buy-esim
description: Help the user choose and buy a SimplySIM travel data eSIM for a trip, ending with a secure Stripe payment link. Use when the user wants mobile data abroad, a travel eSIM, a roaming alternative, or asks about SimplySIM plans, prices or coverage for a country or region.
---

# Buy a SimplySIM travel eSIM

Use the `simplysim` MCP tools. Never guess plan ids, prices or answers; read them from the tools or ask the user.

## Flow

1. **Destination.** Ask where they are travelling if not stated, then call `search_destinations`. For multi-country trips, consider regional plans (for example Europe).
2. **Plans.** Call `get_plans` with the destination slug and currency (GBP or EUR). Ask how long the trip is and roughly how much data they use, then recommend two or three plans with price, data, validity and coverage. Mention that plans are data-only (no calls or SMS) and that hotspot sharing is allowed.
3. **Basket.** Call `create_basket`, then `add_to_basket` with the chosen `plan_id`. Keep the `basket_token` private and reuse it for every basket call.
4. **Codes.** If the user has a promo or referral code, call `apply_code`. Do not try codes the user did not give you.
5. **Checkout questions.** Ask the user, and wait for real answers:
   - Is the trip for **leisure or business**?
   - What **date** do they need the eSIM from?
   - Which **phone** will they use? Call `check_device` with their answer and confirm the matching model with them. Remind them the phone must be eSIM-capable and network-unlocked.
6. **Payment link.** Call `get_checkout_link` with the answers and `device_compatible: true` once the user has confirmed. Give the user the `checkout_url`. They pay on Stripe in their own browser and enter their own email there; the eSIM and installation steps are emailed to them.
7. **Follow up.** If asked, call `get_order_status` with the same `basket_token`.

## Rules

- Show prices exactly as returned, including currency. Prices include VAT; any code discount is confirmed on the Stripe page.
- Never ask for or handle card details. Payment only happens on the Stripe page.
- Never invent device compatibility. If `check_device` finds no match, tell the user and ask them to check their phone's settings for an eSIM option before continuing.
- If a tool returns an error, explain it plainly and offer the next step.

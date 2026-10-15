# SimplySIM Travel eSIMs

Find and buy prepaid travel data eSIMs for 190+ countries from [SimplySIM](https://simplysim.co.uk), a UK travel eSIM provider (SIMPLYSIM SOLUTIONS LTD, Companies House 16302568). Claude can search destinations, compare plans, build a basket, apply a promo code and hand you a secure Stripe payment link. Your eSIM and installation instructions are emailed to you after payment.

## What's included

- **MCP server** `simplysim` at `https://simplysim.co.uk/mcp` (remote, Streamable HTTP, no login needed).
- **Skill** `buy-esim`, which guides Claude through choosing a plan and checking out.

### Tools

| Tool | What it does |
|---|---|
| `search_destinations` | Find a country or region by name |
| `get_plans` / `get_plan` | List and inspect data plans with prices, validity and networks |
| `create_basket` | Start an anonymous basket and get a private basket token |
| `add_to_basket` / `remove_from_basket` / `get_basket` | Manage the basket |
| `apply_code` / `remove_code` | Apply or remove a promo or referral code |
| `check_device` | Check a phone model against the eSIM compatibility list |
| `get_checkout_link` | Save the trip details and create a Stripe payment link |
| `get_order_status` | Check whether the order has been paid and delivered |

## Install

**Claude Code**

```
claude plugin marketplace add h2oracle/simplysim-plugin
claude plugin install simplysim-esim@simplysim-marketplace
```

Then ask: "Find me a Spain eSIM for a week and give me a payment link."

**Claude apps (chat and Cowork):** install from the plugin directory, then connect the SimplySIM connector from the plugin's Connectors tab.

## Data handling

- The plugin sends requests only to `https://simplysim.co.uk/mcp`.
- To create an order it sends the plans you choose, any promo code you give, your trip purpose (leisure or business), the date you need the eSIM from and your phone model. These are stored on the order to provision and support your eSIM.
- It does not collect your name, email or card details. You enter those only on Stripe's payment page; Stripe processes the payment.
- Baskets are anonymous and expire after 24 hours without use. Requests are rate-limited per IP address, and the caller's IP address and user agent are stored with the basket for fraud prevention.
- Paid orders are kept for accounting and tax records as described in the privacy policy.
- Full details: [Privacy policy](https://simplysim.co.uk/support/privacy-policy) and [Terms](https://simplysim.co.uk/support/terms-and-conditions).

## Support

[simplysim.co.uk/support/contact-us](https://simplysim.co.uk/support/contact-us) or hello@simplysim.co.uk.

## License

MIT

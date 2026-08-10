# Public disclosure guidelines

This repository is public. The Createhers application is private. These are
the rules for anything added here — including screenshots, documentation
updates, and diagrams.

**The test:** could a reader use this to recreate the system, attack it, or
learn something about a customer? If yes, it doesn't go in.

---

## Safe to publish

- Screenshots of public-facing experiences (pages any visitor can reach)
- High-level descriptions of product capabilities
- UX and product decisions, and the reasoning behind them
- Design-system documentation — type, color, layout, components, patterns
- Problem → decision → outcome narratives
- General technology stack, at the level of named frameworks
- Sanitized conceptual diagrams showing boundaries, not internals
- Accessibility decisions and standards met
- Responsive-design decisions
- Sample or fictional data, clearly labeled as such

---

## Do not publish

- Secrets, credentials, API keys, tokens, or environment configuration
- Customer, client, subscriber, or order data — including in screenshots
- Production database contents, structure, or file locations
- Private application source code, in whole or in excerpt
- Exact internal routes, admin paths, webhook endpoints, or private APIs
- Security implementations — authentication, verification, or token design
- Anti-abuse techniques, thresholds, or detection heuristics
- Proprietary algorithms or generation logic
- Detailed business rules — pricing logic, fulfillment, access, lifecycle
- Operational automations and internal workflow specifics
- Infrastructure internals — hosting configuration, storage, deployment
  mechanics, persistence behavior
- Payment fulfillment or dispute-handling mechanics
- Screenshots of authenticated surfaces, including navigation that reveals
  the product's structure

---

## Screenshot checklist

Before adding an image, confirm:

1. It shows a page a member of the public can already visit.
2. No real customer names, emails, tokens, or record identifiers appear.
3. No authenticated navigation, menus, or internal labels are visible.
4. Any sample content is clearly fictional and labeled.
5. No browser chrome exposing internal URLs.

---

## Writing checklist

When describing something technical, describe the **outcome and intent**,
not the mechanism.

| Instead of | Write |
|---|---|
| The specific verification algorithm, window, and comparison method | "Payment workflows use secure server-side verification with idempotent fulfillment" |
| Database engine internals, journaling, and migration behavior | "The persistence layer supports reliable state and safe schema evolution" |
| The specific anti-abuse techniques and thresholds | "Public forms include layered abuse prevention and validation" |
| Exact route paths and endpoints | "Public surfaces and an authenticated operations area" |
| Cache durations, retry counts, failure branches | "Integrations degrade gracefully when a service is unavailable" |

---

## If something sensitive is committed by mistake

Deleting the file in a new commit does **not** remove it — it stays in git
history and remains retrievable. Treat any exposed secret as compromised:
rotate it first, then rewrite history (or recreate the repository) before
assuming it is gone.

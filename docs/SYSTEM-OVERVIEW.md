# System overview

How the platform is organized, at the level of product surfaces and system
boundaries. Implementation details, security mechanisms, data architecture,
and operational workflows are intentionally omitted — see
[Public disclosure guidelines](PUBLIC-DISCLOSURE-GUIDELINES.md).

---

## Product surfaces

The platform is one application serving two distinct experiences.

**Public** — marketing and brand, commerce and checkout, a course
classroom, gated resources and lead tools, a free creator tool, and
standalone offer pages authored by the business.

**Authenticated operations** — the studio's working software: relationship
and project records, scheduling, inquiry pipelines, audience management,
campaigns, commerce administration, and content management.

They share a database, a design system, and a rendering model. They differ
in density, tone, and pacing, because their users are doing opposite kinds
of work.

---

## Conceptual boundaries

```
                      ┌─────────────────────────┐
   Visitors  ───────► │  Public experiences     │
                      │  marketing · commerce   │
                      │  learning · tools       │
                      └───────────┬─────────────┘
                                  │  shared design system
                                  │  shared content + records
                      ┌───────────┴─────────────┐
   Operator  ───────► │  Authenticated          │
   (studio)           │  operations             │
                      └───────────┬─────────────┘
                                  │
                      ┌───────────┴─────────────┐
                      │  External integrations  │
                      │  payments · email       │
                      │  calendar (read-only)   │
                      └─────────────────────────┘
```

Three boundaries matter in this system:

1. **Public vs. authenticated.** Everything the operator can do is behind a
   single authentication boundary; nothing operational is reachable from a
   public surface.
2. **Content vs. code.** What the business publishes is data, not markup.
   Adding an offer, a course, an article, or a landing page is an authoring
   task, not a deployment.
3. **Owned vs. integrated.** Payments, email delivery, and calendar are
   external services with narrow, well-defined contracts. Everything else —
   records, content, learning, tools — lives in the platform.

---

## Major integrations

| Integration | Direction | Purpose |
|---|---|---|
| Payments | Two-way | Hosted checkout for services, courses, and digital products; confirmed server-side before access is granted |
| Email | Outbound | Transactional confirmations and audience campaigns, sharing one branded template system |
| Calendar | Read-only, inbound | External schedule surfaced alongside internal events |

Each integration is designed to fail without taking the product with it:
customer-facing actions complete even when a downstream service is
unavailable, and anything time-sensitive is reconciled rather than lost.

---

## High-level data relationships

The model is deliberately small and relational. At a conceptual level:

- **People** — the audience, and the subset who become clients
- **Work** — projects and their lifecycle, tied to people
- **Commerce** — products and the orders placed against them
- **Learning** — courses, their structure, and per-learner progress
- **Content** — everything the public site renders, authored not deployed
- **Signals** — inquiries, bookings, and audience activity

Relationships between these are what make the operations views useful: a
person's inquiries, purchases, projects, and learning are one view, not
five tools.

---

## Design principles

**One system, two registers.** Shared foundations expressed differently for
persuasion and for operation.

**Every page has one job.** A primary action per surface, with secondary
paths subordinate rather than competing.

**The interface carries the process.** Stateful workflows surface what needs
attention; the operator should not have to remember a procedure.

**Publish without deploying.** If the business needs engineering to say
something new, the design is wrong.

**Content is designed.** Copy, terms, empty states, and error messages are
part of the product, written with the same care as the layout.

---

## Accessibility principles

- Semantic structure and correct heading order on every surface
- Visible focus states; all interactive components keyboard-operable
- Contrast pairings documented with the color tokens, including which
  combinations are approved for small text
- `prefers-reduced-motion` honored throughout
- Forms usable without client-side JavaScript
- Wide content scrolls within its own container; the page never scrolls
  sideways
- Alternative text treated as content, not as a checkbox

---

## Scalability considerations

The platform is sized honestly for what it is: software for a studio, not a
multi-tenant SaaS. That framing is a design decision, and it is what keeps
the system comprehensible to one maintainer.

Where growth was anticipated:

- **Content model over hardcoding**, so new offers and pages cost authoring
  time rather than engineering time
- **A component vocabulary** small enough to hold in your head and reused
  across both experiences
- **Clear integration seams**, so an external service can be swapped without
  touching product logic
- **Room to migrate.** The persistence approach suits current scale; the
  boundaries are drawn so it can change without redesigning the product

---

*For anything below this level of detail — architecture, security, data
design, and operational workflow — a private walkthrough can be arranged
during hiring conversations.*

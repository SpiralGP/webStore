# SpiralShop architecture and course mapping

## New source-of-truth boundary
SpiralShop remains the private reusable package product. webStore is a separate educational application and local read-only reference when developing SpiralShop. It is NOT the package development/demo host. The existing SpiralShop application remains that host unless explicitly changed later.

Do not replace SpiralShop's roadmap with the course contents. Use the course sequence as feature-learning milestones; it is not a package architecture or a complete release checklist. Existing documents need a small amendment to move course work out of the product repository, not a rewrite or database reset.

## Rough phases

| Learning milestone | Episodes | Learning exit criterion | Product application |
|---|---|---|---|
| Scaffolding | 1–4 | Bootable app and repeatable catalogue sample data | Package models/factories later; host auth remains separate |
| Storefront and carts | 5–18 | Product browsing and persistent guest/customer cart work | Core cart actions and merge rules; themeable views |
| Payments | 19–26 | Test-mode checkout and verified payment notification work | PaymentProvider + native stripe-php; no package Cashier dependency |
| Order experience | 27–32 | Secure order views and local confirmation mail | Snapshots, access control and transactional notifications |
| Supplementary modernisation | 33 | Understand Livewire changes and search/pagination | Optional frontend choice; do not replay obsolete upgrades |
| Package-only release work | Outside course | Independently installable, tested second-host shop | Administration, stock reservations, manual tax, shipping, refunds and release docs |

## Agreed product direction carried forward
- Local package path: /home/SpiralGP/projects/modules/spiralShop.
- Composer name: spiralcorp/spiral-shop; namespace: SpiralCorp\SpiralShop.
- Guest checkout; database carts; explicit idempotent merge rules.
- Physical products/variants; one currency; no speculative multi-store layer.
- Integer minor-unit persistence and currency codes; brick/money calculations.
- Native Stripe integration behind PaymentProvider, not Cashier.
- Manual tax configuration; course automatic Stripe Tax is a deliberate divergence.
- Time-limited checkout stock reservations, reconciliation and late-payment review.
- Minimal scoped CSS, overridable Blade presentation, isolated optional Filament integration.
- Initial product support target: PHP 8.5 and Laravel 13, tested independently.
- No Jetstream requirement in the product package.

## Proposed logical boundaries
Core: Catalogue, Pricing, Cart, Checkout, Orders, Inventory.
Integrations: Payments/Stripe, Filament admin, mail/storage adapters as needed.
Presentation: Storefront views/components and scoped stylesheet.
Host: authentication, business identity, legal policies, infrastructure configuration.

UI components call commerce actions; payment events reconcile state; historical orders use snapshots rather than live catalogue values. Course application code is reference material, not an automatic package dependency.

## Reference workflow
1. Complete each lesson in webStore.
2. Note installed versions, deviations and observed behaviour.
3. Add focused regression tests where useful.
4. Consult the local course repo when implementing an approved SpiralShop task.
5. Transfer concepts selectively, preserve source attribution and check reuse terms before copying source wholesale.
6. Validate the package in an independent host before release.

Suggested course-notes table:
Episode | Completed | Version difference | Observed behaviour | Test | Product mapping

## Course gaps: independent release checklist
- Payment status separate from order/fulfilment status.
- Signature verification, retries, idempotency and paid-state validation.
- Stock concurrency, reservation expiry, reconciliation, late-payment recovery.
- Cart versioning: do not clear items added after checkout started.
- Admin access control; customer and guest order authorisation.
- Price/tax/shipping revalidation; explicit supported destinations and rounding.
- Refund workflow, historical snapshots, error handling and audit trail.
- Scoped styling, publishable views, package tests and second-host install.
- Backups, queues, scheduler, secrets and deployment documentation.
- Legal/privacy/accessibility review for the actual merchant and jurisdiction.
- Abandoned-cart marketing remains off by default until separately reviewed.

## Documentation amendment instruction for Devin
In SpiralShop, update the existing five planning documents only to reflect the separate reference repository and this feature mapping. Preserve existing agreed architecture and decision IDs. Do not recreate the environment, remove Jetstream/Cashier, extract a package or change dependencies as a side effect. Those changes need a later explicit task. No automatic commits, amendments or push.

## Evidence limits
All provided URLs were inspected. Detailed substep labels were available only for episodes 1–4; later pages exposed subscriber metadata only. The episode register distinguishes verified labels from proposed tasks. Fill remaining chapter details from authorised viewing notes instead of inventing them.

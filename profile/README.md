# c975L

Open-source Symfony bundles for building websites — a shared EasyAdmin back-office, database-backed
configuration, composable page blocks, e-commerce and more, each bundle usable on its own but designed
to plug into the others.

Maintained by [Laurent Marquet](https://github.com/LaurentMarquet) · PHP 8.4 · Symfony 8 · EasyAdmin 5 · MIT

## The core

| | Package | What it does |
|---|---|---|
| <img src="images/CoreBundle.svg" alt="" width="110"> | [CoreBundle](https://github.com/975L/CoreBundle) <br> `c975l/core-bundle` | The base of the ecosystem in a single package. **ConfigBundle** — database-backed application configuration (`site_config`), the shared `/management` dashboard, user accounts, health check, backup, sitemaps, redirects. **UiBundle** — composable page Blocks, media library and site graphics, admin-editable theme, cookie banner, legal documents, database-driven forms, email templates, reviews, ratings and favorites, shared CSS/JS. |

One package, **two bundles**: `c975L\ConfigBundle\` and `c975L\UiBundle\` keep their own namespaces,
services, configs, translation domains and dashboard sections — there is no `c975L\CoreBundle\`
namespace. They referenced each other in both directions and could never be released independently,
so they are now released together. `c975l/config-bundle` and `c975l/ui-bundle` are superseded by this
package; see [CoreBundle's UPGRADE.md](https://github.com/975L/CoreBundle/blob/main/UPGRADE.md) —
no `use`, no `@c975LUi/…` template reference and no `bundles.php` entry changes.

## The bundles

Every bundle below rests on the core, and only on the core (plus PaymentBundle where checkout is
involved). None of them rests on another.

| | Bundle | What it does | Also requires |
|---|---|---|---|
| <img src="images/SiteBundle.svg" alt="" width="80"> | [SiteBundle](https://github.com/975L/SiteBundle) <br> `c975l/site-bundle` | Website foundation — full layout, database-driven pages, navbar and footer menus, collections, per-page SEO and health check | — |
| <img src="images/ShopBundle.svg" alt="" width="80"> | [ShopBundle](https://github.com/975L/ShopBundle) <br> `c975l/shop-bundle` | E-commerce — product catalog with categories, media, downloadable files, gift cards, verified buyer reviews and affinity recommendations | Payment |
| <img src="images/PaymentBundle.svg" alt="" width="80"> | [PaymentBundle](https://github.com/975L/PaymentBundle) <br> `c975l/payment-bundle` | Generic basket/checkout engine and Stripe payments; any bundle plugs its own sellable items in through `BasketItemProviderInterface` | — |
| <img src="images/CrowdfundingBundle.svg" alt="" width="80"> | [CrowdfundingBundle](https://github.com/975L/CrowdfundingBundle) <br> `c975l/crowdfunding-bundle` | Crowdfunding campaigns — counterparts, contributors, news and media — plus an optional lottery tied to a campaign | Payment |
| <img src="images/BookBundle.svg" alt="" width="80"> | [BookBundle](https://github.com/975L/BookBundle) <br> `c975l/book-bundle` | A publisher's catalog of books, series and strips, with media, video, press and marketing collections, short links and reader reviews | — |
| <img src="images/GalleryBundle.svg" alt="" width="80"> | [GalleryBundle](https://github.com/975L/GalleryBundle) <br> `c975l/gallery-bundle` | Photo galleries — categories, batch upload, automatic derivatives, public viewer | — |
| <img src="images/SocialBundle.svg" alt="" width="80"> | [SocialBundle](https://github.com/975L/SocialBundle) <br> `c975l/social-bundle` | Social links managed in one place and share buttons for 15 networks | — |

Installing any of them pulls the core in, so `composer require c975l/site-bundle` is usually all you
need to start.

**A site does not need SiteBundle.** The core plus a shop, a book catalogue or a gallery is a
complete site on its own: it has a page shell, the theme, its favicon and share preview, the cookie
banner, the legal documents, accounts, redirects and the health check. SiteBundle is what adds
*pages* — a composable page tree, menus, collections and their own SEO — not what makes a site work.

## Start here

New to the ecosystem? Read [CoreBundle's README](https://github.com/975L/CoreBundle#readme) first —
it points at the configuration model and the dashboard extension points (`MenuProviderInterface`,
`AlertProviderInterface`, `ShortcutProviderInterface`, `SitemapProviderInterface`…) that every other
bundle plugs into.

Building a website? Start with [SiteBundle](https://github.com/975L/SiteBundle#readme).

Want to see it running? [bundles.975l.com](https://bundles.975l.com) presents every bundle, and its
[block gallery](https://bundles.975l.com/pages/blocks) shows every block kind live.

## Conventions

- Application configuration lives in the database, edited in EasyAdmin — never in `.env`
- A bundle contributes to the dashboard by implementing an interface; no compiler pass to write
- Assets are served through AssetMapper — no npm, no Node, no build step
- Admin controllers live in `Controller/Management/`
- Every bundle is designed to be overridden rather than forked
- A feature belongs to the bundle owning its domain, not to the one that happens to call it

## Archived

Bundles marked archived on this page are no longer maintained. Notably, `ShareButtonsBundle` and
`ContactFormBundle` have been superseded — share buttons moved to
[SocialBundle](https://github.com/975L/SocialBundle), contact forms to the core's database-driven
form system. `PurchaseCreditsBundle` predates the current architecture and is kept for existing
sites only.

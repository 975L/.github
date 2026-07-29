# c975L

Open-source Symfony bundles for building websites — a shared EasyAdmin back-office, database-backed
configuration, composable page blocks, e-commerce and more, each bundle usable on its own but designed
to plug into the others.

Maintained by [Laurent Marquet](https://github.com/LaurentMarquet) · PHP 8 · Symfony 7 · EasyAdmin 5 · MIT

## The bundles

| Bundle | What it does | Requires |
|---|---|---|
| [ConfigBundle](https://github.com/975L/ConfigBundle) <br> `c975l/config-bundle` | Database-backed application configuration (`site_config`), the shared `/management` dashboard, health check, backup, sitemaps | UiBundle |
| [UiBundle](https://github.com/975L/UiBundle) <br> `c975l/ui-bundle` | Composable page Blocks, media library, database-driven forms, email templates, shared CSS/JS | ConfigBundle |
| [SiteBundle](https://github.com/975L/SiteBundle) <br> `c975l/site-bundle` | Website foundation — layout, pages, SEO, menus, users, legal pages | Config, Ui, Social |
| [ShopBundle](https://github.com/975L/ShopBundle) <br> `c975l/shop-bundle` | E-commerce — product catalog, checkout | Config, Ui, Payment |
| [PaymentBundle](https://github.com/975L/PaymentBundle) <br> `c975l/payment-bundle` | Generic basket/checkout engine and Stripe payments | Config, Ui |
| [BookBundle](https://github.com/975L/BookBundle) <br> `c975l/book-bundle` | Books and series catalog for a publishing site | Config, Ui |
| [GalleryBundle](https://github.com/975L/GalleryBundle) <br> `c975l/gallery-bundle` | Photo galleries — categories, batch upload, derivatives | Config, Ui |
| [SocialBundle](https://github.com/975L/SocialBundle) <br> `c975l/social-bundle` | Social links and share buttons | Config, Ui |

**ConfigBundle and UiBundle are the core pair** — they reference each other and are always installed
together. Every other bundle sits on top of them. Installing any satellite bundle pulls the core in,
so `composer require c975l/site-bundle` is usually all you need to start.

## Start here

New to the ecosystem? Read [ConfigBundle's README](https://github.com/975L/ConfigBundle#readme) first —
it documents the configuration model and the dashboard extension points (`MenuProviderInterface`,
`AlertProviderInterface`, `ShortcutProviderInterface`, `SitemapProviderInterface`…) that every other
bundle plugs into.

Building a website? Start with [SiteBundle](https://github.com/975L/SiteBundle#readme).

## Conventions

- Application configuration lives in the database, edited in EasyAdmin — never in `.env`
- A bundle contributes to the dashboard by implementing an interface; no compiler pass to write
- Assets are served through AssetMapper — no npm, no Node, no build step
- Admin controllers live in `Controller/Management/`
- Every bundle is designed to be overridden rather than forked

## Archived

Bundles marked archived on this page are no longer maintained. Notably, `ShareButtonsBundle` and
`ContactFormBundle` have been superseded — share buttons moved to
[SocialBundle](https://github.com/975L/SocialBundle), contact forms to UiBundle's database-driven
form system.

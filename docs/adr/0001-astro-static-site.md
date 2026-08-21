# ADR-0001: Astro static site, payments stay external

Date: 2026-08-21
Status: accepted

## Context

We need an event landing page cloning the structure of the Eventzilla Startup
Weekend Skopje page. Originally styled with the Startup Club Skopje palette
(`#0E766D` / `#E86E24`, Roboto); superseded 2026-08 by the official Techstars
brand palette (Phosphor `#39C463`, Slate `#8298AB`, black/white) with a
Helvetica Neue system font stack. It starts as a
single page with stubbed tickets and coming-soon speakers/sponsors, but must
scale as sections and real content are added. Hosting is Hostinger. Billing
will be a redirect to an external Payment Provider — Eventzilla or CaSys
(CPAY) — never an on-site checkout.

Alternatives considered:

- **Next.js** — full app framework. Rejected: needs a Node server (Hostinger
  VPS) for capabilities we don't use; the site is content, not an app.
- **Plain HTML/CSS** — rejected: speaker/sponsor lists become copy-paste
  maintenance as content grows.
- **WordPress + Elementor** (what startupclubskopje.com uses) — rejected:
  hosting/plugin upkeep, no version control of content, slow pages.

## Decision

Astro + Tailwind CSS, fully static output (`astro build` → plain HTML/CSS).
Speakers, sponsors, agenda live as data files (JSON/content collections), so
adding content is a data edit, not a layout edit. Deployed as static files to
Hostinger shared hosting.

Payments: the Buy Tickets button redirects out.
- Eventzilla: a plain link, zero backend.
- CaSys/CPAY: requires a server-side signed POST (merchant secret must not be
  in browser JS). If chosen, a single small PHP signing endpoint is added
  next to the static files — Hostinger shared hosting runs PHP, so this does
  not force a VPS or a framework change.

## Consequences

- Cheapest Hostinger plan suffices now; no Node runtime anywhere.
- Content updates require a rebuild + deploy (acceptable: content changes are
  infrequent and editor-less; mitigate with CI auto-deploy on push).
- If the site ever needs real server logic beyond payment signing (accounts,
  own checkout), revisit: Astro can flip to hybrid SSR with a Node adapter,
  which would then require a Hostinger VPS.

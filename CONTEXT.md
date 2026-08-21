# Context — Startup Weekend Skopje site

Glossary of domain terms. No implementation details here — those live in `docs/adr/`.

## Terms

**Event** — Techstars Startup Weekend Skopje: a 3-day startup hackathon in Skopje, North Macedonia. The site promotes exactly one upcoming edition at a time.

**Ticketing Redirect** — The "Buy Tickets" action. It never collects payment on this site; it hands the visitor off to an external Payment Provider. Until a provider is wired up, the action is a Stub.

**Payment Provider** — The external party that processes ticket payment. Will be either Eventzilla (hosted event page) or CaSys/CPAY (Macedonian card gateway). Undecided; see ADR-0001 for why the site is built to not care.

**Stub** — A visible, clickable element whose real behavior is not wired yet (e.g. Buy Tickets before a Payment Provider exists). A Stub is shipped to production; it is not hidden.

**Coming Soon section** — A section (Speakers, Sponsors) that renders in its final layout position but shows placeholder content because the real data is not announced yet. Distinct from a Stub: Coming Soon is about missing *content*, a Stub is about missing *behavior*.

**Speaker** — A person featured on the event page. Roles seen at past editions: Facilitator, Judge, Mentor, Organizer.

**Sponsor Tier** — Ranking of sponsors that controls display prominence. Tiers seen at past editions: Exclusive, Global Partner, Gold, Silver, plus Organizer and Partner.

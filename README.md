# RelocateCR — Costa Rica Relocation Cost Calculator

Note: the GitHub repo is still named `Movetocr` (created before we settled on the brand name). Rename the repo on GitHub if you want the URL/slug to match — nothing in the code depends on the repo's name.

Static, single-file site (`index.html`) — no backend, no build step, same pattern as aduanacr. Deploys straight to Netlify from this repo.

## What this is

An interactive, personalized cost-of-living calculator for people considering a move/retirement to Costa Rica, paired with a plain-language check against the real residency visa income thresholds (Pensionado, Rentista, Remote Worker/Digital Nomad, Inversionista).

The bet: every competitor in this space (Live and Invest Overseas, RE/MAX Ocean Surf & Sun, 2CostaRicaRealEstate, assorted expat blogs) publishes a static article with generic numbers. None of them built an actual interactive tool. This is the tool.

## Deploying to Netlify

1. Push this repo to GitHub (already done if you're reading this from the repo).
2. In Netlify: **Add new site → Import an existing project → GitHub → select `Movetocr`**.
3. Build settings: leave **Build command** blank, **Publish directory** = `/` (root). There's nothing to build.
4. Deploy. Netlify Forms will auto-detect the `data-netlify="true"` form in `index.html` (the "Get matched" waitlist capture) — no extra config needed. Submissions show up under **Site → Forms** in the Netlify dashboard.
5. Once you're happy with it, buy the domain through Netlify (or point an existing registrar's DNS at Netlify) and attach it in **Domain settings**.

## Data sources / what's cited

- Visa income thresholds: [Dirección General de Migración y Extranjería](https://migracion.go.cr/regularizacion/), cross-checked against multiple immigration-law sources (Pensionado $1,000/mo, Rentista $2,500/mo or $60K deposit, Remote Worker $3,000/$4,000, Inversionista from $150,000).
- Cost-of-living anchors: reported regional budgets (Atenas retired couple ~$2,400/mo, Tamarindo remote worker ~$3,200/mo, Escazú family of 4 ~$4,200/mo) and rental ranges by region/tier, cross-referenced against Expatistan's San José pricing data.
- CAJA (public health insurance): 7–11% of declared income, per commonly reported resident experience — modeled here at 9% with a $70/mo floor.

All of this is dated **September 2026** in the footer. These figures move — re-verify at least twice a year, especially the visa income thresholds (law changes) and the FX-sensitive cost figures.

## Monetization plan (v1, September 2026)

The competitive set here isn't just content sites — RelocateNow Costa Rica (Sarah Elena/Sarah Blanks, ~50K+ Facebook group, YouTube channel, a decade of personal-brand trust) is a full diversified relocation business: 1:1 concierge, group programs, real estate, a $19/mo planning app (ReloHQ), and shipping logistics. Competing head-on for "who do I trust with my relocation" against that is not a fight worth picking in any reasonable timeframe. The right move is to be the free, no-email-wall top-of-funnel tool, and monetize by referring qualified leads into established paid operators — not by trying to build a rival concierge business.

**Confirmed, open, actionable affiliate programs (checked September 2026):**

1. **StartAbroad** — 10% commission, ~$180/sale average, 1-year cookie, monthly payout (bank/PayPal). Their affiliate program is explicitly targeted at "expat and relocation YouTubers, bloggers and newsletter writers" — i.e., us. Covers full relocation services in Costa Rica, Portugal, Spain, Panama. **Start here.**
2. **GAP Equity Loans** — Costa Rica private mortgage lender, referral program pays 15–20% of their commission per funded loan. Real examples: $500 on a $50K loan, $1,000 on $100K, $5,000 on $500K. No Colegio de Abogados restriction (they're a lender, not a law firm) — clean. Best fit for the Inversionista/property-buyer segment of visitors.
3. **International Living** — up to $200/sale on magazine subscriptions and events, flexible partnership terms. Broadest audience match, lowest specificity to Costa Rica.
4. **RelocateNow / Sarah Elena** — no public affiliate program found. Given she already does podcast guest spots and cross-promotion (published author on internationalliving.com), a direct outreach pitch ("free calculator sends you pre-qualified leads, no ad spend on her end") is worth trying even without a formal program.
5. **Live and Invest Overseas** — affiliate program is currently closed ("not accepting affiliates"). Check back periodically.

**Directory/subscription placement** (independent real estate agents, relocation advisors) is still the plan for local boutique partners who aren't already covered by the affiliate programs above — but keep it a flat listing fee, never a per-lead commission, for anyone who is a licensed abogado/notario: Costa Rican lawyers are ethically barred (Código de Deberes Jurídicos, Art. 29) from paying third parties for client referrals, remunerated or not.

## Known gaps / next steps (not built yet)

- **Affiliate links aren't wired into the site yet** — the CTA still just captures email via Netlify Forms. Next step is turning qualifying results (e.g., visa-qualifies + property-buyer signals) into contextual affiliate placements, not just a generic waitlist.
- **Content depth**: right now this is the calculator + one FAQ block. The SEO plan is to out-depth the incumbents (especially Live and Invest Overseas, whose Costa Rica coverage is thinner than their Panama/Colombia content) with dedicated pages per visa type and per region.
- **Exchange rate**: everything is USD-denominated by design (the target audience thinks in USD) — no colones conversion is exposed. Revisit if targeting a CRC-thinking audience later.
- **Testing**: `test.js` (not deployed — Playwright dev dependency only) drives the calculator headlessly and screenshots desktop + mobile. Run with `npx playwright install && node test.js` if you want to re-verify after edits. Don't commit `node_modules`, `*.png`, or `test.js`'s output — see `.gitignore`.

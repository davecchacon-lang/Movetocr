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

## Known gaps / next steps (not built yet)

- **Lead monetization beyond the waitlist form**: the plan is a paid directory/subscription placement for boutique independent real estate agents and relocation advisors — NOT a per-lead commission model. Costa Rican lawyers are ethically barred (Código de Deberes Jurídicos, Art. 29) from paying third parties for client referrals, so if/when an immigration attorney is added to the directory, it has to be a flat listing fee, never pay-per-lead.
- **Affiliate stack**: international movers, expat health insurance brokers, currency/remittance services — none of this is wired up yet, but these are clean (no regulatory friction) and worth adding before leaning hard on real estate referrals alone.
- **Content depth**: right now this is the calculator + one FAQ block. The SEO plan is to out-depth the incumbents (especially Live and Invest Overseas, whose Costa Rica coverage is thinner than their Panama/Colombia content) with dedicated pages per visa type and per region.
- **Exchange rate**: everything is USD-denominated by design (the target audience thinks in USD) — no colones conversion is exposed. Revisit if targeting a CRC-thinking audience later.
- **Testing**: `test.js` (not deployed — Playwright dev dependency only) drives the calculator headlessly and screenshots desktop + mobile. Run with `npx playwright install && node test.js` if you want to re-verify after edits. Don't commit `node_modules`, `*.png`, or `test.js`'s output — see `.gitignore`.

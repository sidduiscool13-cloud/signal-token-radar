# Signal ↗ — token launch radar

An original, offline research dashboard built for the make.fun token-radar-01 brief. MIT licensed. **Working source bundle, not a submitted or provenance-cleared competition entry.**

## Open it

Open `index.html` directly in a browser. It is a self-contained version with all data, styles and scripts embedded; no server, wallet or internet is required. Alternatively open `dashboard/index.html` with its sibling `../data.js` retained.

- **191 ranked candidates**, all **40 official watchlist** records covered.
- The sealed kit snapshot has **758 protocols**, dated **2026-11-14**.
- **567 excluded records** are searchable in the exclusion ledger.
- Search, category/chain filters, watchlist toggle, saved shortlist, pagination and JSON export.
- A detail brief for every ranked record: model formula, actual peer observations, residual range, eligibility caveat and five farming/product-use steps.
- Local farming-checklist progress. Storage failures are handled gracefully.
- Methodology page with source hash, explicit assumptions and leave-one-token-out error.

## Reproduce (Node 22.18+)

No runtime dependencies or installation are required:

```sh
node main.ts --input input/snapshot.json --output generated
# Or the grader's defaults: /input/snapshot.json -> /output
MAKEFUN_OUTPUT_DIR=generated node main.ts --input input
node test.mjs
```

Use an output directory other than the repository root. `main.ts` reads the supplied snapshot rather than hardcoding its rows. It copies the authored dashboard and committed screenshots, emits `board.json`, `data.js`, a standalone `index.html`, and writes `dossier.json` using the unmodified kit library. The files already at the source root are generated deliverables for immediate inspection.

### Browser checks and screenshot refresh

Development tools only; not needed by the grader:

```sh
npm install
npx playwright install --with-deps chromium
node browser-test.cjs
node capture.cjs
node main.ts --input input --output generated
```

The capture tool opens the committed root dashboard with HTTP(S) blocked and records the board, Steakhouse Financial detail and Risk Curators filter at 1440×1240. Generated screenshot assets are committed, so the sealed runtime needs neither browser nor npm.

## Valuation: conditional circulating market capitalization

`TVL × exp[w ln(category median) + (1−w) ln(global median)]`, with `w=n/(n+6)`.

Token identifiers disqualify a ranked record. The official watchlist is authoritative for its own inclusion. Outside it, conservative product-category, wrapper/version-name and exchange-prefix rules apply. **Parent metadata is absent**, so additional candidates are marked for manual parent review rather than certified independent.

Market-cap peers are grouped by CoinGecko identifier (fallback: symbol); maximum recorded market cap and summed observed product TVL prevent duplicate market-cap observations. Only records with positive market cap and TVL contribute; incomplete TVL aggregation and symbol collisions remain limitations. Product categories and MCAP/TVL ratios outside 0.01–100 are excluded. The six-peer prior and bounds are disclosed modeling choices, not optimized parameters.

The 83 eligible traded-token peers produce a **4.43× median held-out error factor**. Each token is removed, the model refit, and its predicted market cap compared with the observed one. The 10th–90th percentile residual multipliers produce the displayed range. This is not a historical launch backtest or a calibrated launch-price interval. Nothing estimates token timing, probability, fully diluted value, user allocation or expected farming profit.

Farming steps use the available category, protocol name and chain. They are concrete risk-limited product-use checklists, **not verified incentive programs**. The sealed snapshot contains no official app URL, contract address, points campaign, audit or reward rule. The dashboard deliberately invents none.

## Evidence and provenance

- Kit: https://make.fun/c/token-radar-01/kit
- Rules: https://make.fun/bounty/token-radar-01
- Snapshot SHA-256: `42a71213519479f3a180cc5010cbbf6bd18a2447fa0ad29e4c5122b6c9184393`
- Unmodified vendor SHA-256: `9ca51b6e5cd84fe46cb0efa61e2ea99365a1fb0e21f2b75e6007f977f0dc326e`
- `test-report.json`: fresh-run byte identity, board constraints, watchlist, farm-step lengths, dossier equality, local file caps.
- `browser-test-report.json`: all 191 details, filters, checklist state, mobile rendering, zero remote requests and JavaScript errors.
- Three real browser captures in `screenshots/` (JPEG, each under 512 KiB; 1440×1240).

**Submission blockers:** Full authentic agent-session exports and a valid run record are not available from this tool interface. `transcripts/README.md` states this explicitly; build summaries are not disguised as harness transcripts. The competition's current provenance rules may be incompatible with a session whose private harness instructions cannot be exported. Obtain organizer guidance and authentic session exports; do not invent logs, metadata or usage. This build has not been sent to make.fun, has no house score, consumes no submission quota, and is not guaranteed competition-eligible. No account was created, repository published, wallet connected or signing key generated.

## Files

| Path | Purpose |
|---|---|
| `main.ts` | Original Node 22 entrypoint, classifier, model and farm-plan generator |
| `vendor/makefun-board.ts` | Official kit library, byte-for-byte |
| `dashboard/` | Authored static HTML/CSS/JS, approximately 30 KB of readable dossier source |
| `board.json` | All 191 rows, sorted by implied value; model and farm plans |
| `data.js` | Local generated dataset including the exclusion ledger |
| `index.html` | Self-contained dashboard for convenient offline use |
| `dossier.json` | Official library output over dashboard and screenshots |
| `screenshots/` | Board, protocol detail, filtered board |
| `input/snapshot.json` | Official sealed kit input, unchanged |
| `test.mjs`, `browser-test.cjs` | Reproduction and functional checks |
| `capture.cjs` | Screenshot capture tool |

Not financial advice. A snapshot's missing token identifier is not evidence that a token does not exist. Never deposit money solely because an allocation might arrive.

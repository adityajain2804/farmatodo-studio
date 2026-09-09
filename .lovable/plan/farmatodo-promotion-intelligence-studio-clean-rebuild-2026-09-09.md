# FarmaTODO Promotion Intelligence Studio — clean rebuild

One polished dashboard, six screens, built fresh on this project. No parallel v1/v2 copies.

## What gets built

**Shared shell**
- Two-tier header: brand + campaign badge + "15-Day Milestone Freeze" + global SKU search + country picker (Colombia / Venezuela) + user. No overlapping elements at 1280px and up.
- Tab row for the six screens — alert counts move into each screen's own content header, never squeezed into the tab label.
- Bottom status strip: data sync, ML engine, optimizer, market.
- One set of number formatters (COP, millions, integers, percent, multiplier) used on every screen with no exceptions.
- One shared filter state (campaign, country, SKU, campaign type, mechanic, audience, Prime scope, clusters, lifecycle) that every screen reads, so a filter change anywhere updates everything.

**Screens**
1. **Campaign Studio** — left offer builder (8 campaign types, 6 mechanics, 4 audiences, channel, 7 clusters, lifecycle, Prime tier, dual discount ladder with the Prime ≥ Regular rule and a violation warning, budget cap), 7 KPI cards, and the customer allocation table with row-expand drawer (dose response, unit cost waterfall, cannibalization audit showing NIM / DER / ROI / pull-forward / cross-SKU loss) plus an override dialog. Rows flagged "would buy anyway" render de-emphasised as excluded, not approvable.
2. **Price & Quality Review** — market/regulatory banner, four audit cards, pending override queue, margin floor ledger (12% floor, RX banned in digital, Dermocosmética capped at 20%).
3. **Portfolio Analytics** — four KPI cards, six-step profit waterfall with plain-language step cards, campaign cost panel + four-stage delivery funnel with drop-off, cluster efficiency matrix, live in-market table.
4. **Causal Lab** — exposure CATE by decile and dose CATE by depth as two clearly separate panels, lifecycle uplift comparison with the fresh-customer callout, and the discount response curve with the full filter bar (mechanic, campaign type, lifecycle, SKU, channel, category, tier), interactive depth slider, threshold/plateau/statutory markers, and elasticity table.
5. **Post-Campaign Audit** — audit header, four KPI cards, five-step reconciliation, mechanic breakdown, Prime vs non-Prime split with uplift premium, decile calibration chart, 30/60/90-day dip and habituation timeline.
6. **Knowledge Graph** — node-link canvas with the five node types and named edge labels, stat cards, planning copilot panel, macro scenario simulator.

**Behaviour everywhere**
- Every discount-burn figure carries "Redeemed Only — not exposure liability."
- Choosing Venezuela shows a clear "Data Not Yet Onboarded" panel on every screen instead of reused Colombia numbers.
- Loading skeletons, empty state with a reset button, and per-panel error state.
- 1280px+ full layout; 1024–1279px wraps KPI cards and turns the left panel into a slide-over; below that everything stacks and tables scroll.

## Technical notes

- Stays on the existing stack: TanStack Start file routes, React Query, shadcn/Radix, Recharts, Tailwind v4 tokens in `src/styles.css`.
- Adds `zustand` (filter store) and `@tanstack/react-table` (virtualised allocation table).
- Structure: `src/lib/formatters.ts`, `src/store/globalFilters.ts`, `src/data/mock.ts` + `src/data/types.ts`, `src/components/layout/`, `src/components/common/` (KPI card, section header, states, badges), `src/features/<screen>/` for screen sections, thin route files under `src/routes/`.
- Mock data uses the exact taxonomies, field names, and figures from the supplied spec so a later swap to the real API is a data-source change only.
- Design tokens (Farmatodo blue, emerald/amber/rose semantics, slate surfaces, typography scale) go into `src/styles.css` as semantic tokens — no hardcoded colours in components.
- Each route gets its own page title and description.

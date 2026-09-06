# Power of Three (PO3 / AMD)

**Category:** 12-power-of-three
**Aliases:** PO3, AMD, AMD doctrine, market-maker model, MMBM/MMSM
**ICT Confidence:** high
**Year Introduced:** 2016
**Year Refined:** 2026
**Source IDs:** ICT-2016-PO3, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-TURTLE-SOUP, THAI-COMMUNITY-2026-POWER-OF-THREE, THAI-COMMUNITY-2026-STD-PROJECTION
**Tags:** po3, amd, market-maker-model, foundational

## Definition

The Power of Three (PO3), also called the **AMD doctrine**, is ICT's three-phase model for how the algorithm delivers price across any timeframe: **Accumulation → Manipulation → Distribution**. It's both a mental model for reading delivered price and a fractal pattern that repeats at every TF (yearly, monthly, weekly, daily, session, 90-minute). When the model runs to upside distribution, it's called **MMBM** (Market Maker Buy Model); to downside distribution, **MMSM** (Market Maker Sell Model) — see [market-maker-model](../31-models/market-maker-model.md) for the full 6-state elaboration of this same MMBM/MMSM cycle. PO3 is the most foundational ICT framework — every named setup (Silver Bullet, Judas Swing, etc.) is an instance of PO3 at a specific scale.

## Formal Criteria

The three phases:

1. **Accumulation** — quiet, range-bound consolidation while institutions build positions.
2. **Manipulation** — engineered fake-out move (Judas Swing) that sweeps liquidity in the wrong direction, providing counter-flow for institutional fills.
3. **Distribution** — the true intended directional move toward HTF DOL.

Some ICT framings add a 4th phase **X (continuation/reversal)** for the late-cycle behavior — see [quarterly-shift-theory](../04-time-cycles/quarterly-shift-theory.md) for the AMD-X expansion in Quarterly Theory. A 2026 community source names a *different* 4-phase variant it calls "Power of Four" — see [amd-vs-po3](../24-amd-cycle/amd-vs-po3.md) for how it differs from AMD-X.

**Single-candle path order (community-attributed):** the same source frames each candle's own Manipulation→Distribution sequence as a wick-order signature, using OHLC/OLHC as shorthand for *which extreme prints first* — not the universal chart-data column order. Bullish PO3: Open → Low (manipulation sweeps down) → High (distribution) → Close, i.e. **OLHC**. Bearish PO3: Open → High (manipulation spikes up) → Low (distribution) → Close, i.e. **OHLC** — the mirror ("กลับด้าน") of the bullish case. This is the same OLHC/OHLC shorthand [daily-bias](../25-htf-bias/daily-bias.md) cites from an earlier chapter by this author without unpacking it; that entry gets the explanation, this one gets the mechanic. **Upgraded from inferred to source-stated:** a later chapter by the same author spells the two orders out in words on its own diagrams — "PO3 Open Low High Close" for bullish, "PO3 Open High Low Close" for bearish — confirming the decode directly rather than by cross-check alone.

**Manipulation-phase extreme quantified in STDv (community-attributed):** the same later chapter measures the Manipulation phase's own Lower High (bullish) / Higher Low (bearish) extreme, and the Distribution phase's own target, in Standard Deviation multiples of that leg — see [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md)'s 2.0–2.5 / 4.0–4.5 community-attributed pair for the full mechanic; that file, not this one, is the home for the quantified criterion.

## Formula / Math

```
po3_phases = ["accumulation", "manipulation", "distribution"]
po3_x      = "continuation_or_reversal"   # optional 4th in some framings

mmbm := PO3 cycle ending in upward distribution
mmsm := PO3 cycle ending in downward distribution
```

## Machine-Readable

```json
{
  "id": "power-of-three",
  "category": "12-power-of-three",
  "aliases": ["PO3", "AMD", "AMD-doctrine", "market-maker-model", "MMBM", "MMSM"],
  "criteria": [
    {"id": "c1", "expr": "phases = [accumulation, manipulation, distribution]"},
    {"id": "c2", "expr": "fractal — repeats at every TF"},
    {"id": "c3", "expr": "MMBM = upside distribution; MMSM = downside"}
  ],
  "timeframes": ["M5","M15","H1","H4","D","W","MN"],
  "confidence": "high",
  "year_introduced": "2016",
  "year_refined": "2026",
  "related": ["accumulation-phase","manipulation-phase","distribution-phase","intraday-amd","htf-amd","amd-cycle-overview","amd-vs-po3","quarterly-shift-theory","judas-swing","range-contraction","range-expansion","turtle-soup","market-maker-model","external-range-liquidity","internal-range-liquidity","daily-bias","standard-deviation-projections","tgif-weekly-po3"],
  "sources": ["ICT-2016-PO3","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-TURTLE-SOUP","THAI-COMMUNITY-2026-POWER-OF-THREE","THAI-COMMUNITY-2026-STD-PROJECTION"]
}
```

## Visual Pattern

```
   PO3 / AMD across one trading day:

   Asia (accumulation)        London open (manipulation)       NY AM (distribution)
   ────────────                  /\                                   /\
        /\  /\                  /  \   ← Judas swing                 /  \
       /  \/  \                /    \    (sweeps Asian range)       /    \
      /        \              /      \                             /      \
                                       \                          /
                                        \  ← reversal             /
                                         \                       /
                                          \________→ true delivery
                                                     (distribution toward HTF DOL)
```

## Timeframes

PO3 is fractal. Day-PO3 maps to Asia-London-NY phases; H1-PO3 maps to a 3-hour cycle of accumulation-manipulation-distribution; M5-PO3 maps to ~15-minute mini-cycles inside a session.

## Examples

**Example 1 — daily MMBM (bullish PO3):**
- Asia: 30-pip range, low-volatility accumulation.
- London open: M5 wicks below Asia low (manipulation / Judas), closes back inside.
- NY AM: 60-pip green displacement, takes PDH BSL (distribution).
- → MMBM completed.

**Example 2 — H1 MMSM:**
- H1 range-bound for 6 hours (accumulation).
- 7th hour: H1 wick above the range high (manipulation).
- Next 4 H1 candles: bearish displacement breaking PWL (distribution).
- → H1 MMSM.

## Common Mistakes

- **Forcing every move into PO3.** Some moves are pure expansion or pure consolidation; PO3 isn't always the right read.
- **Mistaking accumulation for trend continuation.** Choppy ranges that look like accumulation may be late-distribution exhaustion instead.
- **Single-TF PO3 read.** PO3 is most useful when read with HTF bias — a daily MMBM aligned with weekly bullish bias is high-conviction; against weekly bias is lower.
- **Reading Manipulation-phase price action in isolation from [turtle-soup](../20-turtle-soup/turtle-soup.md).** A 2026 community source explicitly pairs the two: the Manipulation-phase sweep-and-reverse is what a Turtle Soup pattern looks like on the chart, and the source states a personal preference for combining Turtle Soup entries with PO3 context specifically, over using Turtle Soup against arbitrary POIs alone.
- **Not routing PO3 through ERL/IRL.** The same source frames the full cycle as: Manipulation sweeps [external-range-liquidity](../02-liquidity/external-range-liquidity.md) (Old High/Low), price rebalances into an [internal-range-liquidity](../02-liquidity/internal-range-liquidity.md) PD array (FVG, OB) near equilibrium, then Distribution runs it toward the next ERL target. Treating Manipulation/Distribution as bare price legs without this liquidity-pool routing misses where the actual entry (the IRL rebalance) sits.

## Related Concepts

- [accumulation-phase](accumulation-phase.md), [manipulation-phase](manipulation-phase.md), [distribution-phase](distribution-phase.md), [intraday-amd](intraday-amd.md), [htf-amd](htf-amd.md).
- [amd-cycle-overview](../24-amd-cycle/amd-cycle-overview.md), [amd-vs-po3](../24-amd-cycle/amd-vs-po3.md).
- [quarterly-shift-theory](../04-time-cycles/quarterly-shift-theory.md), [judas-swing](../13-judas-swing/judas-swing.md), [range-contraction](../01-market-structure/range-contraction.md), [range-expansion](../01-market-structure/range-expansion.md).
- [turtle-soup](../20-turtle-soup/turtle-soup.md) — the chart signature of the Manipulation phase; see Common Mistakes.
- [market-maker-model](../31-models/market-maker-model.md) — the 6-state elaboration of the MMBM/MMSM cycle this file names but doesn't expand on.
- [external-range-liquidity](../02-liquidity/external-range-liquidity.md), [internal-range-liquidity](../02-liquidity/internal-range-liquidity.md) — the liquidity-pool routing behind Manipulation (sweeps ERL) and the Distribution-phase entry (rebalances in IRL); see Common Mistakes.
- [daily-bias](../25-htf-bias/daily-bias.md) — cites the same OLHC/OHLC candle-path shorthand this file's mechanic explains.
- [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md) — the 2.0–2.5/4.0–4.5 quantified criterion for the Manipulation-phase LH/HL extreme.
- [tgif-weekly-po3](../31-models/tgif-weekly-po3.md) — PO3 applied at weekly scale, Friday-specific.

## Citations

- `ICT-2016-PO3` — original PO3 introduction in 2016 mentorship.
- `ICT-2022-MENTORSHIP-OVERVIEW` — PO3 operational framing refined.
- `THAI-COMMUNITY-2026-TURTLE-SOUP` — Turtle Soup + PO3 pairing rationale, p.262; Accumulation→Manipulation→Breaker→Distribution worked diagram, p.267.
- `THAI-COMMUNITY-2026-POWER-OF-THREE` — dedicated Power of Three chapter: OHLC/OLHC single-candle path-order framing, pp.511–514; ERL-sweep → IRL-rebalance → next-ERL routing, pp.509–510; "Power of Four" naming variant, p.503 (see `amd-vs-po3.md`).
- `THAI-COMMUNITY-2026-STD-PROJECTION` — spelled-out "PO3 Open Low High Close"/"PO3 Open High Low Close" diagram labels confirming the OHLC/OLHC decode, p.554.

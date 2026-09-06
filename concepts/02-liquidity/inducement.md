# Inducement (IDM)

**Category:** 02-liquidity
**Aliases:** IDM, induced liquidity
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-TRADE-SETUP
**Tags:** liquidity, inducement, idm, community-attributed

## Definition

**Inducement (IDM)** is a 2026 community source's name — borrowed explicitly from **Smart Money Concepts (SMC)**, not ICT — for a minor liquidity pool (an equal high/low, or a small swing point) that price sweeps **before** running to the real HTF POI or the actual draw on liquidity. The source is direct about its own vocabulary boundary: *"ในการศึกษา ICT Concept ไม่มี Inducement นะครับแต่มันจะมาจากศาสตร์ SMC"* — "in studying ICT Concepts, there is no Inducement — it comes from the SMC discipline." It then supplies the ICT-side translation itself: **Inducement is [internal-range-liquidity](internal-range-liquidity.md)'s internal SSL/BSL**, read at whatever timeframe is currently the "high" one in the analysis. The purpose is the same either way: an intermediate sweep the algorithm clears to trap early entries before the real move, not the move's actual target.

## Formal Criteria

- Inducement is scale-relative, not a fixed price type — it is whichever internal SSL/BSL sits *between* the current analysis point and the HTF POI:
  - On a weekly-range analysis: the Monday–Friday low-to-high internal range.
  - On an H1-anchored analysis: each session's internal high/low.
- Typical forms: equal highs/lows (a retail double-top/bottom the algorithm engineers), or a minor swing point inside a larger consolidation.
- Price sweeping the Inducement is a prerequisite step, not the destination — the setup's actual entry (FVG, Breaker Block, OTE) sits beyond it, closer to the HTF POI.
- In the source's own [ict-2022-model](../31-models/ict-2022-model.md) "Model 2" variant, sweeping the IDM is an explicit, separate step between the Market Structure Shift and the FVG entry — distinct from the earlier Sweep-SSL/BSL step that triggers the MSS itself.

## Formula / Math

```
inducement(analysis_scale) := internal_SSL_or_BSL(analysis_scale)
                               WHERE analysis_scale ∈ {weekly, daily, session, ...}

setup_sequence := HTF_POI -> sweep(external_SSL/BSL) -> MSS
                   -> sweep(inducement)          # IDM step
                   -> entry_zone (FVG | Breaker Block | OTE)
```

## Machine-Readable

```json
{
  "id": "inducement",
  "category": "02-liquidity",
  "aliases": ["IDM", "induced-liquidity"],
  "criteria": [
    {"id": "c1", "expr": "inducement == internal_SSL_or_BSL at current analysis scale"},
    {"id": "c2", "expr": "swept before reaching the entry zone, not the entry zone itself"}
  ],
  "timeframes": ["M15","H1","H4","D","W"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["internal-range-liquidity","external-range-liquidity","equal-highs","equal-lows","liquidity-sweep","ict-2022-model","unicorn-model","mss"],
  "sources": ["THAI-COMMUNITY-2026-TRADE-SETUP"]
}
```

## Visual Pattern

```
   HTF POI ─────
        \
         \  sweep external SSL → MSS
          \___/\
              \  sweep IDM (internal SSL) ← inducement, not the entry
               \___/\
                    \  FVG / Breaker / OTE ← actual entry, closer to HTF POI
                     \___
                         \→ Next Draw on Liquidity
```

## Timeframes

Scale-relative — M15 for session-level Inducement, up to W for a weekly-range analysis. Always state which timeframe is "internal" for a given Inducement read.

## Examples

**Example 1 — source's own weekly-range framing (p.587):** analyzing a Monday–Friday weekly trading range, the low-to-high of that range is the Inducement; the algorithm sweeps it before the real move toward the HTF POI. Rescaled to H1: if H1 is the designated "high" timeframe, each session's own low-to-high is the Inducement at that scale.

## Common Mistakes

- **Treating the Inducement sweep as the entry.** It's the trap that precedes the entry zone, not the zone itself — same distinguishing role [internal-range-liquidity](internal-range-liquidity.md) already assigns generically to IRL vs. ERL.
- **Confusing which SSL/BSL sweep is "the" Inducement.** A setup can contain two distinct sweeps — an external one that triggers the MSS, and an internal one (the IDM) that clears before the entry. They are not the same event; see [ict-2022-model](../31-models/ict-2022-model.md)'s Model 2 step sequence.

## ICT vs Community

**Inducement / IDM is explicitly NOT ICT-original terminology.** The source states this itself — ICT's own vocabulary has no "Inducement"; the term and its underlying trap-sweep framing come from Smart Money Concepts (SMC), a separate, later community rebrand of similar price-delivery ideas. The source's own translation is that Inducement names exactly what ICT already calls internal SSL/BSL ([internal-range-liquidity](internal-range-liquidity.md)) — same mechanic, borrowed label. This library keeps both names rather than merging them: "Inducement/IDM" when citing this or other SMC-adjacent sources, "internal SSL/BSL" or IRL when citing ICT-original material — cross-linked in both directions so a reader arriving at either term finds the other.

## Related Concepts

- [internal-range-liquidity](internal-range-liquidity.md) — the ICT-side equivalent this file translates from.
- [external-range-liquidity](external-range-liquidity.md) — the sweep that triggers the MSS, distinct from the later Inducement sweep.
- [equal-highs](equal-highs.md), [equal-lows](equal-lows.md) — the most common concrete form an Inducement pool takes.
- [ict-2022-model](../31-models/ict-2022-model.md) — Model 2's explicit IDM step.
- [unicorn-model](../31-models/unicorn-model.md) — shares the same prior-sweep-then-entry sequencing.

## Citations

- `THAI-COMMUNITY-2026-TRADE-SETUP` — Inducement/SMC-vs-ICT disclaimer and internal-SSL/BSL translation, p.587; Model 2's IDM step, p.579.

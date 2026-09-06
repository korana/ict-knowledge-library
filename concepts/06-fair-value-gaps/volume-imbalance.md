# Volume Imbalance (FVG-side)

**Category:** 06-fair-value-gaps
**Aliases:** VI, body imbalance, volume gap
**ICT Confidence:** high
**Year Introduced:** 2018
**Year Refined:** 2026
**Source IDs:** ICT-2017-DISPLACEMENT, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-FVG-TECHNIQUE
**Tags:** fvg, volume-imbalance, body-gap

## Definition

A volume imbalance (in the FVG family) is a **body-vs-body gap** between two consecutive candles — open of candle n is strictly above (bullish VI) or below (bearish VI) the close of candle n-1, but their **wicks may overlap**. It is **not** a strict 3-candle FVG (which requires non-overlapping wicks across 3 candles), but it IS an imbalance and serves as a softer FVG-like reference. See [volume-imbalance-detail](../26-imbalance/volume-imbalance-detail.md) for the deeper imbalance-side treatment; this file documents how VIs are treated alongside FVGs in ICT entry logic.

## Formal Criteria

For a bullish VI:

- Candle n-1 closes at `C_{n-1}`.
- Candle n opens at `O_n > C_{n-1}` (body gap up).
- Wicks of n-1 and n may overlap (this is what differentiates VI from FVG).
- Body gap = `[C_{n-1}, O_n]` (the unworked body region).

For a bearish VI: symmetric.

VIs often nest near or inside an FVG; when a VI sits inside the same zone as a 3-candle FVG, conviction stacks.

## Formula / Math

```
bullish_vi(n) := O_n > C_{n-1}
vi_low        := C_{n-1}
vi_high       := O_n
vi_size       := vi_high - vi_low
```

## Machine-Readable

```json
{
  "id": "volume-imbalance",
  "category": "06-fair-value-gaps",
  "aliases": ["VI", "body-imbalance", "volume-gap"],
  "criteria": [
    {"id": "c1", "expr": "open_n != close_{n-1}"},
    {"id": "c2", "expr": "wicks_may_overlap == true (NOT a strict FVG)"},
    {"id": "c3", "expr": "vi_size_meaningful relative to ATR"}
  ],
  "timeframes": ["M5","M15","H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2018",
  "year_refined": "2026",
  "related": ["fair-value-gap","imbalance-vs-fvg","volume-imbalance-detail","imbalance-definition","displacement-definition","nwog"],
  "sources": ["ICT-2017-DISPLACEMENT","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-FVG-TECHNIQUE"]
}
```

## Visual Pattern

```
   bullish volume imbalance:

       ▲
       █  ← candle n: opens above prior close
       █
       O_n
       ──────────────  ← body gap (volume imbalance)
       C_{n-1}
       █
       █  ← candle n-1
       ▼
   (wicks may overlap visually; bodies do not)
```

## Timeframes

M5+. M1 VIs are micro-noise.

## Examples

**Example 1 — bullish VI inside displacement:**
- M15: candle n-1 close 1.0852, high 1.0855.
- Candle n open 1.0858, low 1.0856.
- Body gap = 6 pips at [1.0852, 1.0858]; wicks overlap [1.0855, 1.0856].
- → bullish VI, not a 3-candle FVG. Treat as a softer support reference inside ongoing bullish displacement.

## Common Mistakes

- **Calling VI an FVG.** They're different patterns; VIs have overlapping wicks.
- **Tiny gaps from feed noise.** Sub-tick VIs are not real; filter by ATR.
- **Treating VI as only meaningful on HTF.** A 2026 community source (`THAI-COMMUNITY-2026-FVG-TECHNIQUE`) recommends confining VI use to Daily/Weekly/Monthly and explicitly advises against H4-and-below — a practitioner preference for signal cleanliness, not an ICT restriction. This file's M5+ scope stands; treat "HTF-only" as this source's own operating choice, not a correction.
- **Missing the NWOG connection.** A weekly VI at the Friday-close-to-Sunday-open boundary is the same geometry as [nwog](../31-models/nwog.md) — NWOG is a specific, named instance of this pattern, not a separate concept from VI.

## Related Concepts

- [fair-value-gap](fair-value-gap.md), [imbalance-vs-fvg](../26-imbalance/imbalance-vs-fvg.md), [volume-imbalance-detail](../26-imbalance/volume-imbalance-detail.md), [imbalance-definition](../26-imbalance/imbalance-definition.md), [displacement-definition](../09-displacement/displacement-definition.md).
- [nwog](../31-models/nwog.md) — the weekly-boundary instance of this same VI geometry.

## Citations

- `ICT-2017-DISPLACEMENT`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-FVG-TECHNIQUE` — HTF-preference note and NWOG equivalence claim, pp. 168–174.

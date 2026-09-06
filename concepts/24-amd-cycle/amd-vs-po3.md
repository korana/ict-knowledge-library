# AMD vs PO3 — Disambiguation

**Category:** 24-amd-cycle
**Aliases:** none (disambiguation page)
**ICT Confidence:** high
**Year Introduced:** 2016
**Year Refined:** 2026
**Source IDs:** ICT-2016-PO3, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-POWER-OF-THREE
**Tags:** amd, po3, disambiguation, terminology

## Definition

This page resolves the relationship between **AMD** and **Power of Three (PO3)** — two terms that describe the same underlying ICT concept from slightly different angles.

**Short version:**
- **PO3 (Power of Three)** = the **doctrine / model** name. Emphasizes the institutional/market-maker framing.
- **AMD (Accumulation-Manipulation-Distribution)** = the **phase sequence** name. Emphasizes what's happening at each stage.

They refer to the same three-phase cycle. Use whichever framing fits the conversation. Many ICT sources use "PO3" and "AMD" interchangeably; the distinction is mostly stylistic.

## Formal Criteria

### PO3 — emphasis

- "Three forces controlling the market": the algorithm/institutional layer.
- Often paired with MMBM (buy model) / MMSM (sell model).
- Frames the why behind delivery (institutional intent).

### AMD — emphasis

- The named phases: A → M → D (and optional X).
- Frames the what at each stage.
- Used when discussing time-construct / cycle / phase mechanics.

### Same Substance

Same three-phase pattern, same fractal repetition, same setup logic.

### "Power of Four" — a different 4-phase variant (community-attributed)

Not to be confused with AMD-X above. A 2026 community source names a second 4-phase framing: **Accumulation → Manipulation → Expansion → Distribution**, splitting what this wiki calls the Distribution phase into an Expansion leg (the displacement move itself) and a separate Distribution leg (institutions taking profit once price trades into Old Highs/Old Lows). Where AMD-X *appends* a 4th phase after Distribution completes, this variant *subdivides* Distribution itself. The source calls its own naming choice ("Power of Four" vs "Power of Three") **unresolved** — its own text argues Expansion and Distribution describe the same price action, which is why this wiki keeps the 3-phase model as primary rather than adopting a 4th named phase.

## Formula / Math

```
PO3_doctrine == AMD_phase_sequence    # same cycle, different names

# Both yield: Accumulation → Manipulation → Distribution
```

## Machine-Readable

```json
{
  "id": "amd-vs-po3",
  "category": "24-amd-cycle",
  "aliases": [],
  "criteria": [
    {"id": "c1", "expr": "PO3 and AMD describe the same cycle"},
    {"id": "c2", "expr": "PO3 emphasizes institutional model; AMD emphasizes phases"},
    {"id": "c3", "expr": "'Power of Four' subdivides Distribution; AMD-X appends after it — distinct 4-phase variants"}
  ],
  "timeframes": ["M5","M15","H1","H4","D","W","MN"],
  "confidence": "high",
  "year_introduced": "2016",
  "year_refined": "2026",
  "related": ["power-of-three","amd-cycle-overview","accumulation-phase","manipulation-phase","distribution-phase","intraday-amd","htf-amd"],
  "sources": ["ICT-2016-PO3","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-POWER-OF-THREE"]
}
```

## Visual Pattern

```
   Same cycle, two names:

   PO3 framing                    AMD framing
   ───────────                    ───────────
   Phase 1                ↔        Accumulation
   Phase 2  (Judas)       ↔        Manipulation
   Phase 3                ↔        Distribution
   (Phase 4 X)            ↔        (X — optional)
```

## Timeframes

All TFs.

## Examples

**Example 1 — same setup, two descriptions:**
- "We're in a daily MMBM" (PO3 framing).
- "We're in the daily distribution phase of the AMD cycle" (AMD framing).
- → identical observation; the institution is delivering price upward today.

## Common Mistakes

- **Treating them as different concepts.** They're the same underlying pattern.
- **Overspecifying the X phase.** PO3 in its strict sense has 3 phases; AMD-X is a 4-phase extension that some sources include and others don't.
- **Conflating "Power of Four" with AMD-X.** They're both 4-phase framings but disagree on *where* the 4th phase goes — AMD-X appends after Distribution, "Power of Four" subdivides Distribution itself. Don't treat a source using one as evidence for the other.

## Related Concepts

- [power-of-three](../12-power-of-three/power-of-three.md), [amd-cycle-overview](amd-cycle-overview.md).
- [accumulation-phase](../12-power-of-three/accumulation-phase.md), [manipulation-phase](../12-power-of-three/manipulation-phase.md), [distribution-phase](../12-power-of-three/distribution-phase.md), [intraday-amd](../12-power-of-three/intraday-amd.md), [htf-amd](../12-power-of-three/htf-amd.md).

## Citations

- `ICT-2016-PO3`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-POWER-OF-THREE` — "Power of Four" naming variant, source's own unresolved framing, p.503.

# Order Block vs Supply/Demand — Disambiguation

**Category:** 07-order-blocks
**Aliases:** none (disambiguation page)
**ICT Confidence:** high
**Year Introduced:** 2016
**Year Refined:** 2026
**Source IDs:** ICT-2016-OB-INTRO, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-ORDER-BLOCK
**Tags:** order-block, supply-demand, disambiguation, terminology

## Definition

Many ICT students arrive from supply/demand-based trading systems (Wyckoff-derived, Sam Seiden's "RBR/DBD" framework, etc.). This page clarifies how ICT order blocks differ from classic supply/demand zones — they look similar but have different qualification rules and operational use.

**Short version:**
- **Supply/Demand zones** are wider price bands marked at consolidations / bases before strong moves. They emphasize zone width and time spent, often using ranges of multiple candles.
- **ICT Order Blocks** are specific 1-candle (sometimes 2-candle) patterns with strict structure-break + displacement requirements.

OBs are precise points; S/D zones are areas. The two often overlap geometrically — but the OB is **inside** the S/D zone, more precisely defined.

## Formal Criteria

### Supply / Demand Zone (typical)

- Multi-candle base / consolidation before a strong move.
- Zone width = high-to-low of the consolidation (often 3–10+ candles).
- "Drop-Base-Rally" (DBR) for demand, "Rally-Base-Drop" (RBD) for supply.
- Often graded as "fresh" / "tested" similar to OBs but with looser criteria.
- **Full 4-pattern taxonomy (community-attributed):** a 2026 community source names the complete classic Base taxonomy, spanning both reversal and continuation Bases:
  - **Reversal:** Rally-Base-**Drop** (RBD, supply) / Drop-Base-**Rally** (DBR, demand) — the trend direction changes across the Base.
  - **Continuation:** Rally-Base-**Rally** (RBR, still demand) / Drop-Base-**Drop** (DBD, still supply) — the trend direction is the same on both sides of the Base.
  - The "Base" itself is a **Big Candle + Small Candle + Big Candle** sequence — the Base box is drawn around the small candle only, using the small candle's own high/low.

### The OB / Base Location Overlap (community-attributed)

- The same source notes (p.189) that an Order Block and a Base can be boxed at the **same underlying location** on two different timeframes — e.g., a D1 Bearish OB (single candle, wide box) and an H4 Base (small-candle box nested inside it). Switching timeframe to find a valid small-candle Base inside a wider OB can tighten the entry and stop-loss without abandoning the OB framing.

### ICT Order Block

- **Single candle** (sometimes a 2-candle pair) — the last opposite-color candle before displacement.
- Strict structure-break requirement (BOS or CHoCH/MSS).
- Body of the OB candle = the precise reference zone (with MT as the entry point).
- Wick used only for SL placement.

### The Relationship

```
ICT OB ⊂ wider S/D zone (often)
```

When an S/D base contains an OB candle, the OB is the precise sub-zone inside the wider base. ICT discipline: trade the OB precisely; the S/D framing is too vague for tight risk.

## Formula / Math

```
sd_zone_width_avg = high(consolidation_bars) - low(consolidation_bars)   # often 3-10+ bars
ob_zone_width_avg = abs(open(ob_bar) - close(ob_bar))                    # 1 bar's body

# OB is typically narrower:
ob_width <= sd_zone_width
```

## Machine-Readable

```json
{
  "id": "order-block-vs-supply-demand",
  "category": "07-order-blocks",
  "aliases": [],
  "criteria": [
    {"id": "c1", "expr": "OB == single_candle_with_strict_structure_break"},
    {"id": "c2", "expr": "SD_zone == multi_candle_base_with_loose_criteria"},
    {"id": "c3", "expr": "OB_often_inside_SD_zone == true"}
  ],
  "timeframes": ["M15","H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2016",
  "year_refined": "2026",
  "related": ["order-block-criteria","bullish-order-block","bearish-order-block","mean-threshold","mitigated-order-block","order-block-trading-framework"],
  "sources": ["ICT-2016-OB-INTRO","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-ORDER-BLOCK"]
}
```

## Visual Pattern

```
   Supply/Demand zone vs ICT OB:

   S/D demand zone (5 bars wide)             ICT OB (1 bar)
   ──────────────────                        ─────────
   ░ ░ ░ ░ ░       ▲ ▲ ▲                     ▼  ← single candle
   ░ ░ ░ ░ ░     ▲ ▲ ▲ ▲     RBR             ▼     body precisely
   ░ ░ ░ ░ ░   ▲ ▲ ▲ ▲ ▲                              defined
   ░ ░ ░ ░ ░                                       ▲▲▲ displacement
   ──────────────────                            ▲▲▲ BOS
   wider, looser zone                       narrower, stricter
```

## Timeframes

All TFs.

## Examples

**Example 1 — overlapping OB inside S/D zone:**
- An S/D demand zone identified as "1.0820–1.0840" (5-bar consolidation low to high).
- Inside that consolidation, the last bearish candle before the bullish displacement has body 1.0825–1.0832.
- ICT OB body: [1.0825, 1.0832]. MT 1.08285.
- Tighter zone, tighter SL — better R:R using OB framing than the wider S/D.

## Common Mistakes

- **Treating S/D zones as OBs.** Wider zones with looser criteria don't satisfy ICT's structure-break + displacement requirements.
- **Treating OBs as S/D zones.** Going wider on the OB to "include the wick" turns a precise reference into an arbitrary zone.
- **Ignoring the structure check.** Without a BOS/CHoCH the candle isn't an OB even if it looks like one.
- **Assuming RBD/DBR are the only Base patterns.** RBR (Rally-Base-Rally) and DBD (Drop-Base-Drop) are the continuation-side counterparts — same Big-Small-Big candle geometry, but the trend direction doesn't flip across the Base.

## Related Concepts

- [order-block-criteria](order-block-criteria.md), [bullish-order-block](bullish-order-block.md), [bearish-order-block](bearish-order-block.md), [mean-threshold](../27-equilibrium/mean-threshold.md), [mitigated-order-block](mitigated-order-block.md).
- [order-block-trading-framework](order-block-trading-framework.md) — uses this Base-boxing convention in its Optimization step.

## Citations

- `ICT-2016-OB-INTRO`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-ORDER-BLOCK` — full RBD/DBR/RBR/DBD taxonomy and OB/Base timeframe-overlap note, pp. 188–189.

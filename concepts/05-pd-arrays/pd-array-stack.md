# PD Array Stack (Spatial Retest Order)

**Category:** 05-pd-arrays
**Aliases:** Stack PD Array, PD array stack order, PDA layers
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-MITIGATION-BLOCK, THAI-COMMUNITY-2026-BREAKER-BLOCK, THAI-COMMUNITY-2026-FVG, THAI-COMMUNITY-2026-LIQUIDITY-VOID, THAI-COMMUNITY-2026-REJECTION-BLOCK, THAI-COMMUNITY-2026-ORDER-BLOCK, THAI-COMMUNITY-2026-OLD-HIGH-LOW, THAI-COMMUNITY-2026-OTE
**Tags:** pd-array, stack, retracement, premium-discount, community-attributed

## Definition

The PD array stack describes the **spatial order in which price tests PD arrays as it retraces from a Market Structure Shift (MSS) back toward equilibrium** — not a conviction ranking (see [pd-array-hierarchy](pd-array-hierarchy.md)) and not a per-trade tabulation tool (see [pd-array-matrix](pd-array-matrix.md)). ICT teaches the underlying premium/discount array concept (sometimes called the "Premium Discount Array Matrix") in the 2022 mentorship; this specific 7-layer ordered stack — and the "Stack PD Array" name — is this community source's own systemization of it, built around a vertical layout from equilibrium outward to the range extreme.

Ordered nearest-to-equilibrium first (the layer price is most likely to test soon after an MSS) to furthest (the layer price tests only on a deep retracement):

1. **Mitigation Block** (closest to equilibrium)
2. **Breaker Block**
3. **Liquidity Void**
4. **Fair Value Gap**
5. **Order Block**
6. **Rejection Block**
7. **Old High / Old Low** (furthest — the range extreme)

**Source discrepancy note:** the author's own prose list (Mitigation Block chapter, pp. 22–23) collapses items 1–2 into one entry ("Mitigation Block or Breaker Block") and orders items 3–4 the other way round (FVG before Liquidity Void). Seven of his own stack diagrams — Mitigation Block chapter p.25, Breaker Block chapter p.42, FVG chapter p.66, Liquidity Void chapter p.113, Rejection Block chapter p.228, Order Block chapter p.176, and Old Highs–Old Lows chapter p.238 — draw Mitigation Block and Breaker Block as two separate boxes (Mitigation nearer equilibrium) and draw Liquidity Void nearer equilibrium than the FVG. Every chapter of the book confirms this order — this file follows the diagrams over the one prose list. Kept here rather than silently corrected so a future reader doesn't "fix" it back to the prose ordering.

## Formal Criteria

- The stack only applies **after price has lost structure (MSS)**, in either direction.
- Layers are read outward from equilibrium toward the premium extreme (for a bearish MSS) or the discount extreme (for a bullish MSS).
- A shallow retracement tests only layer 1 (Mitigation Block) before resuming; a deep retracement tests successively further layers.
- Not every layer is present on every leg — the stack is a **search order**, not a guarantee that all 7 layer types exist on a given swing.

## Formula / Math

```
stack_order = [
  "mitigation_block",  # nearest EQ
  "breaker_block",
  "liquidity_void",
  "fair_value_gap",
  "order_block",
  "rejection_block",
  "old_high_or_low",    # furthest, at the range extreme
]

retracement_depth_reached(price, mss_origin, eq) :=
    index of the deepest stack_order layer price has traded into
    since mss_origin, searching outward from eq
```

This is a qualitative search order the source author derived from repeated backtesting, not an ICT-published formula.

## Machine-Readable

```json
{
  "id": "pd-array-stack",
  "category": "05-pd-arrays",
  "aliases": ["stack-pd-array", "pda-layers"],
  "criteria": [
    {"id": "c1", "expr": "applies_only_after_MSS == true"},
    {"id": "c2", "expr": "layers_ordered_eq_to_extreme == ['mitigation_block','breaker_block','liquidity_void','fvg','order_block','rejection_block','old_high_or_low']"}
  ],
  "timeframes": ["M15","H1","H4","D"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["pd-array-hierarchy","pd-array-matrix","mitigation-block","breaker-block","fair-value-gap","liquidity-void","order-block-criteria","rejection-block","equilibrium-definition","buy-side-liquidity","sell-side-liquidity","ote-overview"],
  "sources": ["ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-MITIGATION-BLOCK","THAI-COMMUNITY-2026-BREAKER-BLOCK","THAI-COMMUNITY-2026-FVG","THAI-COMMUNITY-2026-LIQUIDITY-VOID","THAI-COMMUNITY-2026-REJECTION-BLOCK","THAI-COMMUNITY-2026-ORDER-BLOCK","THAI-COMMUNITY-2026-OLD-HIGH-LOW","THAI-COMMUNITY-2026-OTE"]
}
```

## Visual Pattern

```
   Premium extreme  ─── 0
        Old Highs
        Rejection Block
        Bearish Order Block
        Fair Value Gap
        Liquidity Void
        Bearish Breaker Block
        Bearish Mitigation Block   ← nearest EQ
   Equilibrium      ─── 0.5
        Bullish Mitigation Block  ← nearest EQ
        Bullish Breaker Block
        Liquidity Void
        Fair Value Gap
        Bullish Order Block
        Rejection Block
        Old Lows
   Discount extreme ─── 1
```

Diagram order confirmed independently seven times in the same source — every chapter of the book: Mitigation Block chapter (p.25), Breaker Block chapter (p.42), FVG chapter (p.66), Liquidity Void chapter (p.113), Rejection Block chapter (p.228), Order Block chapter (p.176), and Old Highs–Old Lows chapter (p.238) — the last three all fully-rendered Premium/Equilibrium/Discount graphics naming all seven layers explicitly.

## Timeframes

M15+. Best read on the timeframe where the MSS itself occurred; nested lower-TF stacks can exist inside a single HTF layer.

## Examples

**Example 1 — shallow retracement after a bearish MSS:**
- HTF was bullish; price fails to make a new Higher High (failure swing), then breaks structure down (MSS).
- Price pulls back only into the Bearish Mitigation Block (layer 1, nearest EQ) before resuming down — the shallowest possible retracement per the stack.

**Example 2 — deep retracement:**
- Same bearish MSS, but the pullback trades through the Mitigation Block, the Breaker Block, the Liquidity Void, and the FVG before finally reacting at a Bearish Order Block (layer 5) — a deeper retracement, per the stack's search order.

## Common Mistakes

- **Confusing this with [pd-array-hierarchy](pd-array-hierarchy.md).** The hierarchy ranks arrays by *entry conviction*; this stack describes *where price is likely to test next in sequence* after an MSS. They answer different questions and can disagree on which array "matters more" for a given trade.
- **Confusing this with [pd-array-matrix](pd-array-matrix.md).** The matrix is a per-trade multi-timeframe tabulation tool the analyst builds; the stack is a fixed conceptual ordering, not a document.
- **Treating the stack as ICT-taught verbatim.** ICT teaches the underlying premium/discount array concept; this specific 7-layer ordering and its "Stack PD Array" name are this community source's own systemization — see `## ICT vs Community` below.
- **Not connecting this to [ote-overview](../17-optimal-trade-entry/ote-overview.md).** A 2026 community source's own closing observation (a later, separate chapter on OTE) notes that where price rests within an OTE retracement often corresponds to which stack layer it's landing on — the two frameworks describe overlapping territory (retracement depth vs. PD-array identity) from different angles.
- **Collapsing Mitigation Block and Breaker Block into one layer.** The source's own prose list (Mitigation Block chapter) does this, but all seven of the source's own diagrams draw them as two separate, adjacent tiers (Mitigation nearer equilibrium) — see the source discrepancy note in `## Definition`.

## ICT vs Community

ICT taught the premium/discount array concept publicly (referenced here as the "Premium Discount Array Matrix," per `ICT-2022-MENTORSHIP-OVERVIEW`) — the general idea that PD arrays sit at different depths within premium and discount. This source's author explicitly renames it "Stack PD Array" and supplies the specific 7-layer ordered list (Mitigation Block → Breaker Block → Liquidity Void → FVG → Order Block → Rejection Block → Old High/Low, per his own diagrams) as his own systemization, built from his own trading experience rather than a cited ICT lecture or timestamp. Treat the general premium/discount-array concept as ICT-original (high confidence) and this specific ordered stack as community-attributed.

## Related Concepts

- [pd-array-hierarchy](pd-array-hierarchy.md) — conviction ranking (a different axis; see Common Mistakes above).
- [pd-array-matrix](pd-array-matrix.md) — the per-trade tabulation tool (also a different concept despite the similar name in the source material).
- [mitigation-block](../08-breaker-blocks/mitigation-block.md) — layer 1 of the stack; see that file's `## ICT vs Community` section for the related terminology dispute this source also introduces.
- [breaker-block](../08-breaker-blocks/breaker-block.md) — layer 2 of the stack.
- [fair-value-gap](../06-fair-value-gaps/fair-value-gap.md), [liquidity-void](../02-liquidity/liquidity-void.md), [order-block-criteria](../07-order-blocks/order-block-criteria.md), [rejection-block](../19-rejection-blocks/rejection-block.md) — the other layers.
- [buy-side-liquidity](../02-liquidity/buy-side-liquidity.md), [sell-side-liquidity](../02-liquidity/sell-side-liquidity.md) — layer 7 (Old High / Old Low), the furthest layer from equilibrium.
- [equilibrium-definition](../27-equilibrium/equilibrium-definition.md) — the reference point the stack is ordered from.
- [ote-overview](../17-optimal-trade-entry/ote-overview.md) — retracement depth and stack-layer identity as two views of the same territory; see Common Mistakes.

## Citations

- `ICT-2022-MENTORSHIP-OVERVIEW` — premium/discount array concept ("Premium Discount Array Matrix").
- `THAI-COMMUNITY-2026-MITIGATION-BLOCK` — "Stack PD Array" naming and prose ordering, pp. 22–23; stack diagram, p.25.
- `THAI-COMMUNITY-2026-BREAKER-BLOCK` — second, independent stack diagram confirming the 7-tier order, p.42.
- `THAI-COMMUNITY-2026-FVG` — third, independent stack diagram confirming the 7-tier order, p.66.
- `THAI-COMMUNITY-2026-LIQUIDITY-VOID` — fourth, independent stack diagram confirming the 7-tier order, p.113.
- `THAI-COMMUNITY-2026-REJECTION-BLOCK` — fifth, independent stack diagram confirming the 7-tier order, p.228.
- `THAI-COMMUNITY-2026-ORDER-BLOCK` — sixth, independent stack diagram confirming the 7-tier order, p.176.
- `THAI-COMMUNITY-2026-OLD-HIGH-LOW` — seventh, independent stack diagram confirming the 7-tier order, p.238 — the final chapter of the book; every chapter now confirms the same order.
- `THAI-COMMUNITY-2026-OTE` — a different, later chapter by the same author, cross-referencing OTE retracement depth to stack-layer identity, p.292.

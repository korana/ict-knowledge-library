# Change In State Of Delivery (CISD)

**Category:** 07-order-blocks
**Aliases:** CISD, Change In State Of Delivery, Rare Order Block
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-ORDER-BLOCK, THAI-COMMUNITY-2026-MMXM
**Tags:** order-block, cisd, order-flow, community-attributed

## Definition

**Change In State Of Delivery (CISD)** marks the point where the algorithm's price-delivery program flips — from a Buy Program to a Sell Program, or vice versa. Unlike a standard Order Block, which is boxed as a *zone* (the OB candle's open-to-close body), CISD is drawn as a single **line**, at the **open price** of the highest bullish candle (bearish CISD) or the lowest bearish candle (bullish CISD) within the trading range. This source calls CISD a "Rare Order Block" — every CISD is positionally an Order Block (a Bullish/Bearish candle at the range extreme), but not every Order Block is a CISD; CISD additionally requires a prior liquidity sweep and qualifying displacement through its own line. GLOSSARY.md already carries a bare "shift in institutional order flow" stub for this term; this file is its full treatment.

## Formal Criteria

CISD requires, in order:

1. **A trading range extreme.** The candle in question sits at the highest or lowest point of the current trading range.
2. **Sweep Liquidity.** Price sweeps a liquidity pool (BSL for bearish CISD, SSL for bullish CISD) at or near that extreme.
3. **Displacement through the line.** The CISD line is drawn at that candle's **open price**. A later move must displace price decisively through the line — this displacement is what confirms the CISD, not the original candle's formation alone.
4. **No body close-back through the line.** Once the CISD line is set, subsequent retests may pierce it with a **wick only** — a candle **body** closing back through the line invalidates it.
5. **Not necessarily the single last candle.** The qualifying candle can be part of a small reversal cluster (Morning Star / Evening Star, Three Inside Up / Three Inside Down, Tower Top / Tower Bottom) rather than a lone final candle — identify the cluster's highest-open (bearish) or lowest-open (bullish) candle, not just whichever candle happens to be last.
6. **Nested-FVG entry tolerance, per a second 2026 community source.** When the CISD/OB is confirmed by an FVG nested inside it (its "Order Block Confirm With FVG" case, used at the [market-maker-model](../31-models/market-maker-model.md)'s Smart Money Reversal state), price should not enter that nested FVG immediately — or if it does, not beyond 50% of the FVG — with multiple retests expected before entry. This is distinct from Example 1's "entry at 50% of the CISD candle": that's a depth rule for the CISD candle itself, this is a separate depth rule for a smaller FVG sitting inside the CISD/OB zone.

## Formula / Math

```
cisd_line(candle) := open(candle)   # NOT high/low, NOT close — the open price only

cisd_confirmed :=
    candle_at_range_extreme
    AND liquidity_swept (BSL for bearish, SSL for bullish)
    AND later_displacement_closes_through(cisd_line)
    AND no_body_close_back_through(cisd_line)   # wick-only overlap permitted

# entry technique: the CISD line typically gets retested 1-2 times leaving
# only wick overlap; the THIRD retest is this source's preferred entry trigger
entry_trigger := retest_count(cisd_line) >= 3 AND still_holding(cisd_line)
```

## Machine-Readable

```json
{
  "id": "cisd",
  "category": "07-order-blocks",
  "aliases": ["CISD", "change-in-state-of-delivery", "rare-order-block"],
  "criteria": [
    {"id": "c1", "expr": "candle_at_trading_range_extreme == true"},
    {"id": "c2", "expr": "liquidity_swept == true"},
    {"id": "c3", "expr": "displacement_closes_through_open_price_line == true"},
    {"id": "c4", "expr": "no_body_close_back_through_line == true"}
  ],
  "timeframes": ["D","W","MN"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["order-block-criteria","bullish-order-block","bearish-order-block","order-block-trading-framework","liquidity-sweep","displacement-definition","standard-deviation-projections","market-maker-model"],
  "sources": ["THAI-COMMUNITY-2026-ORDER-BLOCK","THAI-COMMUNITY-2026-MMXM"]
}
```

## Visual Pattern

```
   Bearish CISD:

   HTF POI
   ─────────────
              ▲▲   ← highest bullish candle in the range
              ██   ← CISD line drawn at THIS candle's OPEN price
   ─ ─ ─ ─ ─ ─╱─────  CISD line
             ╱
            ╱  ← later displacement closes below the line
           ╱
   Retest 1 (wick only) ─┐
   Retest 2 (wick only) ─┤  entry trigger: the 3rd retest
   Retest 3 → ENTRY ─────┘
```

## Timeframes

D1+ preferred. This source explicitly favors CISD identification on Daily, Weekly, and Monthly charts over lower TFs.

## Examples

**Example 1 — bearish CISD, per source pp.217–220:**
- Price rallies into an HTF POI. The highest bullish candle in the trading range is identified; the CISD line is drawn at that candle's open price.
- Price displaces down through the line with a body close (not just a wick).
- Price returns to retest the line 1–2 times, each retest leaving only a wick overlap (no body close back above the line).
- On the 3rd retest, entry is taken at the CISD line (or at 50% of the CISD candle); stop-loss beyond the CISD candle's highest wick; targets at TP1/TP2/TP3 (prior swing lows) or TP4 (old high, if trading the reversal from the top of the range).

**Example 2 — distinguishing CISD from a plain Order Block, per source p.222:**
- A trading range shows several points where a bullish candle is broken and price later pushes up again before reversing.
- Only ONE of those points is the true CISD (per the range-extreme + sweep + displacement-through-open-line criteria); the others are ordinary Bearish Order Blocks that happen to sit inside the same range, not CISD.

## Common Mistakes

- **Treating any break-and-retest as CISD.** The source's own worked example (p.222) shows a plain break of a bullish candle's body, followed by another push up before reversing, that is explicitly labeled "NO CISD" — it's an ordinary Bearish Order Block, not a CISD, because it fails the range-extreme + sweep + open-price-line criteria.
- **Boxing CISD like a normal Order Block.** CISD is a single **line** at the candle's **open price**, not a zone bounded by open and close.
- **Requiring the CISD candle to be the literal last candle before reversal.** Per source p.221, the qualifying candle can be inside a small reversal cluster (Morning/Evening Star, Three Inside Up/Down, Tower Top/Bottom) — identify by the range-extreme open price, not by "which candle came last."
- **Entering on the first or second retest.** This source's technique specifically waits for the 3rd retest of the CISD line as the entry trigger, treating the first two as wick-only tests that build the setup.
- **Treating this as ICT-published entry mechanics.** ICT is cited by the author as the origin of the CISD concept itself (via YouTube, ICT Mentorship content) — but the specific line-drawing convention, the 3rd-retest entry rule, and the candle-cluster nuance are this author's own operational synthesis; see `## ICT vs Community` below.

## ICT vs Community

ICT teaches Change In State Of Delivery as a concept describing the algorithm's flip between Buy Program and Sell Program delivery — this source's author explicitly attributes the term's origin to ICT's own YouTube content, not his own invention. What the author supplies as his own contribution is the specific **operational packaging**: drawing CISD as a single open-price line rather than a zone, the requirement that only wicks (never bodies) may overlap it, the candle-cluster identification nuance, and — most notably — the 3rd-retest entry trigger rule. None of these specific mechanics carry an ICT lecture citation or timestamp in the source. Treat the underlying CISD concept as ICT-original (referenced, not independently verified in this library) and this file's specific line-drawing and entry-timing mechanics as community-attributed.

## Related Concepts

- [order-block-criteria](order-block-criteria.md) — CISD is positionally an Order Block; see this file's distinction from ordinary OBs.
- [bullish-order-block](bullish-order-block.md), [bearish-order-block](bearish-order-block.md) — the OB variants CISD is a qualified subset of.
- [order-block-trading-framework](order-block-trading-framework.md) — the broader 5-step OB entry process from the same source.
- [liquidity-sweep](../02-liquidity/liquidity-sweep.md) — required precondition.
- [displacement-definition](../09-displacement/displacement-definition.md) — required confirmation through the CISD line.
- [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md) — alternative CISD target framing.
- [market-maker-model](../31-models/market-maker-model.md) — uses CISD-confirmed-by-nested-FVG as one of its two Smart Money Reversal entry setups.
- [swing-high](../01-market-structure/swing-high.md), [swing-low](../01-market-structure/swing-low.md) — the same author reuses this file's Morning/Evening Star and Three Inside Up/Down cluster list for a second, unrelated purpose: validating a Daily Bias Swing Point rather than locating a CISD candle.

## Citations

- `THAI-COMMUNITY-2026-ORDER-BLOCK` — "Change In State Of Delivery (CISD) ** Rare Order Block," pp. 215–226.
- `THAI-COMMUNITY-2026-MMXM` — nested-FVG ≤50% entry tolerance at a CISD/OB used as a Smart Money Reversal setup, pp.376, 385.

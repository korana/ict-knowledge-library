# Rejection Block

**Category:** 19-rejection-blocks
**Aliases:** RB, wick rejection block, long-wick block
**ICT Confidence:** medium
**Year Introduced:** 2018
**Year Refined:** 2026
**Source IDs:** ICT-2018-BLOCKS, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-REJECTION-BLOCK
**Tags:** rejection-block, wick, foundational

## Definition

A rejection block is a candle (or short cluster) characterized by a **strong wick rejection at a key level**, leaving a long wick relative to the body. The wick documents that price tried to go through a level and was forcibly rejected. Distinct from order blocks (which use the body), rejection blocks reference the **wick** as the key zone — the rejected portion is what becomes the future entry/SL anchor. Less standardized than OBs and FVGs; ICT teaches RBs as secondary references.

## Formal Criteria

A rejection block:

- A candle has a long wick on one side (≥ 60% of total candle range).
- The wick reaches a known key level (HTF swing, prior FVG/OB edge, round number, session extreme).
- Price rejects the wick extreme strongly (the close is far from the wick tip).
- Often combined with displacement on the next candle confirming the rejection.
- **Multi-candle zone construction (community-attributed):** when several candles cluster at the trading-range extreme rather than a single clean wick, a 2026 community source draws the RB zone from whichever candle in the cluster has the **longest wick**, with no requirement that it be the first, middle, or last candle in the sequence — same "longest wick wins" convention used to draw the box, regardless of position.

For a **bullish** RB: long lower wick rejecting downward (price tried to go down, rejected up).
For a **bearish** RB: long upper wick rejecting upward (price tried to go up, rejected down).

## Formula / Math

```
range_n = high(n) - low(n)
body_n  = abs(close(n) - open(n))

# Bullish RB:
lower_wick = min(open(n), close(n)) - low(n)
is_bullish_rb := lower_wick >= 0.60 * range_n
                  AND wick reaches known key level
                  AND close near top of range

# Bearish RB: symmetric on upper wick
```

## Machine-Readable

```json
{
  "id": "rejection-block",
  "category": "19-rejection-blocks",
  "aliases": ["RB", "wick-rejection-block", "long-wick-block"],
  "criteria": [
    {"id": "c1", "expr": "wick_pct >= 0.60 of candle range"},
    {"id": "c2", "expr": "wick reaches known key level"},
    {"id": "c3", "expr": "rejection confirmed by close + next-candle displacement"}
  ],
  "timeframes": ["M15","H1","H4","D"],
  "confidence": "medium",
  "year_introduced": "2018",
  "year_refined": "2026",
  "related": ["bullish-rejection-block","bearish-rejection-block","liquidity-sweep","turtle-soup","stop-run-definition","bullish-order-block","bearish-order-block","pd-array-stack"],
  "sources": ["ICT-2018-BLOCKS","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-REJECTION-BLOCK"]
}
```

## Visual Pattern

```
   bullish rejection block:
          ▲
          █  ← close near top of range
          █
          █
        ▼     ← long lower wick (60%+ of range)
        ▼
        ▼
       (wick tip reaches key level)

   bearish RB: mirror.
```

## Timeframes

M15+. Lower TFs have noisy long wicks that aren't structurally meaningful.

## Examples

**Example 1 — bullish RB at PWL:**
- H1 candle: open 1.0865, close 1.0875, low 1.0848 (deep wick), high 1.0876.
- Lower wick = 0.0017 (17 pips); range = 0.0028 (28 pips); wick% = 60.7%.
- Wick tip 1.0848 = PWL (prior week low) SSL pool.
- Next H1: 22-pip green displacement; bullish FVG.
- → bullish rejection block at the PWL level. Long zone reference for future retests.

**Example 2 — entry and stop mechanics (community-attributed, per source pp.230, 233):** on a later retest of a confirmed RB, this source enters at the **50% point of the longest wick** in the zone (not the wick tip and not the candle body) rather than waiting for a fresh displacement candle. Stop-loss sits just beyond the wick tip of the Old High/Old Low the RB is anchored to — a buffer of 50–100 points is optional, but if the RB needs a much wider buffer than that to hold, the source's own view is that it likely isn't a valid RB in the first place.

## Common Mistakes

- **Calling every long-wick candle "RB."** Without a key-level anchor, the long wick is just noise.
- **Confusing RB with sweep.** Liquidity sweeps and rejection blocks overlap heavily. RBs emphasize the resulting *zone* (the wick + body); sweeps emphasize the *event*.
- **Trading RB without confirmation.** Single-candle RB with no follow-through displacement is low-conviction.
- **Treating a broken Old High/Low as still an RB test.** A 2026 community source (`THAI-COMMUNITY-2026-REJECTION-BLOCK`) is explicit: if price actually overtakes the prior Old High or Old Low the RB is anchored to, that's no longer an RB scenario at all — it's now a [buy-side](../02-liquidity/buy-side-liquidity.md)/[sell-side](../02-liquidity/sell-side-liquidity.md) liquidity event instead. Don't keep calling it "RB" once the anchor level is actually taken.
- **Using RB on lower timeframes.** The same source restricts its own use of RB to D1+ and explicitly discourages H4 and below — at those timeframes price more often just sweeps BSL/SSL through the zone rather than truly rejecting from it. This is a stricter preference than this file's existing M15+ scope; treat it as this source's own operating choice, not a correction.
- **Missing the Failure Swing / Double-Top-Bottom lineage.** The same source notes a holding RB is often the origin point of a [Failure Swing](../08-breaker-blocks/mitigation-block.md) that forms a Double/Triple Top or Double/Triple Bottom — worth checking for when assessing whether an RB is likely to hold.

## Related Concepts

- [bullish-rejection-block](bullish-rejection-block.md), [bearish-rejection-block](bearish-rejection-block.md).
- [liquidity-sweep](../02-liquidity/liquidity-sweep.md), [turtle-soup](../20-turtle-soup/turtle-soup.md), [stop-run-definition](../29-stop-runs/stop-run-definition.md), [bullish-order-block](../07-order-blocks/bullish-order-block.md), [bearish-order-block](../07-order-blocks/bearish-order-block.md).
- [pd-array-stack](../05-pd-arrays/pd-array-stack.md) — RB's position as the outermost layer (just inside Old High/Low) in this community source's spatial retest ordering.

## Citations

- `ICT-2018-BLOCKS`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-REJECTION-BLOCK` — the author cites ICT's own "ICT Mentorship Core Content – Month 04" as the origin lecture for this concept (a secondary pointer, not independently verified here); multi-candle zone construction, 50%-of-wick entry, stop-buffer mechanics, D1+ timeframe preference, and the Failure Swing lineage note, pp. 227–236.

> Confidence is `medium` because RB usage varies across the ICT community; many practitioners fold the concept into liquidity sweeps and OBs.

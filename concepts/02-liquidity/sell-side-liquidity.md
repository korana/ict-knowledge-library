# Sell-Side Liquidity (SSL)

**Category:** 02-liquidity
**Aliases:** SSL, sellstops, resting sell orders, liquidity below
**ICT Confidence:** high
**Year Introduced:** 2016
**Year Refined:** 2026
**Source IDs:** ICT-2016-LIQUIDITY, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-FVG, THAI-COMMUNITY-2026-OLD-HIGH-LOW, THAI-COMMUNITY-2026-LIQUIDITY-TRADING
**Tags:** liquidity, sellside, stops, foundational

## Definition

Sell-side liquidity is the set of resting sell orders sitting below price — primarily stop-losses from long positions and stop-entry orders from breakdown sellers. The mirror of [buy-side-liquidity](buy-side-liquidity.md). Algorithmic price delivery is drawn toward SSL pools when bearish intent is being expressed.

## Formal Criteria

SSL accumulates at:

- The low of any prior swing low (STL, ITL, LTL).
- Equal lows ([equal-lows](equal-lows.md)).
- Ascending trendline lows (retail support trendlines).
- Session lows (Asia low, London low, NY AM low, prior day low, prior week low, prior month low).
- Round-number levels (00, 50) below price.

SSL is "taken" when price trades through the level.

A 2026 community source adds a qualifying **approach structure** for the Old Low specifically: it prefers to see a series of Higher Highs / Higher Lows in the swings leading into the Old Low before treating the eventual sweep as high-conviction, rather than reacting to the first single test.

## Formula / Math

```
SSL_levels(t) = { all unswept swing lows and equal-lows below current price at time t }
                ∪ { unswept session lows below current price }

SSL_swept(level) := low(any future bar) < level
```

## Machine-Readable

```json
{
  "id": "sell-side-liquidity",
  "category": "02-liquidity",
  "aliases": ["SSL", "sellstops", "liquidity-below"],
  "criteria": [
    {"id": "c1", "expr": "level == prior_swing_low OR level == equal_lows OR level == session_low"},
    {"id": "c2", "expr": "level < current_price"}
  ],
  "timeframes": ["M1","M5","M15","H1","H4","D","W"],
  "confidence": "high",
  "year_introduced": "2016",
  "year_refined": "2026",
  "related": ["buy-side-liquidity","equal-lows","liquidity-sweep","liquidity-pool","draw-on-liquidity","swing-low","three-drive-pattern"],
  "sources": ["ICT-2016-LIQUIDITY","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-FVG","THAI-COMMUNITY-2026-OLD-HIGH-LOW","THAI-COMMUNITY-2026-LIQUIDITY-TRADING"]
}
```

## Visual Pattern

```
    \      /  ← current price approaching from above
     \    /
      \  /
       \/        ← prior swing low
   ─────────────
              SSL ←  sell stops + breakdown sell orders rest here
```

Every unswept swing low below price is an SSL pool.

## Timeframes

All TFs. HTF SSL (PDL, PWL, PML) is heavier than LTF SSL.

## Examples

**Example 1 — Equal-lows SSL pool:**
- M15 prints two equal lows at 1.0850.
- A later bar wicks to 1.0848, closes at 1.0860.
- → SSL swept; the equal-lows pool is now "claimed."

**Example 2 — Daily SSL stack:**
- PWL at 1.0700, PDL at 1.0750, current STL at 1.0780.
- Bearish bias targets the 1.0780 → 1.0750 → 1.0700 ladder.

**Example 3 — round-number SSL clustering (gold):**
- Gold sells off toward 1900, a round figure (also 1925, 1950, 1975, 2000).
- Retail sell-stop and breakdown-sell orders cluster at these levels independent of any swing-low structure, per a 2026 community source — the round number itself is the draw, not a prior low.

## Common Mistakes

- **Pixel-perfect lows.** Equal lows don't need to match to the tick — within a few pips on FX, a few ticks on indices, ICT considers them equal.
- **Ignoring sweep direction.** A wick through SSL with a strong reversal close = liquidity raid. A close below SSL with displacement = bearish BOS, not a sweep.
- **One-sided analysis.** Always look at both BSL and SSL relative to current price; the algorithm's draw is whichever is the more attractive target given HTF bias and session.
- **Reacting to the first test of an Old Low.** A 2026 community source prefers to see the swing structure leading in first print a series of Higher Highs / Higher Lows before the sweep — see [three-drive-pattern](../01-market-structure/three-drive-pattern.md) for the fuller multi-leg version of this same approach-structure preference.

## Related Concepts

- [buy-side-liquidity](buy-side-liquidity.md) — mirror.
- [equal-lows](equal-lows.md) — concentrated SSL pools.
- [liquidity-sweep](liquidity-sweep.md) — sweep behavior.
- [liquidity-pool](liquidity-pool.md) — broader concept.
- [draw-on-liquidity](draw-on-liquidity.md) — SSL as a DOL option.
- [swing-low](../01-market-structure/swing-low.md) — primary SSL location.
- [three-drive-pattern](../01-market-structure/three-drive-pattern.md) — the community-attributed multi-leg approach structure into an Old Low.

## Citations

- `ICT-2016-LIQUIDITY` — SSL introduced.
- `ICT-2022-MENTORSHIP-OVERVIEW` — operational framing.
- `THAI-COMMUNITY-2026-FVG` — prior month low (PML) explicitly enumerated alongside PDL/PWL, pp. 79–80.
- `THAI-COMMUNITY-2026-OLD-HIGH-LOW` — Higher-Highs/Higher-Lows approach-structure preference before treating an Old Low sweep as high-conviction, p.242.
- `THAI-COMMUNITY-2026-LIQUIDITY-TRADING` — round-number SSL clustering, gold 1900/1925/1950/1975/2000 worked example, p.320.

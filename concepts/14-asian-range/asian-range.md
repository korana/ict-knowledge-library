# Asian Range

**Category:** 14-asian-range
**Aliases:** Asia range, AR, Asian session range
**ICT Confidence:** high
**Year Introduced:** 2016
**Year Refined:** 2026
**Source IDs:** ICT-2016-LIQUIDITY, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-ASIAN-RANGE
**Tags:** asian-range, liquidity, foundational

## Definition

The Asian range is the price range formed during the Asia session (typically 18:00 prev → 03:00 NY, with most-tracked formation 20:00–00:00 NY inside the Asia killzone). It is bounded by the **Asian range high** ([asian-range-high](asian-range-high.md)) and **Asian range low** ([asian-range-low](asian-range-low.md)). ICT teaches the Asian range as the **engineered liquidity setup** for London delivery: London's first killzone almost always sweeps one bound (the Judas swing) and then expands toward the opposite or beyond.

## Formal Criteria

- Time window: most commonly the Asian killzone 20:00 → 00:00 NY (some references use the entire Asia session 18:00–03:00).
- Bounded by:
  - Asian range high = max(high) over the window.
  - Asian range low = min(low) over the window.
- Equal highs / equal lows along the bounds are common — they make the bounds explicit liquidity pools.
- Range size: typically 25–60 pips on EURUSD; varies by instrument and volatility regime. A 2026 community source independently states the same order of magnitude — "200–400 จุด" (points, its own CBDR-chapter unit, not pips; see [central-bank-dealing-range](../04-time-cycles/central-bank-dealing-range.md)'s unit-correction note) — which on a standard 5-digit FX feed (10 points = 1 pip) converts to ~20–40 pips, checked and left as a confirming citation rather than a change to this figure.
- **Breakout-and-retest continuation (community-attributed):** distinct from the wick-based Judas sweep in [asian-range-sweep](asian-range-sweep.md), a 2026 community source frames the Asian range as a "base" that price sometimes *closes through* with real displacement rather than merely wicking — when that happens, the broken bound often gets retested from the far side before price continues in the breakout direction. This is the flip-zone/breaker mechanic (a broken level trading the opposite role on return) applied to the Asian range's own bound, not a new mechanism — see [inversion-fvg](../06-fair-value-gaps/inversion-fvg.md)'s "Flip Zone" alias and [bullish-breaker](../08-breaker-blocks/bullish-breaker.md)/[bearish-breaker](../08-breaker-blocks/bearish-breaker.md) for the underlying mechanic. The source's own cover subtitle names this the chapter's central use of the range ("building a foundation for Breakout").

## Formula / Math

```
asian_window = [20:00, 00:00] NY      # canonical KZ-anchored
# or [18:00 prev, 03:00] NY for full session anchor

asian_high = max(high(t)) for t in asian_window
asian_low  = min(low(t))  for t in asian_window
asian_range_size = asian_high - asian_low
asian_eq         = (asian_high + asian_low) / 2
```

## Machine-Readable

```json
{
  "id": "asian-range",
  "category": "14-asian-range",
  "aliases": ["asia-range", "AR", "asian-session-range"],
  "criteria": [
    {"id": "c1", "expr": "bounds_formed_during_asian_window == true"},
    {"id": "c2", "expr": "high == max_high AND low == min_low"},
    {"id": "c3", "expr": "closed_through_bound_with_displacement -> broken_bound acts as breaker/flip_zone on retest"}
  ],
  "timeframes": ["M5","M15","H1"],
  "confidence": "high",
  "year_introduced": "2016",
  "year_refined": "2026",
  "related": ["asian-range-high","asian-range-low","asian-range-sweep","asian-session-bias","asian-range-projections","asia-session","asia-killzone","judas-swing","liquidity-pool","range-contraction","inversion-fvg","bullish-breaker","bearish-breaker","central-bank-dealing-range"],
  "sources": ["ICT-2016-LIQUIDITY","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-ASIAN-RANGE"]
}
```

## Visual Pattern

```
   18:00 prev ─── 20:00 ─── 00:00 ─── 03:00 NY
                  |  ↓ Asia KZ  |
   asian_high ────┼─────────────┼──── ← BSL pool
                  │   /\  /\    │
                  │  /  \/  \   │  (overlapping candles)
                  │ /        \  │
   asian_low  ────┴─────────────┴──── ← SSL pool
                                 ↓
                          London open targets one
                          of these bounds (Judas)
```

## Timeframes

M5 / M15 are the practical TFs for marking bounds. H1 captures the entire range in 4 candles and is too coarse to see equal highs/lows.

## Examples

**Example 1 — typical EURUSD Asian range:**
- 20:00–00:00 NY: M5 prints high 1.0876 at 22:30 NY and low 1.0848 at 23:15 NY.
- Range = 28 pips.
- Two equal lows form at 23:00 and 23:50 around 1.0848.
- → London open is highly likely to sweep 1.0848 first (Judas down) before any move up.

## Common Mistakes

- **Using broker time.** All ICT Asian range references are NY-anchored.
- **Ignoring the killzone-vs-session distinction.** The full Asia session (18:00–03:00) range and the Asian KZ range (20:00–00:00) often differ; specify which you're using. Most ICT references use the KZ window.
- **Treating the range as a pivot, not as liquidity.** While the range is still intact (unbroken), it is not a "support/resistance" zone — it is **engineered liquidity** that London is going to take. Bias should be set by HTF, not by the range alone. This is scoped to the *unbroken* range: once a bound has actually been closed through with displacement (see the breakout-and-retest note above), the broken level can legitimately act as a breaker/flip zone on retest — a later-stage mechanic, not a contradiction of this rule.

## Related Concepts

- [asian-range-high](asian-range-high.md), [asian-range-low](asian-range-low.md) — bounds.
- [asian-range-sweep](asian-range-sweep.md) — what London does to the bounds.
- [asian-session-bias](asian-session-bias.md) — how to read direction from Asia.
- [asian-range-projections](asian-range-projections.md) — extension targets.
- [asia-session](../15-sessions/asia-session.md), [asia-killzone](../10-killzones/asia-killzone.md) — parent session/KZ.
- [judas-swing](../13-judas-swing/judas-swing.md) — what London does to the range.
- [liquidity-pool](../02-liquidity/liquidity-pool.md), [range-contraction](../01-market-structure/range-contraction.md).
- [inversion-fvg](../06-fair-value-gaps/inversion-fvg.md), [bullish-breaker](../08-breaker-blocks/bullish-breaker.md), [bearish-breaker](../08-breaker-blocks/bearish-breaker.md) — the flip-zone/breaker mechanic behind the breakout-and-retest note above.
- [central-bank-dealing-range](../04-time-cycles/central-bank-dealing-range.md) — the sibling time-bounded range this file's size figure was cross-checked against.

## Citations

- `ICT-2016-LIQUIDITY`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-ASIAN-RANGE` — breakout-and-retest framing (the chapter's own stated thesis), p.470; "200–400 จุด" range-size figure cross-checked against the existing 25–60 pip figure, p.469.

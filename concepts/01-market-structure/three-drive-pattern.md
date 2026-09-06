# Three Drive Pattern

**Category:** 01-market-structure
**Aliases:** Three Drive, 3 Drive Pattern, Rising Wedge, Falling Wedge
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-OLD-HIGH-LOW
**Tags:** market-structure, three-drive, wedge, reversal, community-attributed

## Definition

The Three Drive Pattern is a three-leg approach structure this community source uses to anchor high-conviction reversals at an [Old High or Old Low](../02-liquidity/buy-side-liquidity.md). It predates SMC/ICT entirely — the author calls it one of his personal "killer techniques," historically taught as Bullish/Bearish Three Drive measured with Fibonacci retracements and later cross-pollinated with Divergence and RTM's "Compression" concept. The modern popular framing draws the same three legs as a **Rising Wedge** (bearish) or **Falling Wedge** (bullish), which is why SMC/ICT practitioners often don't recognize it as the same pattern under its older name. This source packages the classic pattern as a PD-array-stack-integrated entry: the three-drive approach is the setup, and a sweep + displacement + FVG at the Old High/Low is the trigger.

## Formal Criteria

Three legs, each measured against the one before it, in the same direction as the prevailing approach:

1. **Drive 1** — an initial move toward the HTF PD array (Old High for a bearish reversal, Old Low for a bullish one).
2. **Drive 2** — a fakeout push that still maintains the appearance of trend continuation: a Higher High and Higher Low (bullish approach) or Lower Low and Lower High (bearish approach), and it must exceed Drive 1's extreme.
3. **Drive 3** — the final move into the HTF PD array; it must exceed Drive 2's extreme in the same direction.

The pattern does not gate on exactly three drives — price may extend to a 4th or 5th drive before reversing. Do not assume reversal is imminent just because a 3rd drive has completed; that is a common mistake, not a rule.

The full entry checklist (source p.260), in order:

1. Price first breaks through the anchor Old High or Old Low.
2. At least 3 drives complete (more are possible).
3. Drive 3 produces an MSS comprising: a BSL/SSL sweep of the Old High/Low, a qualifying [displacement](../09-displacement/displacement-definition.md), and an FVG formed by the displacement candle.

A failed Drive 3 — one that does not exceed Drive 2's extreme — is not a Three Drive signal. Read it as a plain liquidity sweep instead and fall back to [mitigation-block](../08-breaker-blocks/mitigation-block.md) as the next PD array in the [pd-array-stack](../05-pd-arrays/pd-array-stack.md).

## Formula / Math

```
three_drive_bearish(d1, d2, d3) :=
    d1.high == first_approach_toward(old_high)
    AND d2.high > d1.high AND d2.low > d1.low     # HH/HL fakeout continuation
    AND d3.high > d2.high                          # Drive 3 must exceed Drive 2

three_drive_bullish(d1, d2, d3) :=
    d1.low == first_approach_toward(old_low)
    AND d2.low < d1.low AND d2.high < d1.high      # LL/LH fakeout continuation
    AND d3.low < d2.low                             # Drive 3 must exceed Drive 2

entry_valid :=
    price_broke_old_high_or_old_low
    AND drive_count >= 3
    AND drive_3_produces_MSS   # sweep + displacement + FVG on the displacement candle

# a drive count above 3 is a valid extension, not a disqualifier
# a Drive 3 that fails to exceed Drive 2 disqualifies the pattern entirely
```

## Machine-Readable

```json
{
  "id": "three-drive-pattern",
  "category": "01-market-structure",
  "aliases": ["three-drive", "3-drive-pattern", "rising-wedge", "falling-wedge"],
  "criteria": [
    {"id": "c1", "expr": "price_broke_old_high_or_old_low == true"},
    {"id": "c2", "expr": "drive_count >= 3"},
    {"id": "c3", "expr": "drive_2_exceeds_drive_1_extreme == true"},
    {"id": "c4", "expr": "drive_3_exceeds_drive_2_extreme == true"},
    {"id": "c5", "expr": "drive_3_MSS == (liquidity_sweep AND displacement AND fvg_formed_by_displacement_candle)"}
  ],
  "timeframes": ["H4","D","W"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["mitigation-block","liquidity-sweep","displacement-definition","fair-value-gap","fvg-setup-checklist","pd-array-stack","buy-side-liquidity","sell-side-liquidity","mss"],
  "sources": ["THAI-COMMUNITY-2026-OLD-HIGH-LOW"]
}
```

## Visual Pattern

```
   Bearish Three Drive (Rising Wedge), approaching Old High:

        Old High (BSL)  ─────────────────────────
                                          Drive 3 ╱▲  ← MSS: sweep + displacement + FVG here
                                        ╱────────╱
                              Drive 2 ╱▲
                            ╱────────╱
                  Drive 1 ╱▲
                ╱────────╱
   ────────────╱
   Each drive's high exceeds the one before it; lows also rise (HH/HL) —
   the wedge narrows into the Old High before reversing down.
```

Bullish Three Drive (Falling Wedge) is the mirror, approaching Old Low with descending drives (LL/LH).

## Timeframes

H4+. The source works this pattern on higher timeframes where the Old High/Low anchor and the multi-drive approach are both structurally meaningful; entries are refined on a lower TF once Drive 3's MSS triggers.

## Examples

**Example 1 — successful bearish Three Drive into Old High, per source pp.256, 259:**
- Price approaches an HTF Old High across three rising drives, each exceeding the last.
- Drive 3 sweeps the Old High (BSL taken), displaces down, and leaves an FVG.
- Entry on the retrace into that FVG; the move leads into an HTF FVG/Breaker Block target.

**Example 2 — BSL+SSL combined case where price never reaches Old Low, per source p.257:**
- After the bearish leg completes, the following bullish approach toward Old Low stalls before actually reaching it.
- The source treats this as a *stronger* reversal signal, not a failure — read as institutional absorption rather than a requirement that price must tag the old level.

**Example 3 — failed Three Drive, per source p.258:**
- Price reaches the Old High area, but Drive 3 fails to print a High above Drive 2.
- No Three Drive signal — treat as a plain liquidity sweep ([Failure Swing](../08-breaker-blocks/mitigation-block.md)) and fall back to Mitigation Block as the next PD array layer.

## Common Mistakes

- **Assuming exactly three drives means an immediate reversal.** The source explicitly warns the market may extend to a 4th or 5th drive; count is a minimum, not a ceiling.
- **Treating a failed Drive 3 as a weaker version of the pattern.** Per source p.258, a Drive 3 that doesn't exceed Drive 2 is not a Three Drive setup at all — it's a plain BSL/SSL sweep, and the correct read is to fall back to [mitigation-block](../08-breaker-blocks/mitigation-block.md), not to keep waiting for the wedge to complete.
- **Confusing the entry trigger with [fvg-setup-checklist](../06-fair-value-gaps/fvg-setup-checklist.md).** Both gate entry on a sweep + displacement + FVG triad, and the mechanics of that final trigger are the same. The difference is upstream: Three Drive additionally requires the three-leg approach structure (Drive 1 → Drive 2 → Drive 3, each exceeding the last) before that trigger is even evaluated. A sweep+displacement+FVG with no prior multi-drive approach is an FVG Setup Checklist entry, not a Three Drive entry.
- **Requiring price to tag the old level exactly.** Per source p.257, a move that stalls short of Old Low can be the stronger signal, not a disqualifying one.
- **Treating this as SMC/ICT-original.** The pattern predates both frameworks; see `## ICT vs Community` below.

## ICT vs Community

The Three Drive Pattern (and its Rising Wedge / Falling Wedge framing) is not an ICT or SMC concept. The author states plainly that it is an older classical-chart-pattern technique — used across forex, futures, crypto, and stocks well before SMC/ICT existed, historically paired with Fibonacci-retracement measurement and later cross-pollinated with Divergence and RTM's "Compression" idea. What this source contributes is the specific **integration** of that classical pattern into the PD-array-stack framework: gating the Three Drive's entry trigger on an ICT-original sweep + displacement + FVG (MSS) at the Old High/Low, rather than on the classical pattern's own completion alone. Treat the three-drive/wedge structure itself as pre-ICT community technique, and the sweep+displacement+FVG entry gate as this source's own packaging of ICT-original components (see [fvg-setup-checklist](../06-fair-value-gaps/fvg-setup-checklist.md) for the closely related, non-wedge version of the same trigger).

## Related Concepts

- [mitigation-block](../08-breaker-blocks/mitigation-block.md) — the fallback PD array when a Three Drive attempt fails (Drive 3 doesn't exceed Drive 2).
- [pd-array-stack](../05-pd-arrays/pd-array-stack.md) — Old High/Low is the stack's furthest layer; Three Drive is this source's preferred approach structure into it.
- [buy-side-liquidity](../02-liquidity/buy-side-liquidity.md), [sell-side-liquidity](../02-liquidity/sell-side-liquidity.md) — Old High/Low as a liquidity pool; the anchor this pattern approaches.
- [liquidity-sweep](../02-liquidity/liquidity-sweep.md), [displacement-definition](../09-displacement/displacement-definition.md), [fair-value-gap](../06-fair-value-gaps/fair-value-gap.md) — the three components of Drive 3's MSS trigger.
- [fvg-setup-checklist](../06-fair-value-gaps/fvg-setup-checklist.md) — the same sweep+displacement+FVG trigger without the three-leg approach requirement; see Common Mistakes for the distinction.
- [mss](mss.md) — the structural break Drive 3's trigger is a specific case of.

## Citations

- `THAI-COMMUNITY-2026-OLD-HIGH-LOW` — "PD Array Matrix : Old Highs – Old Lows & Three Drive," Three Drive Pattern sub-chapter, pp. 252–260.

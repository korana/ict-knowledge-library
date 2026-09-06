# Weekly Profile Patterns

**Category:** 22-quarterly-theory
**Aliases:** ICT Weekly Profile, weekly shapes, weekly delivery patterns
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE
**Tags:** quarterly-theory, weekly, community-attributed

## Definition

A 2026 community source's **six-member named taxonomy** of recurring weekly-candle shapes, presented under the heading "ICT Weekly Profile." Where [weekly-quarters](weekly-quarters.md) documents one default week shape (Mon accumulation → Tue manipulation → Wed distribution → Thu continuation/reversal) and that file's own Common Mistakes already warns it fits only "~50% of weeks," this taxonomy is what the other half look like: six distinct day-of-week arrangements for where the week's high, low, and reversal actually land. Each pattern is presented as a Bullish/Bearish mirror pair.

## Formal Criteria

| # | Name | Shape |
|---|---|---|
| 1 | **Classic Tuesday Low/High of Week** | Week's high or low prints on Tuesday; Monday made neither extreme. Source notes the Tuesday extreme itself typically forms during the London or NY killzone, not elsewhere in the day. |
| 2 | **Wednesday Low/High of Week** | Same shape as #1, shifted one day later — the week's extreme prints Wednesday instead of Tuesday, again during London or NY killzone. Source adds an unelaborated note to check for a Higher-High/Lower-Low divergence between the London and NY session at that extreme. |
| 3 | **Consolidation Thursday Reversal** | Price ranges sideways Monday–Wednesday, then Thursday prints a Judas Swing ([judas-swing](../13-judas-swing/judas-swing.md)) that reverses into the week's real directional move. Source notes this shape recurs specifically the **second week of the month, ahead of an FOMC announcement** — corroborated by the same claim appearing on both the Bullish line and the page's own note. |
| 4 | **Consolidation Midweek Rally/Decline** | Bullish: price sets the week's high starting Tuesday, Wednesday prints a Higher High, then reverses down into sell-side liquidity before Thursday. Bearish: mirror — week's low from Tuesday, Wednesday Lower Low, reverses up into buy-side liquidity before Thursday. |
| 5 | **Seek & Destroy Bullish/Bearish Friday** [sic, source spells it "Seak"] | Not a day-of-week shape but a set of **conditions under which the week has no clean shape at all** — price sweeps both sides of a wide sideways range with no directional resolution. Named triggers: FOMC announced on two consecutive days (Wed–Thu); a bank holiday during which the London session sweeps both the Asian high and Asian low; generally thin-liquidity periods where stops run past the normal range because too few participants are trading it; Dollar Index moving opposite the pre-release consensus around key news (e.g. Non-Farm). |
| 6 | **Wednesday Weekly Reversal** | Price ranges sideways Monday–Tuesday, then Wednesday's London session delivers a sharp, large-swing move that sweeps a specific liquidity pool — either an HTF POI's resting SSL/BSL or the prior week's SSL low / BSL high — before reversing hard in the opposite direction. |

## Formula / Math

```
weekly_profile ∈ {
  classic_tuesday_extreme,       # #1
  wednesday_extreme,             # #2
  consolidation_thursday_reversal, # #3
  consolidation_midweek_rally_decline, # #4
  seek_and_destroy,              # #5, no clean shape
  wednesday_weekly_reversal      # #6
}

# not exhaustive of every week — weekly-quarters.md's own default
# Mon-Tue-Wed-Thu shape covers roughly the other half.
```

## Machine-Readable

```json
{
  "id": "weekly-profile-patterns",
  "category": "22-quarterly-theory",
  "aliases": ["ICT-Weekly-Profile", "weekly-shapes", "weekly-delivery-patterns"],
  "criteria": [
    {"id": "c1", "expr": "classic_tuesday_extreme: week high/low on Tue, London/NY killzone, Mon made neither"},
    {"id": "c2", "expr": "wednesday_extreme: same shape shifted to Wed"},
    {"id": "c3", "expr": "consolidation_thursday_reversal: sideways Mon-Wed, Thu Judas Swing reversal"},
    {"id": "c4", "expr": "consolidation_midweek_rally_decline: extreme Tue, Wed extends it, reverses before Thu"},
    {"id": "c5", "expr": "seek_and_destroy: two-sided sweep, no trend, thin-liquidity/FOMC/holiday trigger"},
    {"id": "c6", "expr": "wednesday_weekly_reversal: sideways Mon-Tue, Wed London sweeps SSL/BSL then reverses hard"}
  ],
  "timeframes": ["H4","D","W"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["weekly-quarters","weekly-bias","judas-swing","true-week-open","tgif-weekly-po3","htf-amd"],
  "sources": ["THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE"]
}
```

## Visual Pattern

```
   #1 Classic Tuesday          #3 Consolidation Thu Reversal
   M  Tu  W  Th  F             M  Tu  W  Th  F
   ‾\_/‾‾‾‾‾‾‾‾‾‾               ~~~~~~~~~~\___
      (Tue = extreme)                      (Thu Judas reverses)

   #6 Wednesday Weekly Reversal
   M  Tu  W        Th  F
   ~~~~~ \___/‾‾‾‾‾‾‾‾‾‾
         (Wed London sweep + reversal)
```

## Timeframes

H4 / D for spotting which day printed the extreme; W for confirming the overall shape once the week closes.

## Examples

**Example 1 — source's own diagrammed case, Classic Tuesday Low (p.561):** Monday builds a tight accumulation range (neither week extreme). Tuesday sweeps SSL, prints an FVG/OB, Judas Swing reverses — that low holds as the week's low. Matches Pattern #1 exactly, including the source's own Judas Swing framing.

## Common Mistakes

- **Conflating #2 (Wednesday Low/High of Week) with #6 (Wednesday Weekly Reversal).** Both put the week's turning point on Wednesday, but #2 is purely a *when* claim (the extreme happens to land Wednesday instead of Tuesday); #6 is a *mechanism* claim (a specific Monday–Tuesday sideways setup, then a London-session liquidity sweep drives the reversal). A Wednesday extreme satisfying #6's sweep mechanic also satisfies #2's day-of-week claim — they aren't mutually exclusive, but treat #6 as the more specific, evidence-demanding read.
- **Forcing a week into one of these six shapes.** Same caution as [weekly-quarters](weekly-quarters.md)'s own Common Mistakes — not every week fits a named pattern.
- **Treating #5 (Seek & Destroy) as a tradeable setup.** It names the *conditions that break every other pattern*, not a pattern to trade toward.

## Related Concepts

- [weekly-quarters](weekly-quarters.md) — the single default shape this taxonomy's six patterns supplement; see its own "~50% of weeks" caveat.
- [weekly-bias](../25-htf-bias/weekly-bias.md) — its "Tuesday lows on bullish weeks" adage is this file's Pattern #1.
- [judas-swing](../13-judas-swing/judas-swing.md) — the mechanic behind Patterns #1, #3, and #6.
- [true-week-open](true-week-open.md) — the weekly reference level several of these patterns measure sweeps and reversals against.
- [tgif-weekly-po3](../31-models/tgif-weekly-po3.md) — a separate, specific Friday setup; not one of these six patterns (see that file's reconciliation note against this source's general "don't trade Friday" guidance).

## Citations

- `THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE` — six named weekly profile diagrams, pp.566–571.

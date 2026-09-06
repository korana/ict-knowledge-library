# Central Bank Dealing Range (CBDR)

**Category:** 04-time-cycles
**Aliases:** CBDR, Central Bank Dealer Range
**ICT Confidence:** high
**Year Introduced:** 2016
**Year Refined:** 2026
**Source IDs:** ICT-2016-KILLZONES, THAI-COMMUNITY-2026-SESSION-KILLZONE, THAI-COMMUNITY-2026-CBDR, THAI-COMMUNITY-2026-ASIAN-RANGE, THAI-COMMUNITY-2026-STD-PROJECTION
**Tags:** time, cbdr, session, foundational

## Definition

The Central Bank Dealing Range (CBDR) is the **14:00–20:00 NY time window** during which price is expected to consolidate in a tight, sideways range while major central-bank dealing desks handle end-of-day price delivery. ICT teaches the CBDR as a **projection base**: its own range (high to low) is projected outward in Standard Deviation multiples to anticipate where the *next* day's high and low are likely to form — typically inside [london-open-killzone](../10-killzones/london-open-killzone.md). It sits between the NY PM killzone/session (ending ~16:00) and the Asian killzone (starting 20:00) — see [killzone-times-table](../10-killzones/killzone-times-table.md) for how it fits alongside the canonical killzone windows.

## Formal Criteria

- Time window: 14:00 → 20:00 NY.
- Expected behavior: sideways / consolidating — not a breakout window.
- Falls between NY PM's active delivery hours and the start of the Asian killzone.
- **Validity band (community-attributed):** the source states the CBDR range should fall within **200–400 "จุด"** — literally "points," MT4/MT5 broker-point terminology, not a pip figure and not scoped to any instrument (the source names none; a "major FX pairs" instrument scope was wrongly attributed here in an earlier version of this file — corrected, see Citations). Above ~400 points the source says not to use CBDR at all that day — the fallback is to use the **Asian Range** (20:00–00:00 NY) as the projection base instead, via [asian-range-projections](../14-asian-range/asian-range-projections.md)'s existing extension-target system. See [asian-range](../14-asian-range/asian-range.md); that file is unchanged by this — the fallback is a CBDR usage rule, not an Asian Range property. On a standard 5-digit FX feed, 10 points = 1 pip, so 200–400 points ≈ 20–40 pips — in that reading the band lands close to this wiki's own Asian range size figure (25–60 pips EURUSD); on an index/commodity feed, points are typically the native display unit already (see the Example below). Recorded in points, as the source states it, rather than silently converted to an assumed unit.
- **Standard Deviation (STD) projection (community-attributed):** the CBDR range is projected in **1–4 STD** multiples both above and below the range, where 1 STD = 1× the CBDR range width. Levels *above* the CBDR are read as Sell Day / high-of-day targets; levels *below* are read as Buy Day / low-of-day targets. The next day's actual high or low normally lands at the **1–2 STD** level; a print reaching **3–4 STD** is read as a sign of news-driven expansion rather than the ordinary case.
- This is a **separate anchor system** from [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md): that file's SD levels are negative-fib extensions (−1.5/−2.0/−2.5/−4.0) anchored to a *swing leg*; CBDR's STD levels are plain integer multiples of a *time-bounded range* (14:00–20:00 NY), anchored differently and symmetric on both sides. Don't conflate the two — cross-check which anchor a given "SD"/"STD" reference means.
- **"Crisis Standard Deviation" (community-attributed name for the >4 STD regime):** a later chapter by the same author names the extreme case this file's own >4-STD "news-expansion" note already anticipated — a worked example prints past 6.5 STD, and the source calls that regime "Crisis Standard Deviation." Same >4 threshold, now with the source's own name attached. See [flout-range](flout-range.md), which shares this same STD mechanic on a combined CBDR+Asian window and carries the same >4 naming.

## Formula / Math

```
cbdr_window = [14:00, 20:00] NY

cbdr_high = highest_high(cbdr_window)
cbdr_low  = lowest_low(cbdr_window)
cbdr_range = cbdr_high - cbdr_low

# Validity band (community-attributed) — below this, treat CBDR as too
# tight to be meaningful; above it, fall back to the Asian Range instead.
# Units are the source's own "points" (MT4/MT5 broker points), NOT pips —
# on a 5-digit FX feed 10 points = 1 pip, so this is ~20-40 pips for FX;
# on an index/commodity feed points are usually the native unit already.
valid_range_points = [200, 400]
if cbdr_range_points > 400:
    use asian_range (20:00-00:00 NY) as the projection base instead

# CBDR-anchored Standard Deviation (STD) projection — 1x..4x the CBDR
# range itself, NOT the swing-leg-anchored fib SD system in
# standard-deviation-projections.md.
for n in [1, 2, 3, 4]:
    std_up[n]   = cbdr_high + n * cbdr_range   # Sell Day / HOD target zone
    std_down[n] = cbdr_low  - n * cbdr_range   # Buy Day  / LOD target zone

# Typical case: next day's HOD/LOD forms at std_up[1..2] or std_down[1..2].
# 3-4 STD prints are read as a news-expansion day, not the base case.
```

## Machine-Readable

```json
{
  "id": "central-bank-dealing-range",
  "category": "04-time-cycles",
  "aliases": ["CBDR", "Central-Bank-Dealer-Range"],
  "criteria": [
    {"id": "c1", "expr": "time_in [14:00, 20:00] NY"},
    {"id": "c2", "expr": "expected_behavior == sideways_consolidation"},
    {"id": "c3", "expr": "used_as_next_day_projection_base == true"},
    {"id": "c4", "expr": "valid_range_points in [200, 400], else fallback_to == asian_range"},
    {"id": "c5", "expr": "std_projection == cbdr_range * n, n in [1,2,3,4], symmetric_up_and_down"}
  ],
  "timeframes": ["M15","H1","H4"],
  "confidence": "high",
  "year_introduced": "2016",
  "year_refined": "2026",
  "related": ["killzone-times-table","ny-pm-killzone","asia-killzone","ipda-definition","true-day-open","draw-on-liquidity","standard-deviation-projections","asian-range","asian-range-projections","london-open-killzone","flout-range"],
  "sources": ["ICT-2016-KILLZONES","THAI-COMMUNITY-2026-SESSION-KILLZONE","THAI-COMMUNITY-2026-CBDR","THAI-COMMUNITY-2026-ASIAN-RANGE","THAI-COMMUNITY-2026-STD-PROJECTION"]
}
```

## Visual Pattern

```
   13:30 ── 14:00 ─────────────── 20:00 ── 20:00 (Asia KZ starts)
             |     sideways/         |
             |     consolidating     |
             ────── CBDR ────────────
             14:00 – 20:00 NY
                (range used to project next day's target)

   Next-day STD projection (community-attributed):

   std_up[4]  ────────────────  4 STD (news-expansion territory)
   std_up[3]  ────────────────  3 STD
   std_up[2]  ────────────────  2 STD  ┐ typical HOD/LOD
   std_up[1]  ────────────────  1 STD  ┘ lands here (often in
   cbdr_high  ═══ CBDR range ═══        London Open killzone)
   cbdr_low   ═══════════════════
   std_down[1] ───────────────  1 STD  ┐
   std_down[2] ───────────────  2 STD  ┘
   std_down[3] ───────────────  3 STD
   std_down[4] ───────────────  4 STD (news-expansion territory)
```

## Timeframes

M15 / H1 / H4 — the range itself is measured on lower TFs but read as a single reference block for next-day projection.

## Examples

**Example 1 — CBDR STD projection (bearish day):**
- 14:00–20:00 NY: US30 ranges 39,000–39,250 (CBDR high 39,250, CBDR low 39,000, range 250 points — inside the 200–400 validity band).
- STD levels: std_down[1] = 38,750, std_down[2] = 38,500, std_down[3] = 38,250, std_down[4] = 38,000; std_up[1] = 39,500, std_up[2] = 39,750.
- Next day: Asia and early London trade inside the CBDR range; during [london-open-killzone](../10-killzones/london-open-killzone.md), price sells off and prints the day's low at 38,540 — inside the std_down[1]–std_down[2] zone, the ordinary case rather than a 3–4 STD news day.
- (Source shows both a bearish, p.460, and a bullish, p.461, worked example sharing this same structure — one kept here, both pages cited.)

## Common Mistakes

- **Trading CBDR as a breakout window.** ICT's framing is the opposite — CBDR is expected to be quiet/sideways; treat activity inside it as noise, not signal.
- **Confusing CBDR with a killzone.** The source itself lists CBDR alongside its five killzones (see Related Concepts), but this wiki's canonical killzone-overview.md five-killzone list uses NY PM in that time slot instead — CBDR (14:00–20:00) and NY PM killzone (13:30–16:00) overlap only partially and are not the same window.
- **Conflating CBDR's STD system with the swing-leg SD system.** [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md) and CBDR's STD levels are both called "SD"/"STD" in ICT community usage but use different anchors (swing leg vs. time-bounded range) and different multiples — check which one a given reference means before applying it.
- **Projecting from a CBDR range outside the 200–400 point validity band** — or silently reading "point" as "pip." Too tight or too wide (news-distorted) ranges aren't treated as reliable projection bases by the source; use the Asian Range fallback above ~400 points instead of projecting from a CBDR range regardless of its width, and convert units per feed (10 points = 1 pip on 5-digit FX; native units on most index/commodity feeds) rather than assuming.
- **Treating a 3–4 STD print as the base case.** The source frames 1–2 STD as where the day's high/low normally lands; 3–4 STD is explicitly the news-expansion exception, not a routine target.

## Related Concepts

- [killzone-times-table](../10-killzones/killzone-times-table.md) — CBDR's parent reference table.
- [ny-pm-killzone](../10-killzones/ny-pm-killzone.md), [asia-killzone](../10-killzones/asia-killzone.md) — the killzones CBDR sits between.
- [london-open-killzone](../10-killzones/london-open-killzone.md) — where the next day's projected HOD/LOD typically prints.
- [ipda-definition](../23-ipda/ipda-definition.md) — the broader algorithmic-delivery framework CBDR is presented as part of.
- [true-day-open](../22-quarterly-theory/true-day-open.md) — another time-anchored reference in the same daily-cycle family.
- [draw-on-liquidity](../02-liquidity/draw-on-liquidity.md) — the general next-target-projection concept CBDR's range feeds into.
- [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md) — a different SD/STD system (swing-leg-anchored); see the disambiguation note above.
- [asian-range](../14-asian-range/asian-range.md) — CBDR's fallback projection base when the CBDR range exceeds ~400 points; [asian-range-projections](../14-asian-range/asian-range-projections.md) — the extension-target system that fallback actually uses.
- [flout-range](flout-range.md) — a later-chapter sibling: the same STD mechanic on a combined CBDR+Asian window.

## Citations

- `ICT-2016-KILLZONES` — CBDR presented as part of the same killzone/session time-table family this Source ID already covers.
- `THAI-COMMUNITY-2026-SESSION-KILLZONE` — CBDR window (14:00–20:00 NY), sideways-consolidation behavior, and next-day-projection use, pp.447–448, 451.
- `THAI-COMMUNITY-2026-CBDR` — 200–400 *point* validity band and Asian Range fallback, p.457, p.462; CBDR-anchored 1–4 STD projection system and worked examples, pp.458–461.
- `THAI-COMMUNITY-2026-ASIAN-RANGE` — unit correction, p.469: re-reading the CBDR chapter's own p.457 wording ("200-400 จุด," no instrument named) against this chapter's identical "200-400 จุด" figure for the Asian range's own typical size confirmed "จุด" means MT4/MT5 points, not pips — an earlier version of this file (commit `c8b6f9d`) mis-rendered it as "200–400 pip validity band (major FX pairs)," an instrument scope and unit the source never states. Corrected here rather than silently; the worked Example below was already stated in points and needed no change.
- `THAI-COMMUNITY-2026-STD-PROJECTION` — "Crisis Standard Deviation" naming for the >4 STD regime, worked example reaching 6.5 STD, p.531.

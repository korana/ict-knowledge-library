# Flout Range (Flout Standard Deviation)

**Category:** 04-time-cycles
**Aliases:** Flout STD, Flout Standard Deviation, Flout Range
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-STD-PROJECTION
**Tags:** time, flout, cbdr, asian-range, community-attributed

## Definition

The **Flout Range** is a 2026 community-attributed time-bounded range that spans **14:00–00:00 NY** — the union of [central-bank-dealing-range](central-bank-dealing-range.md)'s window (14:00–20:00) and the Asian killzone window (20:00–00:00, see [asian-range](../14-asian-range/asian-range.md)) — measured and projected as a single combined range rather than two separate ones. It is not an ICT-original term; no prior Source ID in this wiki uses it. The source presents it as a third member of the same STD-projection family as CBDR and Asian-Range STD (see [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md)'s disambiguation note for why this is a *different* anchor system from that file's swing-leg SD levels): a **wider, combined base range** for the same day-trade target-finding purpose, used when the narrower CBDR-only or Asian-only range is preferred to be read as one continuous block instead of two.

## Formal Criteria

- Time window: **14:00 → 00:00 NY** (10 hours) — CBDR start through Asian killzone close.
- High/low taken across the **entire combined window**, not per sub-session.
- Same Standard Deviation projection mechanic as CBDR: project the Flout range in **1–4× multiples**, symmetric above and below.
- **1–3 STD is the typical case; a print past 4 STD is flagged as abnormal** ("ราคาการวิ่งนั้นไม่ปกติ") — same threshold framing as CBDR's own 1–2 (typical) vs. 3–4 (news-expansion) split, though this source states the abnormal cutoff at >4 rather than >2.
- The source situates confirmation/read of Flout STD projections around the **London (Session) Killzone**, the same window CBDR's own next-day HOD/LOD projections typically land in.

## Formula / Math

```
flout_window = [14:00, 00:00] NY   # CBDR window ∪ Asian killzone window

flout_high = highest_high(flout_window)
flout_low  = lowest_low(flout_window)
flout_range = flout_high - flout_low

for n in [1, 2, 3, 4]:
    std_up[n]   = flout_high + n * flout_range
    std_down[n] = flout_low  - n * flout_range

# 1-3 STD: typical case. >4 STD: abnormal / "Crisis Standard Deviation"
# territory — see central-bank-dealing-range.md's own >4 STD naming.
```

## Machine-Readable

```json
{
  "id": "flout-range",
  "category": "04-time-cycles",
  "aliases": ["Flout-STD", "Flout-Standard-Deviation"],
  "criteria": [
    {"id": "c1", "expr": "time_in [14:00, 00:00] NY"},
    {"id": "c2", "expr": "combined_range == cbdr_window union asian_killzone_window"},
    {"id": "c3", "expr": "std_projection == flout_range * n, n in [1,2,3,4], symmetric_up_and_down"},
    {"id": "c4", "expr": "typical_case: n in [1,3]; abnormal: n > 4"}
  ],
  "timeframes": ["M15","H1","H4"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["central-bank-dealing-range","asian-range","standard-deviation-projections","london-open-killzone","asian-range-projections"],
  "sources": ["THAI-COMMUNITY-2026-STD-PROJECTION"]
}
```

## Visual Pattern

```
   14:00 ─────────── 20:00 ─────────── 00:00 NY
         │  CBDR      │    Asian KZ    │
         └──────── Flout Range ────────┘
                (one combined high/low)

   std_up[4]   ── 4 STD (abnormal, "Crisis" territory)
   std_up[1-3] ── typical HOD/LOD zone
   flout_high  ══════════════════════
   flout_low   ══════════════════════
   std_down[1-3]
   std_down[4]  ── 4 STD (abnormal)
```

## Timeframes

M15 / H1 / H4 — range measured on lower TFs, read as a single block for next-window projection, same as CBDR.

## Common Mistakes

- **Reading Flout as a replacement for CBDR or Asian Range individually.** It's a *combined* anchor, not a substitute — the source presents all three (Asia STD, CBDR STD, Flout STD) as siblings for the same day-trade target-finding purpose, not a hierarchy.
- **Conflating "Flout" with any ICT-original term.** No prior Source ID in this wiki uses it; treat as this source's own coinage until corroborated elsewhere.
- **Missing the >4 STD naming.** See [central-bank-dealing-range](central-bank-dealing-range.md)'s "Crisis Standard Deviation" note — the same source names the extreme-STD regime, and it applies to Flout's own >4 case too.

## Related Concepts

- [central-bank-dealing-range](central-bank-dealing-range.md) — one of the two windows Flout combines; shares the same STD-multiple mechanic.
- [asian-range](../14-asian-range/asian-range.md) — the other window Flout combines.
- [standard-deviation-projections](../28-fibonacci-levels/standard-deviation-projections.md) — the differently-anchored swing-leg SD system; see its disambiguation note.
- [london-open-killzone](../10-killzones/london-open-killzone.md) — where the source reads/confirms Flout STD projections, same as CBDR's own next-day projections.

## Citations

- `THAI-COMMUNITY-2026-STD-PROJECTION` — Flout Range definition, window, and STD mechanic, pp.530–533; "Crisis Standard Deviation" naming for the >4 STD regime (worked example reaching 6.5 STD), p.531.

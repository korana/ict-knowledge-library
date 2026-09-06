# TGIF (Weekly Power of Three Projection)

**Category:** 31-models
**Aliases:** TGIF, Weekly PO3 Projection, Thank God It's Friday setup
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-STD-PROJECTION
**Tags:** model, weekly, friday, po3, community-attributed

## Definition

**TGIF** is a 2026 community-attributed weekly-scale setup: on **Friday, during the London Killzone** (occasionally London Silver Bullet or NY Killzone instead), price sweeps the liquidity resting at **Thursday's high or low (BSL/SSL)**, lining up with a **weekly- or daily-scale HTF FVG/POI** formed earlier in the week, then retraces into that FVG to roughly its **20–30% level** (occasionally to 40%, never past 50%) before the week closes. Reaching that zone is what the source calls **"TGIF Success."** It is presented as the [power-of-three](../12-power-of-three/power-of-three.md) doctrine applied at weekly scale — Monday-through-Thursday builds the week's directional POI, Friday is the Distribution-phase retracement into it — and as the specific mechanic behind [weekly-quarters](../22-quarterly-theory/weekly-quarters.md)'s Friday row, which this wiki previously carried only as an unelaborated "profit-taking / week's structure often resolves" placeholder.

**Confidence caveat, in the source's own words:** the author states this setup is "ค่อนข้างแม่นยำ" (fairly accurate) from backtesting but explicitly adds **"แต่ผมยังไม่เคยใช้จริงนะ"** — "but I've never actually used it live." Confidence is set `community-attributed` rather than `high` specifically because of this self-disclaimer; treat as backtested-only, not live-validated.

## Formal Criteria

- Applies once per week, Friday only; not guaranteed to occur every week.
- Directional read: if the week is expected to print its high on Friday, look for it during the London Killzone; symmetric for a Friday low.
- Requires a **weekly- or daily-timeframe FVG/POI** already present from earlier in the week (Monday–Thursday) as the retracement target.
- Trigger: Friday sweeps **Thursday's BSL or SSL** (the liquidity resting at Thursday's high/low), lining up with that HTF FVG.
- Target zone: **0.25–0.30** (20–30%) retracement into the FVG from the swept extreme; the source allows up to **0.40** in some cases but treats **0.50** as a hard ceiling — beyond that is not read as TGIF.
- Primary window: **London Killzone**. Named alternates when London Killzone doesn't produce it: **New York Killzone** or **London Silver Bullet** time.

## Formula / Math

```
tgif_candidate := day == Friday
                  AND htf_fvg_poi exists (from Mon-Thu, D or W scale)
                  AND friday_sweeps(thursday_high_or_low)   # BSL or SSL
                  AND retracement_into_fvg in [0.20, 0.30]  # up to 0.40 seen, 0.50 = ceiling
                  AND window in {london_killzone, ny_killzone, london_silver_bullet}

tgif_success := tgif_candidate AND price_reaches(retracement_zone)
```

## Machine-Readable

```json
{
  "id": "tgif-weekly-po3",
  "category": "31-models",
  "aliases": ["TGIF", "Weekly-PO3-Projection"],
  "criteria": [
    {"id": "c1", "expr": "friday_only == true"},
    {"id": "c2", "expr": "requires_htf_fvg_poi_from_mon_thu == true"},
    {"id": "c3", "expr": "trigger == sweep(thursday_BSL_or_SSL)"},
    {"id": "c4", "expr": "target_zone == 0.20-0.30 retracement into FVG, ceiling 0.50"},
    {"id": "c5", "expr": "window in [london_killzone, ny_killzone, london_silver_bullet]"}
  ],
  "timeframes": ["M30","H1","H4","D","W"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["power-of-three","htf-amd","weekly-quarters","weekly-bias","fair-value-gap","draw-on-liquidity","london-open-killzone","silver-bullet-london","ny-am-killzone"],
  "sources": ["THAI-COMMUNITY-2026-STD-PROJECTION"]
}
```

## Visual Pattern

```
   Mon    Tue    Wed    Thu         Fri (London KZ)
   ─── week builds a weekly/daily FVG somewhere in here ───
                          │ Thu BSL/SSL
                          ▼
                     Friday sweeps it ──► retraces into FVG
                                          to 0.20-0.30 (up to 0.40)
                                          = "TGIF Success"
                                          (never past 0.50)
```

## Timeframes

M30 for tracking the week's day-by-day trend; H1/H4 for the HTF FVG/POI and the Thursday-sweep entry; D/W for confirming the FVG is a genuine weekly- or daily-scale POI, not an intraday one.

## Examples

**Example 1 — Friday low, per the source's worked H4/Daily walkthrough (pp.537–543):** a bearish week builds a weekly-scale FVG as HTF POI by midweek. Thursday prints a high; Friday, during London Killzone, sweeps that Thursday high (BSL), then sells off back into the weekly FVG, reaching its 0.25–0.3 zone before the week closes — logged as TGIF Success.

## Common Mistakes

- **Treating this as a contradiction of "don't trade Friday."** A later chapter by the same author gives the general instruction that Monday and Friday shouldn't be traded (tight, choppy range; see [weekly-quarters](../22-quarterly-theory/weekly-quarters.md)'s Friday note). That's a broader caution against trend-trading a quiet day, not a blanket ban — TGIF is the one specific, narrow setup this source carves out of that same Friday.
- **Expecting TGIF every week.** The source is explicit this doesn't happen every week — it's a recognizable pattern, not a weekly guarantee.
- **Chasing past the 0.50 ceiling.** The source draws a hard line at 50% retracement; beyond that is not this setup.
- **Treating this as live-validated.** The author's own disclaimer (see Definition) — backtested, not personally traded live. Weight accordingly.
- **Skipping the Thursday-sweep precondition.** TGIF isn't just "Friday retraces into an FVG" — the source requires the Thursday BSL/SSL sweep as the trigger that lines the day up with the target FVG.

## Related Concepts

- [power-of-three](../12-power-of-three/power-of-three.md) — the AMD doctrine this file applies at weekly scale.
- [htf-amd](../12-power-of-three/htf-amd.md) — the existing weekly/monthly AMD mapping this setup is a Friday-specific elaboration of.
- [weekly-quarters](../22-quarterly-theory/weekly-quarters.md) — its Friday row ("closing / profit-taking, week's structure often resolves") is the placeholder this file supplies the mechanic for.
- [weekly-bias](../25-htf-bias/weekly-bias.md) — the broader weekly-bias context TGIF operates inside.
- [fair-value-gap](../06-fair-value-gaps/fair-value-gap.md) — the HTF POI type this setup retraces into.
- [draw-on-liquidity](../02-liquidity/draw-on-liquidity.md) — the Thursday BSL/SSL sweep is a DOL-take in miniature.
- [london-open-killzone](../10-killzones/london-open-killzone.md), [silver-bullet-london](../11-silver-bullet/silver-bullet-london.md), [ny-am-killzone](../10-killzones/ny-am-killzone.md) — the three named windows TGIF can resolve in.

## Citations

- `THAI-COMMUNITY-2026-STD-PROJECTION` — TGIF definition, method, and confidence disclaimer, pp.534–535; worked Step-by-Step walkthrough (M30, H4, Daily, H1/Weekly), pp.536–543. Note: the chapter's connective prose around the core mechanic (pp.534, 539) was substantially garbled in OCR; only the clearly legible mechanic (Thursday-sweep → FVG retracement to 0.20–0.30, 0.50 ceiling, three named windows) was kept.

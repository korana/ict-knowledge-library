# Standard Deviation Projections

**Category:** 28-fibonacci-levels
**Aliases:** SD projections, fib projection targets, ICT projection levels
**ICT Confidence:** high
**Year Introduced:** 2017
**Year Refined:** 2026
**Source IDs:** ICT-2017-OTE, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-ORDER-BLOCK, THAI-COMMUNITY-2026-CBDR, THAI-COMMUNITY-2026-STD-PROJECTION
**Tags:** fibonacci, projections, targets, sd

## Definition

Standard Deviation projections are ICT's measured-leg extension targets — price levels **beyond** the original swing leg's destination, calculated as multiples of the leg's size. ICT uses negative fib ratios (−1.5, −2.0, −2.5, −4.0, and an extreme −5.0) to denote extension beyond the leg. These are **target levels**, not entries: when an OTE entry is taken, SD projections answer "where might price reach?" The most-cited targets are −1.5 SD (first extension) and −2.0 SD (typical full-delivery target).

## Formal Criteria

- Anchor: the same swing leg used for retracement (start → end).
- Each negative fib ratio extends past `leg_end` by that multiple of `leg_size`.
- Standard projection set: −1.5, −2.0, −2.5, −4.0.
- Extreme: −4.0 used for major reversal-anchor targets (rarely reached in a single trade). A 2026 community source additionally cites −5.0 as an observed extreme extension (see Examples) — treat as a rare-case extension beyond the standard set, not a new default target.
- **Not the same system as CBDR's STD projection.** [central-bank-dealing-range](../04-time-cycles/central-bank-dealing-range.md) uses a differently-anchored "STD" — plain integer multiples of a time-bounded range (14:00–20:00 NY), not a swing-leg-anchored negative-fib extension. Same abbreviation, different mechanic; don't conflate the two.
- **A dedicated 2026 community source confirms this exact disambiguation from the other direction** — the same author names both systems "STDv" in one chapter, then measures them from two different anchors: a **2.0–2.5 / 4.0–4.5** magnitude pair anchored to the **swing leg from the Manipulation phase's most recent Lower High (bearish) or Higher Low (bullish) out to a significant HTF POI / the MSS+Displacement point** — this file's family — versus the CBDR/Asian/Flout-Range "STDv" family, which stays integer-multiples-of-a-time-bounded-range (see [central-bank-dealing-range](../04-time-cycles/central-bank-dealing-range.md), [flout-range](../04-time-cycles/flout-range.md)). Same word, two anchors, one author — the strongest evidence yet for keeping the two systems separate.
- **This source also reads the 2.0–2.5 / 4.0–4.5 zone as a signal, not only a target.** Price reaching it is used to locate where **Retracement or Reversal** is likely, in addition to the usual target/R:R role — a broader use than "target levels, not entries" alone.
- **The 2.0–2.5 / 4.0–4.5 pair's own anchor (community-attributed):** the most recent **Lower High** (bullish context) or **Higher Low** (bearish) formed during the [manipulation-phase](../12-power-of-three/manipulation-phase.md), measured out to a **significant HTF POI** / the MSS+Displacement point — still a swing leg, just a differently-sourced one than the OTE leg above. Workflow (M5–M15 preferred): mark [true-day-open](../22-quarterly-theory/true-day-open.md); the day's HOD/LOD normally sets inside the Asian Session / [central-bank-dealing-range](../04-time-cycles/central-bank-dealing-range.md) / [flout-range](../04-time-cycles/flout-range.md) windows; wait for price to pull back through the [london-open-killzone](../10-killzones/london-open-killzone.md); mark the Manipulation-phase LH/HL that London Killzone fails to break; wait for MSS + Displacement; then measure 2.0–2.5 / 4.0–4.5 from that leg. Recurs across the source's [power-of-three](../12-power-of-three/power-of-three.md) Accumulation/Manipulation/Distribution mapping — Accumulation's own Stop Hunt is described at the London-Session-anchored version of the same 2.0–2.5 level.

## Formula / Math

```
leg_size = leg_end - leg_start

project(level) = leg_end - level * leg_size      # negative level extends past leg_end

# Bullish leg 1.0800 → 1.0900 (leg_size = 100):
SD_-1_5 = 1.0900 - (-1.5) * 100 = 1.0900 + 150 = 1.1050
SD_-2_0 = 1.0900 + 200 = 1.1100
SD_-2_5 = 1.0900 + 250 = 1.1150
SD_-4_0 = 1.0900 + 400 = 1.1300

# Community-attributed 2.0-2.5 / 4.0-4.5 pair (different leg source,
# same negative-fib mechanic): leg = Manipulation-phase LH/HL -> HTF POI.
```

## Machine-Readable

```json
{
  "id": "standard-deviation-projections",
  "category": "28-fibonacci-levels",
  "aliases": ["SD-projections", "fib-projection-targets", "ICT-projection-levels"],
  "criteria": [
    {"id": "c1", "expr": "projection_levels = [-1.5, -2.0, -2.5, -4.0]"},
    {"id": "c2", "expr": "anchored_to_same_leg_as_retracement == true"},
    {"id": "c3", "expr": "community variant: leg = manipulation LH/HL -> HTF POI, levels 2.0-2.5 / 4.0-4.5, also read as retracement/reversal signal"}
  ],
  "timeframes": ["M5","M15","H1","H4","D","W"],
  "confidence": "high",
  "year_introduced": "2017",
  "year_refined": "2026",
  "related": ["ict-fib-overview","symmetrical-price-projections","fib-62","fib-705","fib-79","draw-on-liquidity","external-range-liquidity","cisd","central-bank-dealing-range","flout-range","manipulation-phase","power-of-three"],
  "sources": ["ICT-2017-OTE","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-ORDER-BLOCK","THAI-COMMUNITY-2026-CBDR","THAI-COMMUNITY-2026-STD-PROJECTION"]
}
```

## Visual Pattern

```
                              ─── -4.0 SD (extreme)
                              ─── -2.5 SD
                              ─── -2.0 SD (typical full-delivery)
                              ─── -1.5 SD (first extension)
   leg_end ─────────  ← 0.0
   ─── 0.50 (EQ) ──
   ─── 0.62 ────── (OTE retracement zone)
   ─── 0.705 ────
   ─── 0.79 ────
   leg_start ─────  ← 1.0
```

## Timeframes

All TFs. HTF SD projections often align with HTF DOL (PWH, PMH, etc.) — when an SD level coincides with an existing liquidity pool, conviction increases.

## Examples

**Example 1 — partial-take ladder using SD projections:**
- Leg 1.0800 → 1.0900.
- OTE entry at 0.705 = 1.08295.
- TP ladder:
  - TP1: -1.5 SD = 1.1050 (~22.7R from a 15-pip risk)
  - TP2: -2.0 SD = 1.1100
  - Final: -2.5 SD = 1.1150 if extended delivery
- Often coincides with PWH (e.g., 1.1095) → confirms TP2 zone as a real liquidity destination.

**Example 2 — extreme extension to −4/−5 SD (per a 2026 community source, p.226):** a worked CISD-anchored trade shows price running the full extension all the way to between −4.0 and −5.0 SD before reversing — offered as evidence that −5.0 is worth keeping on the chart as a rare-case extreme, not a routine target.

## Common Mistakes

- **Using full classical projection set.** Classical 1.272, 1.618, 2.618 don't map to ICT's −1.5/−2.0/−2.5/−4.0. Pick one framework.
- **Treating SD targets as guarantees.** They are areas of interest. Some setups never reach -1.5; others fly past -4.0 on news.
- **Ignoring HTF DOL.** A nearby HTF liquidity pool often resolves before the SD target; check for collisions.

## Related Concepts

- [ict-fib-overview](ict-fib-overview.md), [symmetrical-price-projections](symmetrical-price-projections.md).
- [fib-62](fib-62.md), [fib-705](fib-705.md), [fib-79](fib-79.md).
- [draw-on-liquidity](../02-liquidity/draw-on-liquidity.md), [external-range-liquidity](../02-liquidity/external-range-liquidity.md).
- [cisd](../07-order-blocks/cisd.md) — a related OB variant that uses SD extensions as an alternative target framing.
- [central-bank-dealing-range](../04-time-cycles/central-bank-dealing-range.md), [flout-range](../04-time-cycles/flout-range.md) — differently-anchored "STD"/"STDv" projection systems; see the disambiguation note above.
- [manipulation-phase](../12-power-of-three/manipulation-phase.md), [power-of-three](../12-power-of-three/power-of-three.md) — the community-attributed 2.0–2.5/4.0–4.5 pair's own leg source.

## Citations

- `ICT-2017-OTE`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-ORDER-BLOCK` — −5.0 SD extreme-extension example, p.226.
- `THAI-COMMUNITY-2026-CBDR` — disambiguation cross-reference against CBDR's own, differently-anchored STD projection system, pp.458–461.
- `THAI-COMMUNITY-2026-STD-PROJECTION` — the 2.0–2.5/4.0–4.5 community-attributed pair, its Manipulation-LH/HL-to-HTF-POI anchor, and the retracement/reversal-signal framing, pp.544–545, 549–553, 556–557.

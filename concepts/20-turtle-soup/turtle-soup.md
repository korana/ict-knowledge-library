# Turtle Soup

**Category:** 20-turtle-soup
**Aliases:** TS, false breakout, failed breakout, breakout-fade, fakeout (SMC), swing failure (SMC)
**ICT Confidence:** high
**Year Introduced:** 2018
**Year Refined:** 2026
**Source IDs:** ICT-2017-CHARTER-OVERVIEW, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-TURTLE-SOUP
**Tags:** turtle-soup, false-breakout, foundational

## Definition

A **Turtle Soup** is a **failed breakout** pattern — price briefly trades through a known liquidity level (a swing high/low or session extreme), traps breakout traders, and immediately reverses back inside. Named after the original "Turtle Trader" breakout strategy that this pattern explicitly defeats. The Turtle Soup is the price-action mirror of a [liquidity-sweep](../02-liquidity/liquidity-sweep.md): the sweep is the event, the Turtle Soup is the named pattern. ICT borrowed the term from Larry Connors' original 1998 work and integrated it into the ICT framework as a high-probability reversal setup.

## Formal Criteria

A bullish Turtle Soup (failed bearish breakout):

- Price has been respecting a known SSL (swing low, EQL, session low).
- Price wicks below the SSL.
- The same candle (or within 1–3 bars) closes back above the SSL.
- Subsequent displacement upward confirms the failed breakout.

For bearish: symmetric (failed bullish breakout).

## Formula / Math

```
bullish_turtle_soup := low(n) < known_SSL_level
                       AND close(n+k) > known_SSL_level   for k in [0, 3]
                       AND post-event displacement is up

bearish_turtle_soup := high(n) > known_BSL_level
                       AND close(n+k) < known_BSL_level   for k in [0, 3]
                       AND post-event displacement is down
```

## Machine-Readable

```json
{
  "id": "turtle-soup",
  "category": "20-turtle-soup",
  "aliases": ["TS", "false-breakout", "failed-breakout", "breakout-fade", "fakeout", "swing-failure"],
  "criteria": [
    {"id": "c1", "expr": "wick_through_known_level == true"},
    {"id": "c2", "expr": "close_back_inside_within_few_bars == true"},
    {"id": "c3", "expr": "post-event displacement opposite to break direction"}
  ],
  "timeframes": ["M5","M15","H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2018",
  "year_refined": "2026",
  "related": ["bullish-turtle-soup","bearish-turtle-soup","stop-hunt-pattern","liquidity-sweep","liquidity-run","stop-run-definition","rejection-block","judas-swing","power-of-three","equal-highs","equal-lows","fvg-setup-checklist"],
  "sources": ["ICT-2017-CHARTER-OVERVIEW","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-TURTLE-SOUP"]
}
```

## Visual Pattern

```
   bullish Turtle Soup:                 bearish Turtle Soup:

   resistance level                     ▲   ← wick above resistance
   ─────────                            █   ← close back inside
        │                            ───────
        │  (price respecting)
   support level                        support level
   ─────────                            ─────────
   ──╲   ←  wick below                          (price respecting)
     ╲╱   ← close back above            ▼  resistance level
        ──→ rally up                    ─────────
                                        ──╲  wick above
                                          ╲╱  close back inside
                                              ──→ sell-off
```

## Timeframes

All TFs M5+.

## Examples

**Example 1 — bullish Turtle Soup at PWL:**
- PWL at 1.0850 (known SSL).
- M15 wicks 1.0846 (4 pips below PWL), closes 1.0855.
- Next M15 candle: 18-pip green displacement, FVG forms.
- → bullish Turtle Soup. Long entry on FVG retest at CE.

**Example 2 — bullish Turtle Soup via Equal Low sweep + FVG + equilibrium rebalance, per a 2026 community source (pp.271–272):**
- Price prints an Equal Low near an unfilled bullish FVG (+FVG), itself sitting close to the 0.5 equilibrium of the most recently formed swing.
- Price sweeps the Equal Low (the Turtle Soup event), then closes back inside and rebalances into the FVG right at that equilibrium level — displacement produces an MSS.
- → the EQL sweep, FVG respect, and equilibrium rebalance coinciding is the source's trigger for entry, aligned with the main trend. The source notes this particular sweep also happened to fall in the NY Killzone on a Wednesday that set the week's low at the same equilibrium level — confluence worth noting, not a separate criterion.

**Example 3 — bearish Turtle Soup via Equal High sweep + FVG, mirrored (p.273):**
- In a downtrend, price repeatedly breaks structure (MSS) at each new Equal High, leaving an unfilled bearish FVG (−FVG) above.
- The Equal High is swept, closes back inside, and price enters from the −FVG on the reversal down.
- → same mechanics as Example 2, mirrored for the bearish case.

## Common Mistakes

- **Calling every wick a Turtle Soup.** The level must be **known** liquidity (swing high/low, EQH/EQL, session extreme); random wicks don't qualify.
- **No bias filter.** Counter-bias Turtle Soup setups fail more often than bias-aligned ones.
- **Holding through the close-back-inside.** A wick that doesn't close back inside within 3 bars is a continuation, not a Turtle Soup.
- **Conflating this with [fvg-setup-checklist](../06-fair-value-gaps/fvg-setup-checklist.md).** Both gate entry on a sweep + displacement + FVG sequence. The discriminator: Turtle Soup specifically requires the swept level's wick to **close back inside** within a few bars (the failed-breakout signature); the checklist has no such close-back-inside requirement and treats any qualifying sweep+displacement+FVG+MSS sequence as valid, breakout or fakeout alike. A sweep that keeps closing beyond the level is checklist material, not Turtle Soup.
- **Treating "Judas Swing" and "Turtle Soup" as different patterns.** A 2026 community source states they're the same underlying price behavior — a swept liquidity level with a violent reversal — and the name used depends only on whether the sweep falls inside the Judas Swing's 02:00–05:00 NY timing window. Outside that window (or on HTF/non-session-anchored setups), the same behavior is called Turtle Soup. See [judas-swing](../13-judas-swing/judas-swing.md).
- **Missing the pairing with [power-of-three](../12-power-of-three/power-of-three.md).** A 2026 community source pairs Turtle Soup with PO3 specifically, since the pattern typically forms during PO3's Manipulation phase (the same phase Judas Swing occupies at session scale) — read Turtle Soup as "what the Manipulation-phase sweep looks like on the chart," not a standalone technique divorced from AMD context.

## Related Concepts

- [bullish-turtle-soup](bullish-turtle-soup.md), [bearish-turtle-soup](bearish-turtle-soup.md), [stop-hunt-pattern](stop-hunt-pattern.md).
- [liquidity-sweep](../02-liquidity/liquidity-sweep.md), [liquidity-run](../02-liquidity/liquidity-run.md), [stop-run-definition](../29-stop-runs/stop-run-definition.md), [rejection-block](../19-rejection-blocks/rejection-block.md).
- [judas-swing](../13-judas-swing/judas-swing.md) — same underlying behavior, named differently by session timing; see Common Mistakes.
- [power-of-three](../12-power-of-three/power-of-three.md) — Turtle Soup as the chart signature of PO3's Manipulation phase.
- [equal-highs](../02-liquidity/equal-highs.md), [equal-lows](../02-liquidity/equal-lows.md) — the swept levels in Examples 2–3.
- [fvg-setup-checklist](../06-fair-value-gaps/fvg-setup-checklist.md) — a closely related but distinct sweep+displacement+FVG trigger; see Common Mistakes.

## Citations

- `ICT-2017-CHARTER-OVERVIEW` — turtle-soup terminology integrated into ICT framework.
- `ICT-2022-MENTORSHIP-OVERVIEW` — operational use refined.
- `THAI-COMMUNITY-2026-TURTLE-SOUP` — Equal Low/Equal High + FVG + equilibrium-rebalance worked entry examples (pp.271–273); Turtle Soup/Judas Swing timing-window equivalence (p.269); PO3 pairing rationale (p.262).

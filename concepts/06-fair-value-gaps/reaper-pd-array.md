# Reaper PD Array (Reaper FVG / Reaper iFVG)

**Category:** 06-fair-value-gaps
**Aliases:** Reaper PD Array, Reaper FVG, Reaper iFVG
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-FVG-TECHNIQUE
**Tags:** fvg, reaper, double-sweep, reversal, community-attributed

## Definition

A **Reaper PD Array** is an FVG that price already swept through once **without reacting** — no rejection, no pause, price simply ran through the zone on the way to taking out a liquidity pool — and is then revisited a **second time**, where it does react. This community source's operating idea: the first pass through the FVG is a decoy that stops out traders who entered on the first touch; the real reaction happens on the second visit, after price has taken liquidity on *both* sides (BSL and SSL). Distinct from [delayed-rebalance-fvg](delayed-rebalance-fvg.md) (an FVG simply left unfilled for many bars, no claim about a failed first reaction) and from [stop-run-into-fvg](../29-stop-runs/stop-run-into-fvg.md) (a single sweep → displacement → FVG entry sequence, not a double-sweep, twice-visited FVG).

## Formal Criteria

Per this source, a Reaper PD Array setup requires, in order:

1. A directional FVG forms (e.g. a bullish FVG / BISI during an uptrend leg).
2. Price sweeps **Sell-Side Liquidity (SSL)** — an old low — without reacting to the FVG on the way.
3. Price reverses and sweeps **Buy-Side Liquidity (BSL)** — an old high — again without reacting to the FVG.
4. Price returns to the original FVG zone a **second time** and reacts there (rejection / reversal), now in the direction opposite the FVG's original polarity for entries the author frames as reversal trades.
5. Entry is taken at the original FVG zone on this second touch; stop-loss beyond the wick of the liquidity sweep that preceded it; target at the opposing swing high/low or a 4–4.5 standard-deviation extension.

## Formula / Math

```
reaper_pd_array(fvg) :=
    fvg_formed
    AND first_retest_of(fvg) == no_reaction   # price passes through, untouched
    AND ssl_swept AND bsl_swept                # both sides taken between visits
    AND second_retest_of(fvg) == reaction      # rejection / reversal on 2nd touch

# entry only fires on the SECOND retest, never the first
```

## Machine-Readable

```json
{
  "id": "reaper-pd-array",
  "category": "06-fair-value-gaps",
  "aliases": ["reaper-fvg", "reaper-ifvg"],
  "criteria": [
    {"id": "c1", "expr": "fvg_formed == true"},
    {"id": "c2", "expr": "first_retest_no_reaction == true"},
    {"id": "c3", "expr": "ssl_swept == true AND bsl_swept == true"},
    {"id": "c4", "expr": "second_retest_reaction == true"}
  ],
  "timeframes": ["M15","H1","H4"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["fair-value-gap","delayed-rebalance-fvg","inversion-fvg","stop-run-into-fvg","redelivery-rebalance","equilibrium-definition"],
  "sources": ["THAI-COMMUNITY-2026-FVG-TECHNIQUE"]
}
```

## Visual Pattern

```
   Bullish FVG forms during uptrend
          ▲
        BISI
          █  ← price runs straight through on the way to BSL, no reaction (1st touch, ignored)
         ╱ ╲
       BSL   SSL   ← both liquidity pools swept, in either order
         ╲ ╱
          █  ← price returns to the same BISI zone a 2nd time — reacts here (Reaper entry)
          ▼
```

## Timeframes

M15–H4. The source frames this as a swing-style setup requiring both a prior BSL and SSL sweep, which needs enough range to develop — not a scalping pattern.

## Examples

**Example 1 — bullish Reaper setup (per source, pp.144–146):**
- Price is in an uptrend, forms a bullish FVG (BISI).
- Price sweeps SSL first (dips to take an old low) without reacting to the BISI on the way down.
- Price then rallies and sweeps BSL (takes an old high) without reacting to the BISI on the way up either.
- Price falls back a second time into the original BISI zone — this time it reacts, holding as support.
- Entry at the BISI zone; stop-loss below the wick of the SSL sweep; target at 4–4.5 standard deviations of the move, or the prior high.

## Common Mistakes

- **Entering on the first touch.** The entire premise of a Reaper setup is that the first pass is a no-reaction decoy — entering there defeats the pattern. Only the second retest qualifies.
- **Confusing this with [delayed-rebalance-fvg](delayed-rebalance-fvg.md).** Delayed rebalance is about *time* (an FVG sitting unfilled for many bars before its one and only fill); Reaper PD Array is about a *failed first reaction followed by a double liquidity sweep*, independent of how much time passes.
- **Skipping the double-sweep requirement.** This source is explicit that both BSL and SSL must be taken between the FVG's formation and its second test — a single sweep does not qualify as a Reaper setup.
- **Treating this as ICT-published terminology.** "Reaper PD Array" / "Reaper FVG" is this community source's own name for the pattern; see `## ICT vs Community` below.

## ICT vs Community

The underlying primitives — FVG formation, liquidity sweeps, and price revisiting a PD array multiple times — are all ICT-original concepts documented elsewhere in this library. What ICT does not publish is this specific named pattern: an FVG that fails to react on its first test, gets bracketed by a sweep of both BSL and SSL, and is then traded on its second test. This source's author names it "Reaper PD Array" (also "Reaper FVG" / "Reaper iFVG") and presents it as his own preferred technique within his broader 3-group FVG taxonomy, derived from personal chart study rather than a cited ICT lecture. Treat the component parts as ICT-original (high confidence, per their own files) and this specific double-sweep, twice-tested combination and its naming as community-attributed.

## Related Concepts

- [fair-value-gap](fair-value-gap.md) — the base pattern this technique reuses.
- [delayed-rebalance-fvg](delayed-rebalance-fvg.md) — a different, time-based FVG classification; see Common Mistakes.
- [inversion-fvg](inversion-fvg.md) — a related but distinct polarity-flip pattern (this source's own "Inverse FVG" material, in the same chapter).
- [stop-run-into-fvg](../29-stop-runs/stop-run-into-fvg.md) — single-sweep sequence, not the double-sweep Reaper mechanic.
- [redelivery-rebalance](redelivery-rebalance.md) — another technique from the same chapter/source.
- [equilibrium-definition](../27-equilibrium/equilibrium-definition.md) — referenced for target/entry framing.

## Citations

- `THAI-COMMUNITY-2026-FVG-TECHNIQUE` — "Reaper PD Array" / "Reaper FVG" / "Reaper iFVG," pp. 139–147.

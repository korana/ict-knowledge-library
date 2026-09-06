# Market Maker Model (MMXM)

**Category:** 31-models
**Aliases:** MMXM, Market Maker Model, MMBM, MMSM, Market Maker Buy Model, Market Maker Sell Model
**ICT Confidence:** high
**Year Introduced:** 2020
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-MMXM
**Tags:** model, mmxm, mmbm, mmsm, market-maker, po3-related

## Definition

The **Market Maker Model (MMXM)** is a 6-state elaboration of how the algorithm delivers price from one HTF liquidity pool to the opposite one, forming a V-shape or U-shape on the chart — price returns to rebalance every zone it leaves behind before the cycle completes. It runs in two directional variants: the **Market Maker Buy Model (MMBM)**, a net-bullish cycle that first sweeps HTF Sellside Liquidity via a "sell side of the curve" leg, reverses at a **Smart Money Reversal (SMR)**, then rallies via a "buy side of the curve" leg to HTF Buyside Liquidity; and the **Market Maker Sell Model (MMSM)**, the mirror. [power-of-three](../12-power-of-three/power-of-three.md) already names MMBM/MMSM as its upside/downside outcomes at the 3-phase (Accumulation-Manipulation-Distribution) level of abstraction — MMXM is this source's finer-grained, 6-state packaging of the same underlying model, not a competing framework: its Smart Money Reversal state corresponds to PO3's Manipulation phase.

## Formal Criteria

**The 6 states, in cycle order for MMBM** (MMSM is the exact mirror):

1. **Original Consolidation** — the range the cycle starts and, on a full round-trip, returns to.
2. **Distribution** — first leg of the "sell side of the curve," expanding down out of Original Consolidation.
3. **Re-Distribution** — second leg of the sell side of the curve, continuing toward HTF Sellside Liquidity.
4. **Smart Money Reversal (SMR)** — the reversal point, at or near HTF Sellside Liquidity.
5. **Accumulation** — first leg of the "buy side of the curve," rallying off the SMR.
6. **Re-Accumulation** — second leg of the buy side of the curve, continuing toward HTF Buyside Liquidity; reaching it completes the cycle ("MMBM Complete").

MMSM runs Original Consolidation → Accumulation → Re-Accumulation → SMR → Distribution → Re-Distribution → Sellside Liquidity ("MMSM Complete").

**Composition rule (load-bearing — this is what makes a curve-half real, not just a label):** after price expands out of Original Consolidation, each side of the curve must leave behind **at least 2 states' worth** of directional PD arrays, and price must return to rebalance them before continuing toward the opposite HTF pool — SIBI(-FVG)/-OB for the sell side of the curve (Distribution + Re-Distribution), BISI(+FVG)/+OB for the buy side of the curve (Accumulation + Re-Accumulation). Occasionally a third state (e.g. a second Re-Accumulation) forms before the pool is reached — still valid, the 2-state minimum is a floor, not a cap.

**Invalidation rule (the actual validity gate — not visual resemblance):** a valid MMBM requires price to **not break the low of the Accumulation state**; a valid MMSM requires price to **not break the high of the Distribution state**. Per the source's own worked example (see Examples below), a real chart rarely traces the textbook V/U shape exactly — the criterion for "is this still a valid MMBM" is this state-low/-high not being violated, not whether the swing sequence looks clean.

**SMR entry confirmation** — one of two setups at the SMR state:

- **MSS (Market Structure Shift) + Displacement**, producing a nested Order Block confirmed by an FVG inside it, with a [cisd](../07-order-blocks/cisd.md) line marking the boundary ("Change In State Of Delivery"). Price should not re-enter the nested FVG immediately, or if it does, not beyond 50% of the FVG — expect multiple retests before entry.
- **A Turtle Soup pattern** at the same level (see [turtle-soup](../20-turtle-soup/turtle-soup.md)).

**SMR verification** — one of two, and they route to different entries:

- **Classic Divergence**: cross-check against a correlated pair (e.g. EURUSD vs. GBPUSD, or EURUSD vs. DXY inverse) for [smt-divergence](../16-smt-divergence/smt-divergence.md) at the reversal point. If confirmed, focus entry on the −FVG or −OB sitting above the MSS level, or on a Bearish Breaker Block (mirror for bullish).
- **Failure Swing**: single-pair, no correlated asset needed — price retests the prior extreme, fails to exceed it, then breaks structure the other way. If this is what confirms the SMR, focus entry on the [mitigation-block](../08-breaker-blocks/mitigation-block.md) specifically — price on a Failure Swing usually doesn't exceed the Mitigation Block's range, so the wider −FVG/−OB confluence used for Classic Divergence isn't the reference here.

**HTF/LTF pairing:** identify the HTF zone first (e.g. D1 Order Block or liquidity pool); the LTF reversal (e.g. H1 SMR) is expected to occur exactly inside that HTF zone. Before trusting the LTF reversal, confirm the HTF zone itself already had a prior Breakout & Retest of at least 2 states (SIBI/-OB for a bullish HTF OB, mirror for bearish) — this is [top-down-analysis](../25-htf-bias/top-down-analysis.md)'s TF-pairing rule applied specifically to MMXM zone selection.

## Formula / Math

```
mmbm_states = ["original_consolidation","distribution","re_distribution",
               "smr","accumulation","re_accumulation"]
mmsm_states = ["original_consolidation","accumulation","re_accumulation",
               "smr","distribution","re_distribution"]

composition_valid(curve_half) := states_left_behind(curve_half) >= 2
                                  AND all_rebalanced_before_continuing

mmbm_valid := price_never_breaks(low_of_accumulation_state)
mmsm_valid := price_never_breaks(high_of_distribution_state)
# ^ the actual gate — independent of whether the swing sequence looks textbook

smr_confirmation := (MSS AND displacement AND nested_OB_with_FVG AND CISD_line)
                     OR turtle_soup_pattern

smr_verification :=
    "classic_divergence" -> entry_ref = (-FVG or -OB above MSS) or bearish_breaker
    "failure_swing"      -> entry_ref = mitigation_block
```

## Machine-Readable

```json
{
  "id": "market-maker-model",
  "category": "31-models",
  "aliases": ["MMXM", "MMBM", "MMSM", "market-maker-buy-model", "market-maker-sell-model"],
  "criteria": [
    {"id": "c1", "expr": "6_state_cycle: original_consolidation, [distribution, re_distribution] or [accumulation, re_accumulation], smr, mirror_pair, htf_pool_reached"},
    {"id": "c2", "expr": "each_curve_half_leaves_2plus_states_of_directional_PD_arrays_rebalanced_before_continuing"},
    {"id": "c3", "expr": "mmbm_valid iff price_never_breaks_accumulation_state_low"},
    {"id": "c4", "expr": "smr_confirmed_by_MSS_displacement_nested_OB_FVG_CISD OR turtle_soup"},
    {"id": "c5", "expr": "smr_verified_by_classic_divergence OR failure_swing"}
  ],
  "timeframes": ["H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2020",
  "year_refined": "2026",
  "related": ["power-of-three","cisd","mitigation-block","smt-divergence","turtle-soup","bullish-order-block","bearish-order-block","top-down-analysis","dealing-range"],
  "sources": ["THAI-COMMUNITY-2026-MMXM"]
}
```

## Visual Pattern

```
   Market Maker Buy Model (MMBM) — V/U shape, net bullish:

   Original                                          Buyside Liquidity
   Consolidation                                      | MMBM Complete
        \                                                    /\
         \  Distribution                    Re-Accumulation /
          \      \                              /\         /
           \      \  Re-Distribution          /  \        /
            \      \      \                  /    Accumulation
             \      \      \    +MSS        /
              \      \      \  /\ ← SMR    /
               \______\______\/  \________/
                  HTF POI | Sellside Liquidity
               ← sell side of the curve | buy side of the curve →

   MMSM is the exact vertical mirror: starts low, sweeps Buyside
   Liquidity first (buy side of the curve), reverses at SMR, then
   sells off (sell side of the curve) to Sellside Liquidity.
```

## Timeframes

HTF (D1, H4) for identifying the origin/destination liquidity pools and POI; LTF (H1, M15) for reading the state cycle itself and the SMR entry. The source's worked examples use D1 for HTF zone identification and H1 for the state-by-state read.

## Examples

**Example 1 — EURUSD H1 MMBM, late January 2024 (per source p.380):**
- Late Jan 2024: price sweeps SSL (the prior week's low), then prints a Smart Money Reversal — cross-checked and confirmed via GBPUSD (Classic Divergence).
- Price then moves in an MMBM-like sequence: Original Consolidation, Distribution, Re-Distribution, SMR, Accumulation — but at the point sketched for Re-Accumulation, the swing structure doesn't look like the textbook diagram; price re-tests down toward the Smart Money Reversal zone again before continuing.
- The source's own read: it's still a valid MMBM. Real price action rarely traces the pattern "beautifully" — the test is whether price broke the low of the Accumulation state. It didn't, so the model holds. Had price broken that low, "this Market Maker Buy Model would have failed" (source's own words).

## Common Mistakes

- **Requiring the chart to visually match the textbook V/U diagram.** Per Example 1, the source explicitly states price rarely traces the pattern cleanly — the actual gate is the Accumulation-state low (MMBM) or Distribution-state high (MMSM) not being broken, not visual resemblance to the diagram.
- **Entering the SMR's nested FVG immediately.** The source requires price not enter it at all, or not beyond 50% of the FVG if it does, with multiple retests expected before entry — the same discipline [cisd](../07-order-blocks/cisd.md) already requires for its own line (no body close-back through), applied here to the FVG nested inside it.
- **Skipping the Classic Divergence / Failure Swing verification step.** MSS + Displacement alone identifies a possible SMR; the source treats the divergence/failure-swing check as a required confirmation before treating the zone as tradeable, not an optional extra.
- **Using the wrong entry reference for the verification method that actually confirmed the SMR.** Classic Divergence routes to the −FVG/−OB above MSS or a Breaker Block; Failure Swing routes to the Mitigation Block specifically, since price on a Failure Swing usually doesn't exceed the Mitigation Block's range. Using the Classic Divergence entry reference after a Failure Swing confirmation (or vice versa) is not what the source's worked examples do.
- **Confusing MMXM with a competing framework to PO3.** MMXM's SMR state is PO3's Manipulation phase described in more granular detail; MMXM doesn't replace [power-of-three](../12-power-of-three/power-of-three.md), it elaborates the Distribution/Accumulation half of the cycle into named sub-states.

## Related Concepts

- [power-of-three](../12-power-of-three/power-of-three.md) — the 3-phase parent framework; MMXM's SMR state = PO3's Manipulation phase.
- [cisd](../07-order-blocks/cisd.md) — the entry-line technique at the SMR's Change-In-State-Of-Delivery boundary.
- [mitigation-block](../08-breaker-blocks/mitigation-block.md) — the entry reference when SMR is confirmed via Failure Swing.
- [smt-divergence](../16-smt-divergence/smt-divergence.md) — the cross-pair technique behind Classic Divergence verification.
- [turtle-soup](../20-turtle-soup/turtle-soup.md) — the alternative SMR-confirmation pattern alongside MSS+Displacement.
- [bullish-order-block](../07-order-blocks/bullish-order-block.md), [bearish-order-block](../07-order-blocks/bearish-order-block.md) — the OB variants nested at the SMR.
- [top-down-analysis](../25-htf-bias/top-down-analysis.md) — the HTF/LTF pairing rule MMXM applies to zone selection.
- [dealing-range](../05-pd-arrays/dealing-range.md) — Original Consolidation is a dealing range at the cycle's start/end.

## Citations

- `THAI-COMMUNITY-2026-MMXM` — full 6-state MMXM/MMBM/MMSM model, composition rule, invalidation rule, SMR entry/verification methods, HTF/LTF pairing, and the EURUSD H1 worked example, pp.370–386.

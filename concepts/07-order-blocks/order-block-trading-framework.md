# Order Block Trading Framework (5-Step)

**Category:** 07-order-blocks
**Aliases:** OB 5-step framework, POI-Optimization-Observation-Entry-Stoploss
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-ORDER-BLOCK
**Tags:** order-block, framework, entry-process, community-attributed

## Definition

This source packages Order Block trading into a **5-step operational pipeline**: Point of Interest (POI) → Optimization → Price Observation → Entry on Lower Timeframe → Stoploss Placement. Each step narrows the trade from a coarse HTF Order Block down to a precise LTF entry with a defined invalidation. Distinct from [top-down-analysis](../25-htf-bias/top-down-analysis.md): that file's 6-rung MN→W→D→H4→H1→M5 ladder is a **bias-setting** sequence (what direction, what context); this framework is a narrower **OB-specific entry pipeline** applied once an HTF Order Block has already been identified as the trade idea.

## Formal Criteria

The 5 steps, in order:

1. **Point of Interest (POI).** Identify the Order Block on a higher timeframe first (H4, Daily, Weekly) — treat "POI" as a focus/priority marker, not a separate concept from the OB itself. HTF OBs reflect who currently controls market sentiment.
2. **Optimization.** Narrow the POI's effective entry area by dropping to a lower timeframe and looking for a Demand or Supply zone nested inside the HTF OB's range, using the [Base pattern boxing convention](order-block-vs-supply-demand.md) to tighten the zone. The goal: a smaller entry area, a shorter stop-loss, and better realized R:R.
3. **Price Observation.** Do not enter simply because price has reached the OB. Distinguish **Aggressive Entry** (enter on first touch, higher risk) from **Conservative Entry** (wait for an actual Market Structure Shift + Displacement off the zone before entering, lower risk, later entry).
4. **Entry on Lower Timeframe.** Once the HTF POI is set, drop to a lower timeframe for the actual trigger, following a Top-Down-style pairing (see [top-down-analysis](../25-htf-bias/top-down-analysis.md) for the general framework; this source's own discrete pairing table is below) to keep R:R efficient.
5. **Stoploss Placement.** Place the stop beyond the wick of the Order Block (bullish OB: below OB low; bearish OB: above OB high), sized with a buffer — see [stop-placement-by-pd-array](../32-risk-management/stop-placement-by-pd-array.md) for this source's specific buffer preference relative to ICT's own guidance. Before entry, always confirm Bullish OBs sit in the Discount Zone and Bearish OBs sit in the Premium Zone.

This source's discrete HTF→LTF pairing table (step 4):

| Higher Timeframe (POI) | Lower Timeframe (Entry) |
|---|---|
| Weekly | 4 Hour |
| Daily | 1 Hour |
| 4 Hour | 30 Minute / 15 Minute |
| 1 Hour | 15 Minute |

## Formula / Math

```
ob_trading_framework(htf_ob) :=
    step1_poi := identify_ob(higher_tf in [H4, D, W])
    step2_optimized := narrow_zone(step1_poi, lower_tf_base_pattern)
    step3_confirmed := wait_for(mss_plus_displacement) if conservative else immediate
    step4_entry := trigger_on(entry_tf_paired_to(higher_tf))
    step5_sl := beyond_ob_wick(buffer)

# entry_tf_paired_to per this source's table:
#   Weekly -> 4H | Daily -> 1H | 4H -> 30m/15m | 1H -> 15m
```

## Machine-Readable

```json
{
  "id": "order-block-trading-framework",
  "category": "07-order-blocks",
  "aliases": ["ob-5-step-framework", "poi-optimization-observation-entry-stoploss"],
  "criteria": [
    {"id": "c1", "expr": "step_order == ['POI','Optimization','Price Observation','Entry on Lower TF','Stoploss Placement']"},
    {"id": "c2", "expr": "poi_identified_on_higher_tf == true"},
    {"id": "c3", "expr": "entry_tf_paired_per_table == true"}
  ],
  "timeframes": ["H1","H4","D","W"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["order-block-criteria","order-block-vs-supply-demand","top-down-analysis","stop-placement-by-pd-array","cisd","htf-bias-framework"],
  "sources": ["THAI-COMMUNITY-2026-ORDER-BLOCK"]
}
```

## Visual Pattern

```
   POI (Weekly OB)
        │
        ▼ Optimization (drop to 4H, find nested Base/Demand zone)
        │
        ▼ Price Observation (Aggressive: enter now | Conservative: wait for MSS+Displacement)
        │
        ▼ Entry on Lower TF (per pairing table: Weekly POI -> 4H entry)
        │
        ▼ Stoploss Placement (beyond OB wick + buffer; confirm Discount/Premium zone)
        │
      ENTRY
```

## Timeframes

H1–W. The framework is explicitly TF-agnostic in structure — the pairing table (step 4) is what fixes the specific TF combination for a given POI.

## Examples

**Example 1 — Weekly POI, 4H entry, per source pp.199–211:**
- Step 1 (POI): a Weekly bullish Order Block is identified in the discount zone of a larger bullish structure (XAUUSD example, pp.201–203).
- Step 2 (Optimization): dropping to Daily/4H, a Demand Zone nested inside the Weekly OB is boxed, narrowing the entry area.
- Step 3 (Price Observation): rather than buying immediately on touch (Aggressive), the source waits for a Market Structure Shift + Displacement off the zone (Conservative) before considering entry.
- Step 4 (Entry on Lower TF): per the pairing table, a Weekly POI pairs with a 4H entry trigger.
- Step 5 (Stoploss Placement): SL placed below the Weekly OB's wick low, with the buffer discussed in [stop-placement-by-pd-array](../32-risk-management/stop-placement-by-pd-array.md); confirms the OB sits in the Discount Zone before committing.

## Common Mistakes

- **Confusing this with [top-down-analysis](../25-htf-bias/top-down-analysis.md).** That file's 6-rung MN→W→D→H4→H1→M5 ladder sets directional bias across every timeframe in sequence; this framework is narrower — it starts from an already-identified HTF Order Block and walks it down to one specific entry, using this source's own discrete TF-pairing table (which skips rungs, e.g. Weekly straight to 4H) rather than the adjacent-step ladder.
- **Skipping straight to entry without Optimization.** Entering directly off the HTF POI without narrowing via a nested lower-TF Base/Demand zone produces wider stops and worse R:R than the framework intends.
- **Treating Price Observation as optional.** The source is explicit that reaching the OB zone is not itself a trade signal — Aggressive vs Conservative is a deliberate choice, and Conservative requires waiting for actual Market Structure Shift + Displacement.
- **Treating this as an ICT-published process.** The individual steps compose ICT-original concepts (OB, MSS, displacement, top-down analysis), but this specific 5-step packaging and the discrete TF-pairing table are this source's own synthesis; see `## ICT vs Community` below.

## ICT vs Community

Each component this framework calls on — Order Blocks, Market Structure Shift, displacement, Discount/Premium zones, top-down multi-timeframe analysis — is individually ICT-original and documented in its own file. What ICT does not publish is this specific named 5-step sequence (POI → Optimization → Price Observation → Entry on Lower Timeframe → Stoploss Placement) or the discrete HTF→LTF pairing table used in step 4. The author presents this explicitly as his own condensed, practical process — contrasted in the source text against his own earlier, longer treatment of the same subject in a prior book ("Technical Analysis II," 2023) — built from personal trading experience rather than a cited ICT lecture. Treat the individual components as ICT-original (high confidence, per their own files) and this specific 5-step packaging as community-attributed.

## Related Concepts

- [order-block-criteria](order-block-criteria.md) — the POI being optimized.
- [order-block-vs-supply-demand](order-block-vs-supply-demand.md) — the Base-pattern boxing convention used in the Optimization step.
- [top-down-analysis](../25-htf-bias/top-down-analysis.md) — a different, broader bias-setting framework; see Common Mistakes.
- [stop-placement-by-pd-array](../32-risk-management/stop-placement-by-pd-array.md) — step 5's SL mechanics.
- [cisd](cisd.md) — a related, more specific OB variant from the same source.
- [htf-bias-framework](../25-htf-bias/htf-bias-framework.md) — the general bias concept this framework operationalizes for OB entries specifically.

## Citations

- `THAI-COMMUNITY-2026-ORDER-BLOCK` — "5 ขั้นตอนวิธีทำกำไรจาก Order Blocks," pp. 199–214.

# Price Delivery Cycle

**Category:** 01-market-structure
**Aliases:** Price Delivery, the 4 price behavior contexts, IPDA behavior cycle
**ICT Confidence:** high
**Year Introduced:** 2018
**Year Refined:** 2026
**Source IDs:** ICT-2018-IPDA, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-PRICE-DELIVERY
**Tags:** structure, ipda, consolidation, expansion, retracement, reversal, state-machine, foundational

## Definition

Price Delivery is ICT's algorithmic model for how [IPDA](../23-ipda/ipda-definition.md) moves price over time. It describes every candle-by-candle behavior as belonging to one of **four contexts**: [range-contraction](range-contraction.md) (Consolidation), [range-expansion](range-expansion.md) (Expansion), [retracement](retracement.md) (Retracement), and Reversal. The Price Delivery Cycle formalizes these four contexts into a **state machine**: a fixed set of legal transitions between them, so that "what happens next" can be narrowed down structurally instead of guessed. Every price leg — regardless of instrument or timeframe — must begin from Consolidation, and every subsequent context is reachable only through specific, non-skippable transitions.

## Formal Criteria

The four contexts and their transition rules:

- **START → Consolidation.** Every dealing range begins with price building [equilibrium](../27-equilibrium/equilibrium-definition.md) inside a bounded range (accumulation).
- **Consolidation → Expansion only.** Consolidation can never transition directly to Retracement or Reversal — a directional break (with [displacement](../09-displacement/displacement-definition.md)) must occur first.
- **Expansion → Retracement or Reversal.** Once price displaces out of the dealing range, the very next context is either a Retracement (pullback that resumes the same direction) or a Reversal (pullback that flips direction). Expansion can never transition directly back to Consolidation.
- **Retracement → Expansion → Consolidation.** A Retracement that completes (price rebalances the FVG/Liquidity Void left by the displacement leg) resumes Expansion in the original direction, which eventually decays back into a new Consolidation.
- **Reversal → Expansion (opposite direction) → Consolidation.** A Reversal first raids the opposing [liquidity-pool](../02-liquidity/liquidity-pool.md) (Old High or Old Low), then Expansion resumes in the new direction, which eventually decays into a new Consolidation.

## Formula / Math

```
state ∈ {CONSOLIDATION, EXPANSION, RETRACEMENT, REVERSAL}

legal_transitions = {
  CONSOLIDATION: [EXPANSION],
  EXPANSION:     [RETRACEMENT, REVERSAL],
  RETRACEMENT:   [EXPANSION],
  REVERSAL:      [EXPANSION]           # expansion resumes in the opposite direction
}

illegal_transitions = {
  CONSOLIDATION -> RETRACEMENT,   # never
  CONSOLIDATION -> REVERSAL,      # never
  EXPANSION -> CONSOLIDATION      # never (must pass through RETRACEMENT or REVERSAL first)
}
```

State → produced PD-array mapping (what to look for as evidence a state has occurred):

| Price Delivery Context | Structural Artifact Produced |
|---|---|
| Expansion | [order-block-criteria](../07-order-blocks/order-block-criteria.md) (Order Blocks) |
| Retracement | [fair-value-gap](../06-fair-value-gaps/fair-value-gap.md), [liquidity-void](../02-liquidity/liquidity-void.md) |
| Reversal | [liquidity-pool](../02-liquidity/liquidity-pool.md) (Old Highs / Old Lows) |
| Consolidation | [equilibrium-definition](../27-equilibrium/equilibrium-definition.md) (50% of the range) |

## Machine-Readable

```json
{
  "id": "price-delivery-cycle",
  "category": "01-market-structure",
  "aliases": ["price-delivery", "ipda-behavior-cycle"],
  "criteria": [
    {"id": "c1", "expr": "state_sequence_always_starts_with == 'CONSOLIDATION'"},
    {"id": "c2", "expr": "CONSOLIDATION.next in ['EXPANSION']"},
    {"id": "c3", "expr": "EXPANSION.next in ['RETRACEMENT','REVERSAL']"},
    {"id": "c4", "expr": "RETRACEMENT.next in ['EXPANSION']"},
    {"id": "c5", "expr": "REVERSAL.next in ['EXPANSION']"}
  ],
  "timeframes": ["M5","M15","H1","H4","D","W"],
  "confidence": "high",
  "year_introduced": "2018",
  "year_refined": "2026",
  "related": ["range-contraction","range-expansion","retracement","ipda-definition","algorithmic-price-delivery","equilibrium-definition","liquidity-pool","fair-value-gap","liquidity-void","order-block-criteria"],
  "sources": ["ICT-2018-IPDA","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-PRICE-DELIVERY"]
}
```

## Visual Pattern

```
        START
          │
          ▼
   ┌─────────────┐   NEVER    ┌──────────────┐
   │ CONSOLIDATION│───────X──►│ RETRACEMENT  │
   └──────┬───────┘   NEVER   └──────────────┘
          │           ───X──► REVERSAL
          ▼
   ┌─────────────┐   NEVER
   │  EXPANSION  │───────X──► back to CONSOLIDATION
   └──────┬──────┘
          │  OR
   ┌──────┴───────┐
   ▼              ▼
RETRACEMENT     REVERSAL
   │              │
   ▼              ▼
EXPANSION    EXPANSION (opposite direction)
   │              │
   ▼              ▼
CONSOLIDATION  CONSOLIDATION
```

## Timeframes

All TFs, M5 → W. The cycle is fractal: an H4 Expansion leg is itself built from nested M15 Consolidation → Expansion → Retracement/Reversal cycles.

## Examples

**Example 1 — Retracement branch:**
- Price consolidates in the Asian range (Consolidation).
- London open produces a displacement candle breaking the range high (Expansion), leaving an Order Block behind.
- Price pulls back into the FVG left by the displacement candle (Retracement) without breaking the Order Block.
- Price resumes upward (Expansion, same direction) toward the next HTF liquidity target, then digests into a new Consolidation.

**Example 2 — Reversal branch:**
- Price expands upward (Expansion) into a prior swing high liquidity pool.
- Price sweeps that Old High (raiding Buy-Side Liquidity) rather than retracing into an FVG — the state machine reads this as entering Reversal.
- Price then expands downward (Expansion, opposite direction) and eventually digests into a new Consolidation.

## Common Mistakes

- **Treating Retracement and Reversal as interchangeable.** They produce different structural artifacts (FVG/Liquidity Void vs. Liquidity Pool sweep) and imply opposite forward bias — same-direction continuation vs. trend flip.
- **Trading inside Consolidation expecting a Retracement or Reversal signature.** Neither can occur until an Expansion (displacement out of the range) has happened first — the state machine forbids the direct jump.
- **Assuming Expansion decays straight back into Consolidation.** ICT's model requires a Retracement or Reversal leg between an Expansion and the next Consolidation; skipping straight back implies the Expansion never actually displaced.

## Related Concepts

- [range-contraction](range-contraction.md) / [range-expansion](range-expansion.md) — the Consolidation / Expansion states in their own dedicated files.
- [retracement](retracement.md) — the Retracement state in detail.
- [ipda-definition](../23-ipda/ipda-definition.md), [algorithmic-price-delivery](../03-order-flow/algorithmic-price-delivery.md) — the algorithmic thesis this cycle operationalizes.
- [market-efficiency-paradigm](../23-ipda/market-efficiency-paradigm.md) — who the algorithm is delivering price for/against.
- [equilibrium-definition](../27-equilibrium/equilibrium-definition.md), [liquidity-pool](../02-liquidity/liquidity-pool.md), [fair-value-gap](../06-fair-value-gaps/fair-value-gap.md), [liquidity-void](../02-liquidity/liquidity-void.md), [order-block-criteria](../07-order-blocks/order-block-criteria.md) — the artifacts each state produces.

## Citations

- `ICT-2018-IPDA` — IPDA framing of price as algorithmically delivered rather than random.
- `ICT-2022-MENTORSHIP-OVERVIEW` — Consolidation/Expansion terminology for live trading.
- `THAI-COMMUNITY-2026-PRICE-DELIVERY` — explicit 4-state flowchart with "never" transition rules and the state → PD-array mapping table.

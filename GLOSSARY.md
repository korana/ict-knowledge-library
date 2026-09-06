# Glossary — ICT Abbreviations

Single-page lookup for every abbreviation used in this library. Each entry links to the canonical concept file (file may not yet exist if its phase hasn't shipped — entries marked `(pending)` will be wired up as their phase lands).

Format: `**ABBR**` — full term — short note — link.

---

## A

- **AMD** — Accumulation, Manipulation, Distribution. The three-phase market-maker cycle. → [power-of-three](concepts/12-power-of-three/power-of-three.md)
- **APD** — Algorithmic Price Delivery. The notion that price is delivered by an algorithm, not random walk. → [algorithmic-price-delivery](concepts/03-order-flow/algorithmic-price-delivery.md)
- **ATH / ATL** — All-Time High / All-Time Low.

## B

- **Break Away Gap** — Non-ICT term; used by a 2026 community source for an untested BISI/SIBI positioned just below (or above) a [Redelivery Rebalance](concepts/06-fair-value-gaps/redelivery-rebalance.md) zone, serving as a fallback target if the RDRB fails to hold. Not ICT-original. → [redelivery-rebalance](concepts/06-fair-value-gaps/redelivery-rebalance.md)
- **BB** — Breaker Block. An order block whose extreme has been broken; flips polarity. → [breaker-block](concepts/08-breaker-blocks/breaker-block.md)
- **Bear Trap** — Non-ICT retail term for a fake bearish breakdown that reverses; used by a 2026 community source as vocabulary he used before learning ICT, same behavior as a Stop Hunt / Sweep Liquidity. Not ICT-original. → [stop-hunt-pattern](concepts/20-turtle-soup/stop-hunt-pattern.md)
- **BISI** — Buy-side Imbalance / Sell-side Inefficiency. The bullish form of an FVG. → [bullish-fvg](concepts/06-fair-value-gaps/bullish-fvg.md)
- **BOS** — Break of Structure. Price making a new swing high (bullish) or low (bearish) in the current trend direction. → [bos-bullish](concepts/01-market-structure/bos-bullish.md) / [bos-bearish](concepts/01-market-structure/bos-bearish.md)
- **BPR** — Balanced Price Range. A range with overlapping bullish and bearish FVGs. → [balanced-price-range](concepts/06-fair-value-gaps/balanced-price-range.md)
- **BSL** — Buy-Side Liquidity. Resting buy-stops above swing highs / equal highs. → [buy-side-liquidity](concepts/02-liquidity/buy-side-liquidity.md)
- **Bull Trap** — Non-ICT retail term for a fake bullish breakout that reverses; used by a 2026 community source as vocabulary he used before learning ICT, same behavior as a Stop Hunt / Sweep Liquidity. Not ICT-original. → [stop-hunt-pattern](concepts/20-turtle-soup/stop-hunt-pattern.md)

## C

- **CBDR** — Central Bank Dealing Range. The 14:00–20:00 NY window where price is expected to consolidate sideways; used as a reference range for projecting the next day's price target. → [central-bank-dealing-range](concepts/04-time-cycles/central-bank-dealing-range.md)
- **CE** — Consequent Encroachment. The 50% midpoint of an FVG. → [consequent-encroachment](concepts/06-fair-value-gaps/consequent-encroachment.md)
- **CISD** — Change In State Of Delivery. A shift in the institutional order flow, often accompanying an MSS. → [cisd](concepts/07-order-blocks/cisd.md)
- **CHoCH** — Change of Character. A structural break in the opposite direction of the prior trend. → [choch-bullish](concepts/01-market-structure/choch-bullish.md) / [choch-bearish](concepts/01-market-structure/choch-bearish.md)
- **Clean Traffic** — Non-ICT term (Demand/Supply methodology); used by a 2026 community source as a synonym for [liquidity-void](concepts/02-liquidity/liquidity-void.md) — a wide, one-sided, low-resistance price corridor. Not ICT-original. → [liquidity-void](concepts/02-liquidity/liquidity-void.md)
- **CRT** — Candle Range Theory. Community-attributed (Romeo, ~2024). NOT ICT-original. → [candle-range-theory](concepts/21-crt/candle-range-theory.md)

## D

- **D&S** — Demand and Supply. Non-ICT term (classic S&D theory); used by a 2026 community source as its label for the full-candle-body-and-wick entry zone on small/doji candles. Not ICT-original. → [mitigation-block](concepts/08-breaker-blocks/mitigation-block.md)
- **DBD** — Drop-Base-Drop. Non-ICT term (classic S&D theory); continuation-side Base pattern (supply, trend unchanged across the Base). Not ICT-original. → [order-block-vs-supply-demand](concepts/07-order-blocks/order-block-vs-supply-demand.md)
- **DOL** — Draw On Liquidity. The targeted liquidity pool the algorithm is drawn toward. → [draw-on-liquidity](concepts/02-liquidity/draw-on-liquidity.md)
- **DST** — Daylight Saving Time. Critical for any time-of-day rule; ICT teaches in NY time. → [dst-handling](concepts/04-time-cycles/dst-handling.md)

## E

- **EQH** — Equal Highs. Two or more highs at the same price level — pool of liquidity. → [equal-highs](concepts/02-liquidity/equal-highs.md)
- **EQL** — Equal Lows. Mirror of EQH on the sell side. → [equal-lows](concepts/02-liquidity/equal-lows.md)
- **EQ** — Equilibrium. The 50% midpoint of a dealing range. → [equilibrium-definition](concepts/27-equilibrium/equilibrium-definition.md)
- **ERL** — External Range Liquidity. Liquidity outside the current dealing range. → [external-range-liquidity](concepts/02-liquidity/external-range-liquidity.md)

## F

- **Failure Swing** — Non-ICT term (Dow Theory framing): a swing that fails to print a new Higher High (uptrend) or Lower Low (downtrend) before structure breaks the other way. Used by a 2026 community source as the trigger condition for its "Mitigation Block." → [mitigation-block](concepts/08-breaker-blocks/mitigation-block.md)
- **Flout / Flout STD** — Non-ICT term; a 2026 community source's coinage for a combined 14:00–00:00 NY window (CBDR window ∪ Asian killzone window), projected with the same STD mechanic as CBDR. Not ICT-original; no prior Source ID in this wiki uses it. → [flout-range](concepts/04-time-cycles/flout-range.md)
- **FOMC** — Federal Open Market Committee. The macro event ICT's two-stage delivery model targets. → [fomc-two-stage-delivery](concepts/30-news-driven/fomc-two-stage-delivery.md)
- **FVG** — Fair Value Gap. Three-candle imbalance where the middle candle's range is not overlapped. → [fair-value-gap](concepts/06-fair-value-gaps/fair-value-gap.md)

## H

- **HH / HL / LH / LL** — Higher High / Higher Low / Lower High / Lower Low. The four basic structural relationships between consecutive swings. → [swing-high](concepts/01-market-structure/swing-high.md) / [swing-low](concepts/01-market-structure/swing-low.md)
- **HOD** — High of Day. Daily high; structural reference. → covered in `25-htf-bias`
- **HTF** — Higher Time Frame. Any TF used to set bias for a lower TF entry. → [htf-bias-framework](concepts/25-htf-bias/htf-bias-framework.md)

## I

- **IDM** — Inducement. A community/SMC term (explicitly not ICT-original per its 2026 source) for a structural level intended to trap retail traders before the real move; the source's own translation is that it's the ICT-side internal SSL/BSL. Not ICT-original. → [inducement](concepts/02-liquidity/inducement.md)
- **IFVG** — Inversion FVG. A traded-through FVG whose role flips (support↔resistance). → [inversion-fvg](concepts/06-fair-value-gaps/inversion-fvg.md)
- **IPDA** — Interbank Price Delivery Algorithm. ICT's name for the institutional algorithm; uses 20/40/60-day lookbacks. → [ipda-definition](concepts/23-ipda/ipda-definition.md)
- **IRL** — Internal Range Liquidity. Liquidity inside the current dealing range (FVGs, OBs, internal swing points). → [internal-range-liquidity](concepts/02-liquidity/internal-range-liquidity.md)

## L

- **LOD** — Low of Day. Daily low; structural reference. → covered in `25-htf-bias`
- **LTF** — Lower Time Frame. Used for entry refinement.

## M

- **MMBM** — Market Maker Buy Model. AMD running to upside distribution. → [power-of-three](concepts/12-power-of-three/power-of-three.md)
- **MMSM** — Market Maker Sell Model. AMD running to downside distribution. → [power-of-three](concepts/12-power-of-three/power-of-three.md)
- **MSS** — Market Structure Shift. A specific form of CHoCH characterized by displacement through the prior structure level. → [mss](concepts/01-market-structure/mss.md)

## N

- **NDOG** — New Day Opening Gap. Gap between previous day's close and new day's open at midnight NY. → [ndog](concepts/31-models/ndog.md)
- **NFP** — Non-Farm Payrolls. Monthly US labor report; high-impact news. → [nfp-protocol](concepts/30-news-driven/nfp-protocol.md)
- **NWOG** — New Week Opening Gap. Gap between Friday close and Sunday/Monday open. → [nwog](concepts/31-models/nwog.md)
- **NY** — New York time. The canonical timezone for every time-of-day reference in this library (subject to DST). → [dst-handling](concepts/04-time-cycles/dst-handling.md)

## O

- **OB** — Order Block. Last opposite-direction candle before a displacement. → [bullish-order-block](concepts/07-order-blocks/bullish-order-block.md) / [bearish-order-block](concepts/07-order-blocks/bearish-order-block.md)
- **OTE** — Optimal Trade Entry. The 0.62–0.79 retracement zone, typically entered at 0.705. → [ote-overview](concepts/17-optimal-trade-entry/ote-overview.md)

## P

- **PD Array** — Premium / Discount Array. Any institutional price level (FVG, OB, breaker, equilibrium, etc.). → [pd-array-definition](concepts/05-pd-arrays/pd-array-definition.md)
- **PDH / PDL** — Previous Day High / Low. Liquidity reference levels for the current day. → covered in `02-liquidity` and `25-htf-bias`
- **PMH / PML** — Previous Month High / Low. Monthly liquidity reference. → covered in `25-htf-bias`
- **PO3** — Power of Three. Same as AMD. → [power-of-three](concepts/12-power-of-three/power-of-three.md)
- **POI** — Point of Interest. Used by a 2026 community source as a focus/priority marker for an HTF Order Block, the first step of its 5-step OB trading framework. → [order-block-trading-framework](concepts/07-order-blocks/order-block-trading-framework.md)
- **PWH / PWL** — Previous Week High / Low. Weekly liquidity reference. → covered in `25-htf-bias`

## Q

- **Quasimodo / QM** — Non-ICT term (classic Technical/price-action reversal pattern, also used in Demand/Supply and RTM circles). A 2026 community source compares it in passing to [Turtle Soup](concepts/20-turtle-soup/turtle-soup.md) for Technical-methodology readers, but does not treat it as an ICT concept. Not ICT-original; out of scope for a dedicated file. → [turtle-soup](concepts/20-turtle-soup/turtle-soup.md)

## R

- **R** — R-multiple. Profit/loss measured in units of initial risk. → [r-multiple](concepts/32-risk-management/r-multiple.md)
- **RBR** — Rally-Base-Rally. Non-ICT term (classic S&D theory); continuation-side Base pattern (demand, trend unchanged across the Base). Not ICT-original. → [order-block-vs-supply-demand](concepts/07-order-blocks/order-block-vs-supply-demand.md)
- **Reaper PD Array** — Non-ICT term (also "Reaper FVG" / "Reaper iFVG"); used by a 2026 community source for an FVG that fails to react on its first test, gets bracketed by a sweep of both BSL and SSL, and reacts only on a second visit. Not ICT-original. → [reaper-pd-array](concepts/06-fair-value-gaps/reaper-pd-array.md)
- **RDRB** — Redelivery Rebalance. Non-ICT term; used by a 2026 community source for a 3-candle repricing zone formed within a strong directional run. Not ICT-original. → [redelivery-rebalance](concepts/06-fair-value-gaps/redelivery-rebalance.md)
- **Rising Wedge / Falling Wedge** — Pre-ICT classical chart pattern; the modern popular framing of a [Three Drive Pattern](concepts/01-market-structure/three-drive-pattern.md). Not ICT-original. → [three-drive-pattern](concepts/01-market-structure/three-drive-pattern.md)
- **RTM** — Read The Market. A price action trading methodology focusing on Rally/Drop phases and Significant Demand Engulfment.

## S

- **SD** — Standard Deviation (in ICT's projection tool). Used at -1.5, -2, -2.5, -4 SD targets. → [standard-deviation-projections](concepts/28-fibonacci-levels/standard-deviation-projections.md)
- **Seek & Destroy** [sic, source spells it "Seak"] — A 2026 community source's name for a week with no clean shape: price sweeps both sides of a wide sideways range with no trend, triggered by conditions like back-to-back FOMC days, a bank holiday, or thin-liquidity periods. Not one of that source's own six named weekly shapes — it names the conditions that break all of them. → [weekly-profile-patterns](concepts/22-quarterly-theory/weekly-profile-patterns.md)
- **STDv** — A 2026 community source's own shorthand for "Standard Deviation," used across at least two different anchor systems in the same chapter: time-bounded-range multiples (CBDR/Asian/Flout family) and swing-leg extensions (this file's own family, 2.0–2.5/4.0–4.5 variant). Check which family a given "STDv" reference means before applying it. → [standard-deviation-projections](concepts/28-fibonacci-levels/standard-deviation-projections.md), [central-bank-dealing-range](concepts/04-time-cycles/central-bank-dealing-range.md)
- **SIBI** — Sell-side Imbalance / Buy-side Inefficiency. The bearish form of an FVG. → [bearish-fvg](concepts/06-fair-value-gaps/bearish-fvg.md)
- **SMC** — Smart Money Concepts. Community rebrand of ICT material. Distinct from ICT-original. SMC vocabulary maps to ICT concepts; see "SMC Vocabulary Cross-Reference" section at the bottom of this file.
- **SMR** — Smart Money Reversal (also "SMR Divergence"). A 2026 community source's modern ICT-era name for SMT Divergence — same Correlation + Divergence technique, no new mechanic. → [smt-divergence](concepts/16-smt-divergence/smt-divergence.md)
- **SMT** — Smart Money Technique (divergence). Divergence between correlated assets. → [smt-divergence](concepts/16-smt-divergence/smt-divergence.md)
- **SRF** — Support/Resistance Flip. RTM-methodology term. This 2026 community source uses it loosely across two of its own chapters — equated with its "Mitigation Block" reading in one, and with "Breaker Block" in another — with an explicit author's-own caveat in the Breaker Block chapter that his ICT-based Breaker Block and generic SRF are "similar but not the same" (his Breaker requires a prior BSL/SSL liquidity sweep; generic SRF does not). Not ICT-original. → [mitigation-block](concepts/08-breaker-blocks/mitigation-block.md), [breaker-block](concepts/08-breaker-blocks/breaker-block.md)
- **SSL** — Sell-Side Liquidity. Resting sell-stops below swing lows / equal lows. → [sell-side-liquidity](concepts/02-liquidity/sell-side-liquidity.md)
- **Stop Raid** — Synonym for Stop Hunt / Stoploss hunting, used explicitly alongside BSL/SSL by a 2026 community source. → [stop-hunt-pattern](concepts/20-turtle-soup/stop-hunt-pattern.md)

## T

- **TDO** — True Day Open. Midnight NY open of the daily candle. → [true-day-open](concepts/22-quarterly-theory/true-day-open.md)
- **TF** — Time Frame.
- **TGIF** — "Thank God It's Friday." Non-ICT term; a 2026 community source's own name for a Friday-specific weekly Power of Three setup (Thursday liquidity sweep into a weekly/daily HTF FVG retracement). Not ICT-original; explicitly backtested-only, never traded live per the source. → [tgif-weekly-po3](concepts/31-models/tgif-weekly-po3.md)
- **Three Drive** — Pre-ICT classical reversal pattern (also "3 Drive Pattern"); a 2026 community source integrates it with the PD-array stack, gating entry on a sweep + displacement + FVG at the Old High/Old Low. Not ICT-original. → [three-drive-pattern](concepts/01-market-structure/three-drive-pattern.md)
- **TWO** — True Week Open. Sunday 18:00 NY (or Monday 00:00 NY depending on broker). → [true-week-open](concepts/22-quarterly-theory/true-week-open.md)

---

## Timeframe Shorthand

Standard chart timeframe abbreviations used throughout the library:

- **M1** — 1-minute
- **M5** — 5-minute
- **M15** — 15-minute
- **M30** — 30-minute
- **H1** — 1-hour
- **H4** — 4-hour
- **D / D1** — Daily
- **W / W1** — Weekly
- **MN / MN1** — Monthly

---

## SMC Vocabulary Cross-Reference

The Smart Money Concepts (SMC) community uses several terms that are **synonyms or near-synonyms for ICT-original concepts**. ICT did not author the SMC framework — it's a community rebrand — but for searchability, the most-common SMC terms are listed here with their ICT equivalents. Each ICT concept file's `Aliases:` field has been extended with the corresponding SMC term where applicable.

| SMC term | ICT equivalent | File |
|---|---|---|
| Demand zone / demand block | Bullish Order Block | [bullish-order-block](concepts/07-order-blocks/bullish-order-block.md) |
| Supply zone / supply block | Bearish Order Block | [bearish-order-block](concepts/07-order-blocks/bearish-order-block.md) |
| Liquidity grab | Liquidity Sweep (raid / stop hunt) | [liquidity-sweep](concepts/02-liquidity/liquidity-sweep.md) |
| Fakeout / swing failure | Turtle Soup (failed breakout) | [turtle-soup](concepts/20-turtle-soup/turtle-soup.md) |
| Internal BOS / external BOS | Internal vs external structure + BOS | [bos-bullish](concepts/01-market-structure/bos-bullish.md), [bos-bearish](concepts/01-market-structure/bos-bearish.md), [internal-structure](concepts/01-market-structure/internal-structure.md), [external-structure](concepts/01-market-structure/external-structure.md) |
| Imbalance | FVG / volume imbalance | [imbalance-vs-fvg](concepts/26-imbalance/imbalance-vs-fvg.md) |
| Buy-side imbalance (BISI) / Sell-side imbalance (SIBI) | Bullish / Bearish FVG | [bullish-fvg](concepts/06-fair-value-gaps/bullish-fvg.md), [bearish-fvg](concepts/06-fair-value-gaps/bearish-fvg.md) |
| Equal highs / equal lows | Same as ICT (already shared vocabulary) | [equal-highs](concepts/02-liquidity/equal-highs.md), [equal-lows](concepts/02-liquidity/equal-lows.md) |
| Premium / discount / equilibrium | Same (ICT-original) | [premium-array](concepts/05-pd-arrays/premium-array.md), [discount-array](concepts/05-pd-arrays/discount-array.md), [equilibrium-definition](concepts/27-equilibrium/equilibrium-definition.md) |
| Compression | Range contraction / accumulation phase | [range-contraction](concepts/01-market-structure/range-contraction.md), [accumulation-phase](concepts/12-power-of-three/accumulation-phase.md) |
| Order flow | Same (covered as full directory) | [03-order-flow/](concepts/03-order-flow/) (6 files) |

Terms in **SMC-only** territory (not ICT-original, not in this library):

- **Engulfing block** — community-coined OB variant; not part of ICT canon. Note (2026): a separate Thai community source uses the bare term "Engulfing" for a different meaning again — a liquidity level that fails to sweep (price pierces the level but closes back inside it), as distinct from a confirmed sweep/BOS (close beyond the level). Neither usage is ICT-original or the standard candlestick-pattern "engulfing." → [liquidity-sweep](concepts/02-liquidity/liquidity-sweep.md)
- **Wyckoff spring / upthrust** — Wyckoff terminology sometimes blended with SMC; out of scope per this library's ICT-only policy.

If a community-attributed concept becomes important enough to add (precedent: CRT in `concepts/21-crt/`), it should be filed under its own directory with `confidence: community-attributed` and an explicit `## ICT vs Community` section per [`AGENTS.md`](AGENTS.md).

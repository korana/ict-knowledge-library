# Daily Bias

**Category:** 25-htf-bias
**Aliases:** D bias, daily direction, daily setup bias
**ICT Confidence:** high
**Year Introduced:** 2017
**Year Refined:** 2026
**Source IDs:** ICT-2017-CHARTER-OVERVIEW, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-DAILY-BIAS-CLOSE, THAI-COMMUNITY-2026-DAILY-BIAS-ORDER-FLOW, THAI-COMMUNITY-2026-DAILY-BIAS-HOW-TO-USE, THAI-COMMUNITY-2026-POWER-OF-THREE, THAI-COMMUNITY-2026-STD-PROJECTION, THAI-COMMUNITY-2026-DAILY-BIAS-SWING-POINT
**Tags:** htf-bias, daily, foundational

## Definition

Daily bias is the directional read from the **daily chart** — the primary bias-setting TF for ICT day-traders. While weekly and monthly provide context, daily bias is what most intraday setups align against. It changes faster than weekly but slower than H4, and a fresh daily CHoCH/MSS frequently signals the start of a new multi-day swing.

## Formal Criteria

Daily bias is bullish when:

- Most recent daily external BOS was up OR a daily CHoCH-up has just printed.
- Current price below daily EQ (in daily discount).
- Daily DOL is upside (PDH/PWH ahead).

Bearish when symmetric. Neutral when conflicting.

Common signals:

- True Day Open (00:00 NY) above prior day's range = mild bullish lean.
- Daily candle closed strongly directional yesterday = momentum continuation expected today.
- Daily wicked one bound = sweep + reversal possible.

**A 2026 community source's own three-method taxonomy** (distinct from the structure/EQ/DOL method above, which predates this source and isn't part of its numbering):

1. **Method 1 — Order Flow.** Read which direction the market's institutional Order Flow is committed to, via bullish/bearish FVG-or-OB respect-and-continuation sequences. This is the source's primary, most-elaborated method — no new criteria beyond what's already documented at [bullish-order-flow](../03-order-flow/bullish-order-flow.md) / [bearish-order-flow](../03-order-flow/bearish-order-flow.md); the source itself recommends studying [cisd](../07-order-blocks/cisd.md) over generic Order Blocks, calling CISD the only "Original" ICT order block.
2. **Method 2 — close vs. prior day's range.** Detailed immediately below.
3. **Method 3 — past Swing Points.** Named but not elaborated when this footnote was first written; a later chapter by the same author, dedicated to exactly this method, supplies it below.

**Method 3 in full (community-attributed):** the same close-through mechanic as Method 2, generalized from "yesterday's high/low" to a **ranked set of candidate Swing Points**, plus a validity filter for which highs/lows count as a genuine Swing Point in the first place.

- **Candidate anchors, in the source's own stated priority order:** Equal High/Equal Low → Previous Month High/Low → Previous Week High/Low → Previous Day High/Low → Previous Killzone High/Low. (Previous Day High/Low sitting inside this list is what makes Method 2 a special case of Method 3, not a separate rule — Method 2 is this list read at just its "Previous Day" tier.) This is a different axis from `top-down-analysis.md`'s Major/Medium/Minor Liquidity TF-tiers (Session/Daily/Weekly/Monthly swings bucketed by *timeframe*) — that classification doesn't rank *which specific anchor* to prefer for Daily Bias the way this list does, so the two aren't the same content restated.
- **Validity filter:** a candidate Old High/Low only counts as a confirmed Swing Point if it's marked by a **3-candle reversal cluster** — the source names "Star" (Morning Star / Evening Star) or Three Inside Up/Down. This is the identical cluster list a different chapter by the same author already uses for locating a CISD candle inside a reversal (see [cisd](../07-order-blocks/cisd.md) Common Mistakes) — same author reusing his own technique for a second purpose, not independent corroboration of the technique itself.
- **The bias rule:** a **close** (not a wick) beyond a confirmed Swing Point's high/low sets Daily Bias to Sell Day (close below) or Buy Day (close above) — the same close-through logic as Method 2's PDH/PDL rule, now applied at whichever tier of the ranked list the trader is tracking.
- **Locating each tier's Swing Point, per the source's own MT4/MT5 charting convention:** set the platform's Period Separator one level coarser than the working timeframe — Weekly chart → Yearly separator, Daily chart → Monthly separator, H4 chart → Weekly separator, H1/M15 chart → Daily separator. Each separator-bounded block is where that tier's high/low is read from (e.g. a Previous Month High is read off one Yearly-separator block on the Weekly chart). A charting-convenience note, not a new price-delivery rule.
- **Self-deferral, resolved backward:** the source closes by pointing to Session + Killzone as the next topic to compound with Daily Bias — already covered in this wiki (`asia-session.md`/`london-session.md`/`ny-am-session.md`, `killzone-overview.md`), so this deferral resolves to existing content rather than a future ingest.

**Method 2 in full (community-attributed):**

The source's second method reads the *next* day's bias purely from where the daily candle **closes** relative to the prior day's high (PDH) and low (PDL) — distinct from the structure/EQ/DOL method above:

- **Close above PDH** → bullish bias for the next day (source labels this "OLHC"; targets the next Draw on Liquidity upside).
- **Close below PDL** → bearish bias for the next day (labels this "OHLC"; targets the next Draw on Liquidity downside).

*(This chapter used "OLHC"/"OHLC" as labels without defining them. A later chapter by the same author, on [power-of-three](../12-power-of-three/power-of-three.md), supplies the definition: the letters name the order in which the candle's extremes print, driven by which PO3 phase produced each one. OLHC = Open→Low(manipulation)→High(distribution)→Close, the bullish path; OHLC = Open→High(manipulation)→Low(distribution)→Close, its bearish mirror — hence the close-above-PDH/close-below-PDL split above lining up with those two letter orders. A still-later chapter by the same author (`THAI-COMMUNITY-2026-STD-PROJECTION`, p.554) spells both orders out in words on its own diagrams, upgrading this from an inferred decode to source-stated.)*
- **Sweeps PDH first, then closes back below PDH** → failed-sweep reversal; bearish bias for the next day (see [stop-hunt-pattern](../20-turtle-soup/stop-hunt-pattern.md) for the underlying mechanic — this is its daily-close, next-day-bias application).
- **Sweeps PDL first, then closes back above PDL** → failed-sweep reversal; bullish bias for the next day. Reaching the Draw on Liquidity target can take more than one day.
- **Closes inside the prior day's range** (breaks neither PDH nor PDL) → no bias, don't trade; wait for a breakout of the prior day's range in either direction before acting. (Source frames the prior day as a "Mother Bar" and the inside close as an "Inside Bar" — a different use of that vocabulary than its entry-timing role in [equilibrium-definition](../27-equilibrium/equilibrium-definition.md).)

**Operational caution:** don't act on either method's read before price actually reaches the PDH/PDL level in question — the source warns against inferring a bias from the visual shape of the daily candle alone and trading ahead of price confirming it.

**Weekly check-stop for the daily cascade (community-attributed):** applying Method 2 day after day — each day's close setting the next day's bias — is a *cascade*: a run of same-direction closes (e.g. four straight lower-lows) reads as "continue." A companion 2026 chapter by the same author warns this cascade is subordinate to the weekly close: if the streak has run several days but the most recently closed **weekly** candle did *not* itself close beyond the prior week's range, expect a sweep-then-reverse instead of further continuation — the cascade's own worked example confirms this exact override (a 4-day-down streak stopped and reversed because the closing weekly candle hadn't broken the prior week's low). See [bias-invalidation](bias-invalidation.md) for the underlying CHoCH/MSS-with-displacement mechanic this reversal rides on. The same source also states (without giving specific thresholds) that the Method 2 close-based read generalizes to Weekly, Monthly, and Yearly bias, and its own worked example determines the week's bias first before cascading down into daily.

## Formula / Math

```
daily_dealing_range = [LTL_d, LTH_d]
d_eq = (LTL_d + LTH_d) / 2

daily_bias :=
  "bullish" if last_daily_external == bullish AND price < d_eq AND upside_DOL
  "bearish" if last_daily_external == bearish AND price > d_eq AND downside_DOL
  "neutral" otherwise
```

## Machine-Readable

```json
{
  "id": "daily-bias",
  "category": "25-htf-bias",
  "aliases": ["D-bias", "daily-direction", "daily-setup-bias"],
  "criteria": [
    {"id": "c1", "expr": "uses_daily_external_structure"},
    {"id": "c2", "expr": "considers_price_vs_daily_eq"},
    {"id": "c3", "expr": "considers_PDH_PDL_DOL"}
  ],
  "timeframes": ["D","H4","H1"],
  "confidence": "high",
  "year_introduced": "2017",
  "year_refined": "2026",
  "related": ["htf-bias-framework","monthly-bias","weekly-bias","bias-confluence","top-down-analysis","true-day-open","time-of-day-pivots","buy-side-liquidity","sell-side-liquidity","stop-hunt-pattern","bullish-order-flow","bearish-order-flow","cisd","bias-invalidation","power-of-three","swing-high","swing-low"],
  "sources": ["ICT-2017-CHARTER-OVERVIEW","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-DAILY-BIAS-CLOSE","THAI-COMMUNITY-2026-DAILY-BIAS-ORDER-FLOW","THAI-COMMUNITY-2026-DAILY-BIAS-HOW-TO-USE","THAI-COMMUNITY-2026-POWER-OF-THREE","THAI-COMMUNITY-2026-STD-PROJECTION","THAI-COMMUNITY-2026-DAILY-BIAS-SWING-POINT"]
}
```

## Visual Pattern

```
   Daily chart bullish bias:

   PDH ───────────  (yesterday's high — potential BSL target today)
       /\
      /  \   today's price near discount of D range
   ──────── D_EQ
            \
   PDL ────── (yesterday's low — already swept = manipulation)
```

## Timeframes

D / H4 / H1.

## Examples

**Example 1 — bullish daily bias:**
- D LTH 1.0950 (yesterday); D LTL 1.0820 (3 days ago).
- D_EQ = 1.0885.
- Today's price 1.0855 = discount.
- Today's TDO 1.0860 above PDH 1.0860? → mild bullish lean.
- DOL: PDH BSL above 1.0950 (today's target).
- → bullish daily bias; intraday setups long-aligned.

## Common Mistakes

- **Stale daily bias.** Once today's session confirms a structural shift on D, refresh the bias.
- **Single-candle daily reads.** A daily CHoCH on a thin-volume day may not stick — wait for confirmation in the next 1-2 sessions.
- **Conflict ignorance.** When weekly and daily disagree, the conflict itself is the signal — reduce conviction or wait.
- **Trading the visual shape, not the level.** A daily candle that merely "looks" like it's forming a certain bias (e.g. looks like a downtrend) can still resolve the opposite way once it actually closes relative to PDH/PDL — wait for the close-vs-PDH/PDL confirmation from the community-attributed method above, don't front-run it from chart shape alone.

## Related Concepts

- [htf-bias-framework](htf-bias-framework.md), [monthly-bias](monthly-bias.md), [weekly-bias](weekly-bias.md), [bias-confluence](bias-confluence.md), [top-down-analysis](top-down-analysis.md).
- [true-day-open](../22-quarterly-theory/true-day-open.md), [time-of-day-pivots](../04-time-cycles/time-of-day-pivots.md).
- [buy-side-liquidity](../02-liquidity/buy-side-liquidity.md), [sell-side-liquidity](../02-liquidity/sell-side-liquidity.md) — PDH/PDL as the reference levels for the close-vs-PDH/PDL method.
- [stop-hunt-pattern](../20-turtle-soup/stop-hunt-pattern.md) — the sweep-then-fail-to-close-through mechanic behind the reversal branches.
- [bullish-order-flow](../03-order-flow/bullish-order-flow.md), [bearish-order-flow](../03-order-flow/bearish-order-flow.md) — Method 1 (Order Flow), the source's primary Daily Bias method.
- [cisd](../07-order-blocks/cisd.md) — the source's preferred reference over generic Order Blocks for Method 1.
- [bias-invalidation](bias-invalidation.md) — the CHoCH/MSS-with-displacement mechanic behind the weekly check-stop's sweep-then-reverse.
- [power-of-three](../12-power-of-three/power-of-three.md) — the OLHC/OHLC candle-path-order mechanic behind Method 2's labels.

## Citations

- `ICT-2017-CHARTER-OVERVIEW`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-DAILY-BIAS-CLOSE` — close-vs-PDH/PDL as an alternative Daily Bias method ("Method 2"), all five branches, pp.402, 406–411.
- `THAI-COMMUNITY-2026-DAILY-BIAS-ORDER-FLOW` — the source's own Method 1/2/3 taxonomy and Method 1 (Order Flow) detail, pp.388–390.
- `THAI-COMMUNITY-2026-DAILY-BIAS-HOW-TO-USE` — the weekly check-stop on the daily cascade (worked example, pp.421–422, 427) and the Weekly/Monthly/Yearly generalization claim (p.412), pp.412–427.
- `THAI-COMMUNITY-2026-POWER-OF-THREE` — the OLHC/OHLC candle-path-order definition this file's Method 2 labels were missing, pp.511–514.
- `THAI-COMMUNITY-2026-DAILY-BIAS-SWING-POINT` — Method 3 in full: ranked Swing Point anchors, 3-candle validity filter, and the MT4/MT5 Period Separator locating convention, pp.429, 432–433.

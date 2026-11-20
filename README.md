# OKX Options Fees: 0.02%/0.03% Base Rates, the 7% Premium Cap, and Which of the Three Trading Channels Fits Your Order Size

OKX charges **0.02% maker and 0.03% taker** on options at the regular tier, and no single trade can cost more than **7% of the premium** you paid. Exercise adds a separate charge, the minimum of 0.02%, your taker rate, and 7% of settlement value, and it is billed only on options you actually exercise. Options that expire on any day other than Friday carry no exercise fee at all.

Those numbers cover most of the bill, but not all of it. A cheap far-out-of-the-money contract often costs a fraction of 0.03% because the 7% cap takes over, and a forced liquidation is priced on a different formula again. The rate on the fee page is also not always the rate your account sits on, since the schedule changes by region, account type and VIP tier. What follows is the arithmetic behind each charge, the three channels you can trade through, and the cases where OKX is the wrong venue for the trade you have in mind.

> **Quick take:** estimate at 0.02%/0.03% first. If you buy cheap OTM options, the 7% cap usually sets your real cost, and it can cut the fee by 80% or more. Buy-only accounts can start in Simple Options with no minimum capital.
> 👉 [Open an OKX account and check your own Options fee tier](https://okx.com/join/CASH20)

## The four charges in an OKX options position

Options are not priced like spot or perpetuals. There is a trading fee on the fill, a cap on that fee, an exercise fee at expiry, and a liquidation fee if the position is closed by the risk engine. OKX's own help documentation states plainly that "both transaction fees and exercise fees are applied," so you should not model a round trip using the trading fee alone.

| Charge | Formula (official) | Regular tier figure | When it applies |
| --- | --- | --- | --- |
| Trading fee, maker | Min(fee rate, 7% × option premium) × multiplier × contract size × contracts | 0.02% | Every fill that rests on the book |
| Trading fee, taker | Same formula, positive rate | 0.03% | Every fill that takes liquidity |
| Premium cap | 7% of the option premium | Sets the ceiling per trade | Binds whenever the percentage fee would exceed it |
| Exercise fee | Min(0.02%, your taker tier, 7% × settlement value) × multiplier × contract size × contracts | 0.02% in most cases | Exercised options only, and never on daily (non-Friday) expiries |
| Liquidation fee | Min(your taker tier, 7% × mark price) × multiplier × contract size × contracts | Your taker rate | Forced liquidation only |

Three mechanical details matter for the arithmetic:

- **Fees are charged in crypto.** BTC options settle in BTC and ETH options in ETH, so the fee comes out of the same coin. The USDT-margined version of the formula multiplies the whole expression by the index price.
- **One BTC contract is 0.01 BTC of notional, one ETH contract is 0.1 ETH.** The underlying index is BTC-USD or ETH-USD. If you trade in portfolio margin or multi-currency mode you can post stablecoins as margin, but settlement stays in BTC or ETH.
- **The 0.02%/0.03% pair is the figure OKX uses in its worked example.** The Options tab of the live fee schedule is the authoritative source for your own tier, and regional schedules differ. On spot, for instance, EEA accounts without a derivatives account and US accounts start at 0.20% maker and 0.35% taker instead of the global 0.08%/0.10%.

## The three channels, and what each one costs you to enter

OKX does not sell options as a monthly or annual plan, so there is no "package price" to compare. What changes is the channel, the capital you need before the channel opens, and the VIP tier that sets your rate inside it.

| Channel | What you can do | Minimum capital | Fee treatment | Access |
| --- | --- | --- | --- | --- |
| Simple Options | Buy options only, no selling, simplified ticket | None | Standard trading fee, 7% premium cap applies | [Start with Simple Options](https://okx.com/join/CASH20) |
| Options Chain | Full strike and expiry grid, Greeks, buy and sell, the whole order book | None for overseas KYC; 10,000 USD for mainland China KYC | Standard fee by tier, cap applies per leg | [Open Options Chain access](https://okx.com/join/CASH20) |
| RFQ / Liquid Marketplace | Single-leg blocks and multi-leg strategies, not available in the app | 10,000 USD minimum per RFQ | Fees quoted per strategy, cap applies | [Request RFQ access](https://okx.com/join/CASH20) |

Two thresholds sit outside the channel table. Switching to a multi-currency account and switching to portfolio margin both require 10,000 USD, and neither is needed if you only buy options. Long option positions can be held as isolated positions with no liquidation risk, so a pure buyer can skip margin modes entirely.

## What the 7% premium cap actually saves you

OKX cut the cap from 12.5% to 7% of the option premium, announced on 8 May 2025 and effective at **07:00 UTC on 15 May 2025**. The same adjustment applied to the exercise fee and the liquidation fee. Any guide still quoting 12.5% is describing the pre-May-2025 schedule.

The cap does nothing on an at-the-money contract, where the percentage fee is already tiny relative to the premium. It matters on cheap contracts, and you can work out exactly where the switch happens from the official formula. The cap binds when the percentage fee exceeds 7% of the premium, which is when the premium falls below roughly **0.43% of contract value for a taker** (0.03 ÷ 7) or **0.29% for a maker** (0.02 ÷ 7). Below those levels you pay 7% of the premium and nothing more.

A worked case, using the official formula and illustrative numbers:

- You buy 100 BTC call contracts as a taker, so notional is 100 × 0.01 = 1 BTC.
- The premium is 0.0005 BTC per unit of notional, which is 0.05% of the underlying and well into out-of-the-money territory. Total premium is 0.0005 BTC.
- The uncapped taker fee would be 0.03% × 0.01 × 100 = 0.0003 BTC, or 60% of the premium.
- The cap is 7% × 0.0005 = 0.000035 BTC. That is what gets charged, about 88% below the headline rate.

This is the single most useful thing to understand about OKX options pricing: the 0.03% figure is a ceiling on the rate, not a floor on what cheap options cost. Someone buying lottery-ticket calls pays a rate close to 0.0035% of notional rather than 0.03%.

👉 [Open an account and price a small OTM order to see the cap applied](https://okx.com/join/CASH20)

## Exercise fees, and the daily-option exemption

Exercising an in-the-money option costs the smallest of three numbers: 0.02%, your taker fee tier, or 7% of the settlement value. At the regular tier the 0.02% almost always wins, so budget 0.02% of the contract's multiplier-adjusted value on exercised contracts. A VIP desk whose taker rate is below 0.02% pays its own lower rate instead.

The exemption is where most fee write-ups stop short. **Daily options, defined by OKX as options that do not expire on a Friday, carry no exercise fee.** If your strategy uses short-dated non-Friday expiries and you plan to hold them into settlement, that line item disappears entirely. For Friday expiries, keep 0.02% in the model. It shows up as a real cost on a large exercised position, and it is charged in BTC or ETH like everything else.

## Liquidation fees and the portfolio margin trap

A forced liquidation is charged the smaller of your taker tier or 7% of the mark price, applied across the multiplier, contract size and contract count. Liquidation is also where portfolio margin behaves in a way that surprises people. OKX calculates portfolio margin by risk unit, and BTC-USDT and BTC-USD are separate underlyings. Hedging BTC-USD options with a BTC-USDT perpetual produces **no margin offset**, because the two sit in different risk units. A trader who assumes the hedge reduces margin requirements will find the account sized as if the hedge did not exist.

The second PM detail is the liquidation sequence. PM liquidation starts with delta hedging, using perpetuals or futures to neutralise delta rather than dumping the options book directly. That protects option marks from slippage, but it also means a liquidation can leave you with a futures position you did not choose. Neither of these is a fee, and both cost more than the fee when they catch you out.

## How VIP tiers move the options rate

Tier qualification uses either total account assets or 30-day trading volume in the relevant market, whichever gets you higher. Global VIP 1 starts at 100,000 USD in assets or 1,000,000 USD of 30-day spot volume. EEA accounts that have opened a derivatives account are measured in euros, with VIP 1 at 100,001 EUR in assets or 1,000,001 EUR of volume. Options volume and total assets feed into the calculation, so a heavy spot trader can end up with a better options rate without trading more options.

The specific options rate for each VIP level lives on the Options tab of the live fee schedule, and that tab is the only figure worth quoting. Do not assume the options rate falls in the same increments as spot, and do not rely on claims about negative maker rates at high tiers unless you can see them on your own schedule. Holding OKB does not lower trading fees, and neither does a referral code, per OKX's Trading Fee Rules FAQ updated 9 September 2026. The code gets you an account; the tier gets you a rate.

## How the cost compares with other venues

Cross-venue comparisons get misleading fast, because an options fee is charged on premium while a spot fee is charged on notional. Keep the product categories separate.

MEXC publishes 0.0000% maker and 0.0500% taker on spot, 0.010% maker and 0.040% taker on standard futures, and a promotional 0.000%/0.020% on BTCUSDT perpetuals. It does not serve residents of the United States, the United Kingdom or the EEA, so those numbers are reference only for a large part of the audience. On a 1,000 USD spot taker order, OKX's global regular tier charges 1.00 USD against MEXC's 0.50 USD, or 0.40 USD with its token deduction. None of that tells you anything about options pricing, where the premium cap does most of the work.

Deribit is the usual benchmark for options liquidity, and its current schedule should be read on Deribit's own fee page. The verifiable structural difference is the cap: OKX's ceiling is 7% of premium, down from the 12.5% it charged before May 2025, and traders arriving from venues with a 12.5% ceiling notice it on cheap strikes. The daily-option exercise exemption is the second structural difference, and it is easy to miss when comparing headline maker and taker rates.

## Who should not trade options on OKX

- **Buy-only traders with small size.** Simple Options has no minimum capital and no liquidation risk on long positions. Do not push 10,000 USD into a multi-currency or portfolio margin account to buy calls you could have bought in the simple ticket.
- **Multi-leg traders under 10,000 USD per order.** RFQ requires 10,000 USD minimum per request and is not available in the app. Below that size, leg into the position on Options Chain and accept paying the standard rate per leg.
- **Anyone hedging BTC-USD options with BTC-USDT perpetuals and expecting margin relief.** The risk units are separate and the offset does not exist.
- **Traders whose entire edge depends on maker rebates.** The regular-tier options maker rate is 0.02%, one basis point below taker. Capture it with limit orders where the strategy allows, but do not build a plan around rebates you have not confirmed on your own Options tab.

## Questions that come up before the first trade

**Are OKX options fees charged in USDT?** No. BTC options settle in BTC and ETH options in ETH, and the fee is deducted in the same coin. The USDT-margined formula multiplies by the index price to express the same charge in stablecoin terms.

**Is there a fee to open and another to close?** Each fill is charged once at your tier, capped at 7% of premium. Closing a long option is another fill, so a round trip is two trading fees. Exercise is a third, separate charge, and it only applies if you exercise.

**Do I pay an exercise fee on every expiry?** Only on options that are actually exercised, and never on options that do not expire on a Friday.

**What is the smallest options trade I can place?** Simple Options and Options Chain have no minimum capital requirement for overseas KYC accounts. Mainland China KYC accounts need 10,000 USD to enable options trading beyond the simple interface, and RFQ needs 10,000 USD per request.

## How to decide, and what to check before you click buy

Match the channel to the order, then match the tier to your volume:

- Buying only, any size: Simple Options, no minimum capital, standard 0.02%/0.03% with the 7% cap.
- Buying and selling, single legs or manually legged spreads under 10,000 USD: Options Chain.
- Multi-leg or block size at 10,000 USD and above: RFQ, where the strategy gets quoted as a whole.
- Holding a large balance on the platform anyway: check whether assets alone put you at a higher VIP tier before you trade more volume to get there.

Two things to confirm on the day you trade. Open the Options tab of the live fee schedule and read the maker and taker rate for your own tier, since regional schedules and account types differ. Then check which schedule your account is on, because an EEA account without a derivatives account or a US account does not sit on the global rates quoted throughout this article.

👉 [Open your OKX account and read your own options rate before the first order](https://okx.com/join/CASH20)

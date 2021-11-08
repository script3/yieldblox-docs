# FX Forwards

![](../.gitbook/assets/fx-forwards-header.svg)

## What's an FX forward?

An [FX forward](https://www.investopedia.com/terms/f/forwardcontract.asp) (foreign exchange forward) is an agreement to exchange two assets at a future date at a set price. This functionality will not be available in the alpha release of YieldBlox; it will be included in the beta release.

## How does YieldBlox do FX forwards?

YieldBlox enables individuals and institutions to enter into forward contracts to lock in asset prices.

In YieldBlox, forward contract legs are tokenized so that they can be traded on the Stellar DEX. If users do not cover the short leg of their forward before the settlement date, the protocol seizes their [collateral](lending-borrowing/#what-is-collateral) and does not settle the long leg of their forward. Settlement failures are insured by YBX default protection.

## "Leg?" What's that?

A trader's FX forward position has two "legs", a short leg and a long leg. The short leg represents the assets the trader agrees to sell at contract expiration. The long leg represents the assets the user agrees to buy at contract expiration. To settle their forward contract, the trader must provide the assets that comprise their short leg by the contract's expiration date.&#x20;

## How does forward trading work?

Forward trading is a three-step process, forward origination, forward trading, and forward settlement.

### Forward origination

A user enters into a forward position by posting collateral and borrowing asset credits from the YieldBlox protocol. These credits represent the short leg of their forward. They are associated with an underlying asset and a settlement time. By borrowing the credits, they agree to cover the short leg of their forward contract by paying YieldBlox an amount of the credit's underlying asset equal to the number of credits borrowed by the credits settlement date.&#x20;

For example, say Trader A borrows 1000 USDC credits with a settlement time of 10:00:00 UTC, 10/20/2022. They're agreeing to pay YieldBlox 1000 USDC before 10:00:00 UTC, 10/20/2022. If they do not do so, they will forfeit their collateral, and YieldBlox will not settle any tokenized long legs they are holding.

### Forward trading

Users can trade forward legs they own for other forward legs with the same settlement date using the Stellar DEX. The credit tokens that make up forward legs have asset controls that ensure they are only tradeable for other credit tokens and cannot be transferred between accounts outside of a trade. As a result, all forward contract trades must be approved by a YieldBlox smart contract. When a trader trades the short leg of their forward for another trader's short leg, the leg they receive in the trade will become the long leg of the forward because the pool will pay them an amount of the credit's associated underlying asset equal to the number of credits they are holding at the credit's settlement date.&#x20;

For example, say Trader A takes their 1000 USDC credits and trades them for 800 EURT credits. They are obligated to pay YieldBlox 1000 USDC by the settlement date, and YieldBlox will pay them 800 EURT on the settlement date. Thus they have entered into a USDC:EURT forward contract with 1000 USDC as their short leg and 800 EURT as their long leg.

### **Forward settlement**

To settle forward contracts, traders cover their short leg by paying the associated underlying asset amount to YieldBlox. Once they do so, they create a DEX offer to sell all credit tokens they're currently holding (the trader's tokenized long leg) for the associated underlying asset. Both the repayment and offer creation are performed through a YieldBlox smart contract so that traders can't create this settlement offer without settling their short leg. At settlement time, YieldBlox will fill all of these offers, settling the long leg of all forward traders who have covered their short leg.&#x20;

For example, Trader A would cover their short leg by paying YieldBlox 1000 USDC. Then they would create an offer to sell their 800 EURT credits for 800 EURT. YieldBlox will fill the settlement offer by selling 800 EURT for 800 EURT credits at the settlement date.  As a result of this system, if a trader does not settle their short leg, they will not be able to settle their long leg as they will not be able to create a settlement offer for their credit tokens.&#x20;

If a trader does not settle their short leg, but the trader that is their forward contract counterparty does, it can create a settlement asset imbalance. In this case, YieldBlox will use a rebalancing mechanism to sell the delinquent trader's collateral and the overweight asset for the required settlement assets on the Stellar DEX.&#x20;

For example, say Trader A does not settle their short leg by paying YieldBlox 1000 USDC, but Trader B settles their short leg by paying YieldBlox 800 EURT. YieldBlox is now expected to pay Trader B 1000 USDC, but it has 800 EURT plus Trader A's confiscated collateral. YieldBlox will sell the 800 EURT and the confiscated collateral for 1000 USDC using the Stellar DEX then use the 1000 USDC to settle Trader B's position.  [YBX Default Protection](ybx-tokens/ybx-backstop.md#how-does-ybx-default-protection-protect-fx-forward-settlement) protects this settlement mechanism to ensure it never fails.&#x20;

## Can traders exit forward positions without settling them?

Yes! YieldBlox allows traders to settle their short legs by returning the borrowed credit tokens. So all a trader needs to do to exit a position without settling is to unwind their position, so they hold their original credit balance. For example, say Trader A borrowed 1000 USDC credits and traded them for 800 EURT credits. If they want to exit this position without settling, they can trade the 800 EURT credits for 1000 USDC credits then pay those USDC credits to YieldBlox, canceling their short leg. Traders can also use this mechanism to reduce the size of their forward position.

## Do I need collateral for an FX forward?

Yes. All users need to post collateral equal to 5-15% of the value of the short leg of their forward.

## What are the collateral requirements?

Forward contract parties must post collateral equal to 5-15% (dependent on the asset) of the value of the short leg of their forward. Like borrowing, forwards use a [health factor model](lending-borrowing/health-factors.md). If the user’s forward position falls in value and causes the user’s health factor to drop below 1.00, their position can be [liquidated](lending-borrowing/liquidations.md) by another protocol user. Liquidation profitability is ensured by [YBX default protection](ybx-tokens/ybx-backstop.md).

## What are the interest rates?

Forward contract interest rates use the same [demand-based interest](lending-borrowing/interest-rates.md) model as borrowing. However, **≈90%** of interest fees are used to repurchase and distribute [YBX tokens](ybx-tokens/) to [YBX stakers](staking.md).&#x20;

## How large can forward markets be

Forward contract market sizes are limited by the balance of the underlying asset in the lending pool. This is to prevent markets from getting too big for rebalancing to be feasible on the DEX.&#x20;

## Can I settle a forward in advance?

Yes. Once a user has covered the short leg of their forward, they can settle their forward contract in advance of the settlement period using YieldBlox borrowing. They can post their long leg as collateral and borrow the underlying asset from the protocol with a 100% loan-to-value ratio. When they perform this operation, they must pay the current fixed [interest rate](lending-borrowing/#how-do-loan-interest-rates-work) for the time period between the borrow and settlement date in advance.&#x20;

## How do forward contract liquidations work?

If a forward trader's[ health factor](lending-borrowing/health-factors.md) falls below 1.00, they can be liquidated by another protocol user. The liquidator will assume a portion of the trader's position to bring their health factor back up to 1.02 in exchange for a portion of the trader's collateral plus a [liquidation incentive](lending-borrowing/liquidations.md#what-incentivizes-liquidators-to-liquidate-undercollateralized-borrowers). Like borrower liquidations, forward liquidation profitability is ensured by the [YBX Default Protection](ybx-tokens/ybx-backstop.md) system.  \

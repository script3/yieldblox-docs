# Lending

## How does lending work on YieldBlox?

Lenders provide assets to the lending pool and receive interest in return. Borrowers can [borrow](borrowing.md) these assets by posting [collateral](borrowing.md#what-is-collateral) and paying interest at loan repayment.

Loans can be taken out for any time period, as long as the user maintains an account [health factor](./#whats-a-health-factor) above 1.00. If the accounts health factor falls below 1.00, the accounts loans can be [liquidated](liquidations.md) by another protocol participant until their account health factor increases to 1.02.

When a lender deposits money in the YieldBlox protocol, they receive pool tokens that act as a certificate of deposit. These tokens track the [proportion of the pools lending balance](../../technical-docs/math.md#pool-token-issuance) that the user owns. Users can burn these token at any time to withdraw their lent assets and all accrued interest.

## What are pool tokens?

When users deposit assets into the YieldBlox lending pool, they receive pool tokens which represent their [share of the balance](../../technical-docs/math.md#pool-token-issuance) of that asset in the lending pool. This is a sort of certificate of deposit. These tokens are Stellar assets, so they are transferrable and tradeable. The amount of underlying assets associated with these pool tokens increases over time, as borrowers pay interest into the lending pool. Lenders can burn these tokens to [withdraw their lent assets](../../technical-docs/math.md#asset-payout) along with their share of the interest accrued by the pool. Because interest is paid back into the pool, lenders' interest yields are auto-compounded.

Pool tokens are also used as collateral. Borrowers collateralize pool tokens they receive from depositing assets in the lending pool. Once they repay their loan (or a portion of their loan), they can withdraw their collateralized pool tokens (or a portion of their collateralized pool tokens). Because pool tokens are used as collateral, YieldBlox can lend the underlying assets associated with collateralized pool tokens. As a result, borrowers receive interest on collateral deposits.

## Why would users lend on YieldBlox?

In exchange for lending with YieldBlox, lenders receive interest from borrowers and [YBX](../ybx-tokens/#how-do-i-get-ybx-tokens) issuance from the protocol. In addition, when lending on YieldBlox, users retain control of their funds. The protocol is decentralized, trust-free, and non-custodial. Only the protocol smart contracts have control over user funds, and users can withdraw their funds at any time.

Lenders should note that to receive YBX issuance, they must deposit the pool tokens they received from lending as collateral.

## What is the interest rate for lending on YieldBlox?

Lending interest rates equal the _borrowing interest rate_ multiplied by the _utilization ratio_ since interest paid by borrowers is distributed proportionally to lenders. Borrowing interest rates are [demand-based](interest-rates.md#how-do-loan-interest-rates-work) and calculated using the utilization ratio. This means borrowing interest rates increase as the percentage of protocol assets lent to borrowers increases. Currently, an asset's borrowing interest rate ranges from 5% at 0% utilization to over 100% at 97%+ utilization. However, [governance proposals](../governance.md) can modify the rate at which interest rates adjust based on utilization rates.

## How do lenders receive interest?

Borrowers pay their accrued interest into the lending pool when they repay their loan. When lenders withdraw their lent assets, they also withdraw their share of the interest earned by the pool. This works because interest is paid into the lending pool and pool tokens represent a user's share of the pools balance of the lent asset. So, when interest is paid into the pool, the [amount of the underlying asset](../../technical-docs/math.md#asset-payout) associated with a pool token increases.

## Who controls my lent assets?

You do! Assets lent to the protocol are controlled by YieldBlox's smart contracts. Therefore, you can use those smart contracts to withdraw your lent assets at any time.

## What assets can be lent?

Any Stellar-based asset approved by [protocol governance](../governance.md) can be lent with YieldBlox. More assets will be added to the protocol over time through governance proposals voted on by YBX holders.

## How do lenders withdraw lent assets?

Lenders can withdraw assets by using YieldBlox's smart contracts to burn the pool tokens they received for lending assets. Doing so will also withdraw all interest the lender has accrued.

## Is there any situation where lenders can't withdraw assets?

If an assets utilization ratio is too high, there may not be sufficient liquidity for a lender to withdraw assets because too much of the asset balance is currently lent out. However, due to YieldBlox's [demand-based interest rate model](interest-rates.md), this is extremely unlikely. Interest rates are extremely high (over 100%) at high utilization ratios, which heavily incentivizes borrowers to repay their loans and new entities to lend to the protocol, thus adding liquidity and lowering the utilization ratio.

# Borrowing

## How does borrowing work on YieldBlox?

When borrowing, users deposit assets into the lending pool and withdraw assets they wish to borrow from the pool. To repay, the borrower returns the borrowed assets to the lending pool. Then they are allowed to withdraw their collateral if they choose.

## What is collateral?

Collateral is the assets the borrower pledges to secure the repayment of a loan. If a loan ever becomes undercollateralized, meaning its repayment is at risk, the loan is liquidated, and a portion of the borrower's collateral is forfeited. YieldBlox uses [pool tokens ](lending.md#what-are-pool-tokens)as collateral. This means that borrowers will receive interest on their collateral deposits!

## What is accepted as collateral?

Any asset on [Stellar's network](https://developers.stellar.org/docs/start/introduction/) that has been approved by protocol [governance](../governance.md) can be converted into pool tokens and used as collateral.

## How much collateral do I need?

Borrowers must have a [health factor ](health-factors.md)of above 1.10 after loan origination in order to borrow assets from YieldBlox. They must maintain a health factor of above 1.00 in order to avoid liquidation. Health factors are based on a collateral assets loan-to-value ratio, so collateral requirements vary depending on the asset the user is collateralizing. Loan-to-value ratios are set by governance proposals, so they can change.

## What happens to the collateral?

The assets provided for collateral are converted into pool tokens, so they can be lent out. This allows borrowers to generate interest on their collateral deposits. These pool tokens are then locked in claimable balances claimable by only the pool account. Collateralized pool tokens can be reclaimed by the borrower once they repay their loan. In the case of a liquidation, liquidators will withdraw the collateralized [pool token](../../technical-docs/math.md#pool-token-issuance) rather than its associated underlying asset.

## How do I repay my loan?

Borrowers repay loans by returning all borrowed assets and accrued interest to the YieldBlox lending pool. After doing so, they can withdraw their collateral deposits if they wish.

## Can borrowers repay only part of their loan?

Yes! Borrowers can repay portions of loans at any time. Doing so also lowers their collateral requirements allowing them to withdraw collateral if they wish to.&#x20;

## Can I repay my loan with collateral?

Yes! YieldBlox enables borrowers to repay loans with collateral. The protocol sells as much collateral as necessary to repay the loan, and the user can withdraw the remainder.

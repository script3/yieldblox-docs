# Liquidations

## What is a liquidation?

If a borrower's loan becomes undercollateralized \(their [health factor](./#whats-a-health-factor) falls below 1.00\), another protocol user can repay a portion of the borrower's debt in exchange for a portion of their collateral. This is known as [liquidation](../../technical-docs/math.md#maximum-liquidation-amount). 

## When would a borrower be liquidated?

Borrowers can be liquidated if their account's health factor falls below 1.00. The [health factor](./#whats-a-health-factor) is a measure of an account's collateralization levels and is calculated with a user's liability value, collateral value, the average collateral liquidation factor, and the average collateral liquidation incentive.

## How do YieldBlox liquidations protect borrowers?

Being liquidated is never fun. YieldBlox protects borrowers [by only allowing liquidators to liquidate the borrower's position to the point where their health factor reaches 1.02](../../technical-docs/math.md#maximum-liquidation-amount). This minimizes liquidation amounts ensuring that the borrower loses the smallest amount of collateral possible.

## Who liquidates the borrowers?

Any other protocol user may liquidate borrowers. The borrower can only be [liquidated to the point where their health factor reaches 1.02](../../technical-docs/math.md#maximum-liquidation-amount). Because of this, borrowers are unlikely to have their positions fully liquidated.

## What incentivizes liquidators to liquidate undercollateralized borrowers?

To incentivize liquidations of undercollateralized accounts, liquidators receive a discount on the assets they withdraw from the borrower's collateral based on the collateralized asset's liquidation incentive. For example, if a liquidator repays 100 USD of a borrower's position, and the borrower's collateral has a liquidation incentive of 1.05, the liquidator is permitted to withdraw 105 USD worth of the collateralized asset. The [governance system](../governance.md) sets the liquidation incentive for each asset supported by YieldBlox.

## Can liquidators liquidate positions using the borrower's collateral?

Yes, YieldBlox allows liquidators to use borrower's collateral to repay their debts by burning the collateralized pool tokens and trading the underlying collateral assets for the necessary assets for repayments on the DEX. In this case, the liquidator will withdraw the borrower's collateral as the collateralized pool token's underlying asset rather than as pool tokens.

## What if the liquidated borrower does not have sufficient collateral to support the liquidation incentive?

In cases of extreme volatility, it is possible for the liquidation incentive to be impossible to pay out under normal market conditions. This could happen if the value of the user's liability increased drastically in a very short amount of time, or the value of the user's collateral fell rapidly. To ensure the undercollateralized loan is still liquidated, YieldBlox uses the [YBX backstop system](../../technical-docs/protocol.md#ybx-backstop). 


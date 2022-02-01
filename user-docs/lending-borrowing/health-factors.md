# Health Factors

## What's a health factor?

An account's _health factor_ is a measure of the account's collateralization levels. It is based on the account's total liability value, collateral value, and collateral liquidation factors.

To originate a loan, a user must ensure their health factor will be above 1.10 after the loan has been originated. If a user account's health factor falls below 1.00, its positions can be liquidated until its health factor reaches 1.00. See a rough health factor scale below:

![](<../../.gitbook/assets/health factor scale.svg>)

An accounts health factor is calculated with a user's liability value (outstanding loan value + accrued interest), collateral value, the average loan-to-value ratio of their collateral, and the average collateral liquidation incentive using [this formula](../../technical-docs/math.md#health-factor).

$$
H=\frac {\sum^{|C|}_{i=1}Fi*V_{ci}} {\sum^{|L|}_{i=1}V_{li}}
$$

Where:\
$H=$ the account's health factor\
$|C|=$ the number of collateralized assets held by the account\
$F_i=$ the liquidation factor for collateral asset $i$ \
$V_{ci}=$ the collateral value of collateral asset $i$ \
$|L|=$ the number of outstanding loans held by the account\
$V_{li}=$ the liability value of loaned asset $i$

Liquidation factors are assigned to supported assets by the protocol, and they govern the point at which an account's positions can be liquidated.

## How can I increase my health factor?

A user can increase their health factor by depositing more [collateral](./#what-is-collateral) or decreasing their liability value (e.g. repaying their loans).

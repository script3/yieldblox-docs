# Default Protection

The YBX Default Protection program is used to eliminate counterparty risk from the YieldBlox protocol. It enables the protocol to take on user debt to ensure that liquidations are profitable.

## How does YBX Default Protection remove counterparty risk?

In the case a [liquidation](liquidations.md#what-is-liquidation) would be unprofitable for the liquidator, the lending pool will assume a portion of the liquidated user's debt to reduce the amount the liquidator must repay. This ensures liquidations are always carried out no matter how underwater a position is. The pool will slowly pay off its debt using fees it would normally distribute to YBX escrowers.

## How much debt will the pool take on during a default protection scenario

When a liquidator attempts a liquidation the pool calculates the average liquidation incentive of the collateral held by the user being liquidated. If the value of the user's liabilities exceeds the value of the user's collateral value divided by one plus the user's liquidation incentive, the pool will assume debt equal to the difference. See the equation [here](../../math.md#Yieldblox-Default-Protection-Amount).

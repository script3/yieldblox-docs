# Default Protection

The YBX Default Protection program is used to eliminate counterparty risk from the YieldBlox protocol. It enables the protocol to take on user debt to ensure that liquidations are profitable.

## How does YBX Default Protection remove counterparty risk?

In the case a [liquidation](liquidations.md#what-is-liquidation) would be unprofitable for the liquidator, the lending pool will assume a portion of the liquidated user's debt to reduce the amount the liquidator must repay. This ensures that liquidations are always carried out no matter how underwater a position is. The pool will slowly pay off its debt using fees it would normally distribute to YBX escrowers. Note: this assumes that fees are non-0. &#x20;

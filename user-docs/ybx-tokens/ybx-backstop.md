# YBX Default Protection

The YBX Default Protection program is used to eliminate counterparty risk from the YieldBlox protocol. It enables the protocol to use YBX as a reserve asset to ensure liquidations and FX forward settlements are successful.

## How does YBX Default Protection remove counterparty risk?

In the case a [liquidation](../lending-borrowing/liquidations.md#what-is-liquidation) would be unprofitable for the liquidator, or an FX forward settlement would be impossible, the protocol will sell YBX accrued by the YBX staking pool from [fee distributions](ybx-tokenomics.md#level-1-users-can-stake-ybx-to-earn-a-portion-of-yieldblox-protocol-revenue) to ensure the liquidation is profitable, or the FX forward settlement is successful. A maximum of 20% of the staking pool can be sold this way. If this amount is insufficient, the protocol will mint new YBX to cover the remaining deficit.&#x20;

![](https://lh4.googleusercontent.com/5cYyUTtNVNem73p1avk2WK0k5gWvrMcTjo5obymnSbXcqdWN3qHOxMzOzT6eCa9RY7zevAz-j7uaZni67gdwUGP1x2NCYgmjzKeUpGwzLlPuqJHgtTTFKAfa8Jtf4evFNKCr2JuvOss)

## How does YBX Default Protection protect liquidations?

YBX Default Protection ensures [liquidations](../lending-borrowing/liquidations.md) happen by guaranteeing their profitability for liquidators. Say a user’s loan is too underwater for the base liquidation incentive to make it profitable for a liquidator to liquidate. YieldBlox will sell YBX on the Stellar DEX to repay a portion of the loan so the liquidator has less to repay. This backstop mechanism ensures the liquidation is profitable.

## How does YBX Default Protection protect FX forward settlement?

YBX Default Protection ensures [FX Forwards](broken-reference) are always correctly settled. Suppose a forward contract party fails to settle their leg of a forward. In this case, YieldBlox will attempt to trade the delinquent user’s collateral and the settled legs capital (provided by the other party in the forward) for the required settlement assets on the DEX. If high slippage makes this trade impossible, the protocol will also sell YBX to reach the required settlement asset amount.

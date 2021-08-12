---
description: >-
  High-level rational decision making with YBX tokens and the YieldBlox
  protocol.
---

# Game Theory of YBX

## How can I get the most value out of my YBX?

A user can essentially do five actions with YBX tokens, each one impacting the protocol and, therefore, the value of the YBX they have. The more participation within YieldBlox, the better it is for all parties involved. These actions are highlighted in the [Five Levels of YieldBlox Productivity](ybx-tokenomics.md#the-five-levels-of-ybx-productivity), the effects these actions have on the protocol and the benefits they have can be illustrated with game theory. 

The five actions a user can do with YBX \(simplified\):

* Sell \(-\)
* Hold \(+\)
* [Stake](ybx-tokenomics.md#level-1-users-can-stake-ybx-to-earn-a-portion-of-yieldblox-protocol-revenue) \(++\)
* Stake + [Vote](ybx-tokenomics.md#level-4-users-can-use-sybx-to-vote-on-the-allocation-of-ybx-incentives-to-different-lending-pools) \(+++\)
* Stake + Vote + [AMM](ybx-tokenomics.md#level-4-users-can-use-sybx-to-vote-on-the-allocation-of-ybx-incentives-to-different-lending-pools) \(+++++\)

In the above list, anything from "Hold" and below is seen as a positive outcome \(increasing in benefit as one goes down the list\), and "Sell" is a negative outcome. The positivity of these actions takes the following goals into mind: users want to profit, the protocol wants high liquidity to repurchase and sell YBX easily through its [staking](../staking.md#how-does-staking-work-on-yieldblox) and [default protection](ybx-backstop.md#how-does-ybx-default-protection-remove-counterparty-risk) functions, and the protocol and users want to minimize YBX selling pressure to ensure the default protection system is effective. Each user wants the most positive outcome for them and the protocol.

Let's say there are two users who both have YBX. Their action strategies can be seen here:

![](../../.gitbook/assets/ybx-game-theory-3x%20%281%29.png)

If they both claim YBX and do nothing with it \(hold\), it is seen as a positive outcome \(1,1\). The protocol still functions as it is supposed to, and users still get their YBX for lending or borrowing. Therefore, the protocol would see the base positive outcome of \(1,1\) \(1 +1 = 2\).

If both users [stake](../staking.md) their claimed YBX, a more positive outcome \(over just holding YBX\) occurs \(2,2\). This has the same benefits of holding, but stakers gain more benefits. Users staking their YBX for sYBX earn interest for staking since they receive a portion of protocol fees. Additionally, the threat of selling pressure is reduced, allowing default protection to function optimally. These actions result in the second positive outcome of \(2,2\) \(2 + 2 = 4\).

If both users stake their claimed YBX and [vote](../governance.md) on YieldBlox governance proposals, the third positive outcome occurs \(3,3\). Both users still see the rewards of staking YBX for sYBX, but the protocol is now guided by their decisions, allowing them to increase their control and [allocate YBX incentives](../governance.md#ybx-incentive-allocations) where they see fit. This results in a fairly positive outcome for the users, \(3,3\) \(3 +3 = 6\).

Now let's say both users stake and vote, but they also utilize automated market makers to stake [AMM shares](ybx-tokenomics.md) on YieldBlox. This is the maximum positive outcome for all parties \(5,5\). Not only do the users gain their share of protocol revenue, but they also get to claim trading fees from the AMM shares. This is also hugely beneficial for the protocol, as it provides maximum liquidity for the staking and backstop functions. The most positive outcome occurs if both users use this strategy, \(5,5\) \(5 + 5 = 10\).

When both users sell, the worst outcome occurs \(-5,-5\). This is detrimental to the protocol and users. The protocol's staking and backstop mechanisms do not function as well, and users will not be able to claim the benefits of staking YBX, vote on governance proposals, or receive AMM trading fees. If this outcome occurs, the total benefit score is -10.

Of course, not every user will use the same strategy. Other combinations of strategies can be seen in the visual above.


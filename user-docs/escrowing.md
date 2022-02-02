# Escrowing

![](<../.gitbook/assets/staking header.svg>)

## What is escrowing?

Escrowing is locking [YBX tokens](ybx-tokens/) for a period of time in exchange for voting escrowed YBX tokens, veYBX.

## Why would I escrow?

YieldBlox users escrow their [YBX tokens](ybx-tokens/) for veYBX which have the ability to vote on YieldBlox [governance proposals](governance.md). Governance proposals can determine key protocol functionalities like upgrades, supported assets, YBX allocations, and more! There is also a portion of YBX emissions that get paid out to users who escrow their YBX. Basically, users can earn YBX tokens passively and control protocol development - just for having YBX.

## How does escrowing work on YieldBlox?

[YBX token](ybx-tokens/) holders can escrow their YBX in exchange for veYBX. Their YBX is locked for a 3 month, 6 month, or 1 year time period in the YBX escrow pool. After the escrow lockup ends, the user can exchange their veYBX for the original amount of YBX they locked plus any YBX earned from YBX issuance or fees over the lock period.

The protocol also allows users to unlock any escrowed YBX before the time period is up. However, early unlocked YBX is not eligible to collect fees earned over the time period. Further, there is a small penalty applied to avoid potential voting exploits.

![](<../.gitbook/assets/staking (4).svg>)

## How do I escrow on YieldBlox?

If a user holds any [YBX tokens](ybx-tokens/), they can escrow them through the YieldBlox protocol.

Currently, you can escrow YBX for 3 different lock periods. Each of these lock periods correlates to a different amount of veYBX you will be issued per YBX locked.

| Lock Period |   veYBX Issuance   |
| :---------: | :----------------: |
|  3 months   | 0.25 veYBX per YBX |
|  6 months   |  1 veYBX per YBX   |
|  12 months  | 4.00 veYBX per YBX |

Consider the example where a user whishes to escrow lock 100 YBX for 3 months. Once they escrow-lock the YBX through the YieldBlox protocol, their YBX is locked in a claimable balance only the protocol can claim. They also receive 25 veYBX in their account they can now use to vote in [governance proposals](governance.md).

## How do I unlock escrowed YBX on YieldBlox?

A user can unlock any escrowed YBX they have through the YieldBlox protocol. They can unlock this position regardless of how recently it has been originally locked.

If the escrowed position has completed the Lock Period associated with it, unlocking returns the full amount of YBX to the user _plus_ any fees or emissions earned by the escrow locked YBX. These fees are captured by converting the veYBX issued by the escrowed position into YBX!

If the escrowed position has NOT completed the Lock Period associate with it, unlocking works a bit differently. They receive the original escrow amount, minus some penalty, and do not get any fees they generated during the escrow period.

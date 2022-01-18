# Escrowing

![](<../.gitbook/assets/staking header.svg>)

## What is escrowing?

Escrowing is locking [YBX tokens](ybx-tokens/) for a period of time in exchange for voting escrowed YBX tokens, veYBX.

## Why would I escrow?

YieldBlox users escrow their [YBX tokens](ybx-tokens/) for veYBX which have the ability to vote on YieldBlox [governance proposals](governance.md) which includes voing on YBX issuance allocations. In the future protocol, fees may also be paid to YBX escrowers. Basically, users can earn YBX tokens passively and control protocol development-- just for having YBX.

## How does escrowing work on YieldBlox?

[YBX token](ybx-tokens/) holders can escrow their YBX in exchange for veYBX. Their YBX is locked for a 3 month, 6 month, or 1 year time period in the YBX escrow pool. After the escrow lockup ends, the user can exchange their veYBX for the original amount of YBX they locked plus any YBX earned from YBX issuance or fees over the lock period.&#x20;

In the future, a YBX fee allocation may be toggled on. This would mean a portion of protocol fees may be used used to repurchase YBX on the Stellar DEX and send it to the YBX escrow pool. This staking pool is proportionally distributed to veYBX holders when their escrow period ends. Through this repurchase mechanism, YBX escrowers earn a portion of protocol revenue.

![](<../.gitbook/assets/staking (4).svg>)

## How do I escrow on YieldBlox?

If a user holds any [YBX tokens](ybx-tokens/), they can escrow them on the YieldBlox web app.

When a user connects their [wallet](general.md#what-do-i-need-to-use-yieldblox), their Account Overview will be on the first section of every page. The rightmost section of the Account Overview is _Escrowed YBX_. This section will show the YBX issuance allocated to YBX escrows, the amount of escrowed YBX (veYBX) the account has, and the amount of YBX the account has.

Once the 'Manage' button is selected, an escrow modal will appear. There, a user can enter the amount of the YBX they'd like to escrow and the time period they'd like to lock it for. A user can lock their YBX for three months, six months, or a year -- the longer it's locked, the more veYBX a user gets.&#x20;

Locking for 3 months has a 1.00x ve multiplier, locking for 6 months has a 1.50x ve multiplier, and locking for 1 year has a 4.00x ve multiplier. After users decide on a lockup period, they select 'Submit' and sign the transaction in their wallet.

In the example above, a user escrows 100 YBX. The ve multiplier is multiplied by the lockup period multiplier and the number of escrowed YBX. The lockup period multiplier is based on one year (e.g. 1 year has a lockup period multiplier of 1, 6 months (1/2 year) has a lock-up period multiplier of 0.5, etc.). The product of this equation is the number of veYBX tokens a user will receive for escrowing (equation below). If they lock for 3 months, they will receive 25 veYBX. If they lock for 6 months, they will receive 75 veYBX. If they lock for 1 year, they will receive 400 veYBX.

$$
veYBX_{received} = Y * L * YBX_{escrowed}
$$

Where:\
$$Y=$$ the yield multiplier\
$$L=$$ the lockup period\
$$YBX_{staked} =$$ the YBX escrowed

Technical users can also stake by interacting with the YieldBlox smart contracts directly through Stellar Turrets.

## How do I unlock escrowed YBX on YieldBlox?

If a user wishes to un-escrow their YBX, they should select the 'Manage' button in the escrow section of their Account Overview. The escrow modal will appear. Once there, the user should toggle to 'Unlock.'

A user will be shown how much veYBX they have unlocked. This number is the amount of veYBX the user can unlock for YBX. They will also be shown their next unlock period -- how long they have until they can unlock their next YBX escrow.&#x20;

Technical users can also unlock by interacting with our smart contracts directly through Stellar Turrets.

## Can I unlock early?

Yes. Users can unlock early if they want to receive the original amount of YBX they escrowed. However, they will forfeit any additional YBX earned over the escrow period so far.


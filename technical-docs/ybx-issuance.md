# YBX Issuance

YBX issuance is the process by which platform YBX incentives are paid out to protocol lenders (only lenders with collateralized deposits receive YBX incentives), borrowers, and escrowers. Issuance is paid out daily and tracked and distributed with 2 different processes, Issuance Tracking and YBX Claims.

### Issuance Tracking

Issuance tracking tracks the amount of YBX that should be distributed to each user on a given issuance period(day). To do so, the protocol uses issuance tracker trades made by the UPDATE operation in the Claim contract. The issuance tracker trades track a pool or liability tokens [issuance ratio](math.md#Issuance-Ratio), or the amount of YBX issued per pool or liability token of that type for the given issuance period. These trades exchange an assets [issuance ratio tracker token](yieldblox-protocol-assets.md#Pool-Issuance-Ratio-Tracker-Token) for its [issuance shift tracker token](yieldblox-protocol-assets.md#Pool-Issuance-Shift-Tracker-Token). The trades track the issuance ratio floating point style, the amount of ratio tokens sold is equal to the mantissa of the issuance ratio, and the amount of shift tokens sold is equal to that mantissa's exponential. The exponential amount is added to 15 to avoid numbers less than 0.

For example, if a pool tokens issuance ratio for a period is 12.1, the issuance trade will exchange 1.21 ratio tracker tokens for 14 shift tracker tokens.

### YBX Claims

Users claim YBX accrued to a given position whenever they modify the position or run the CLAIM operation in the Claim contract. To calculate accrued YBX, the protocol uses the following process

1. Check the last block the claimable balance for the position was modified.
2. Pull every trade involving the ratio and shift assets associated with the protocol token representing that position made after the block found in step 1.&#x20;
3. Calculate the amount of YBX accrued by taking the sum of the following:
   1. The position size times the most recent issuance trade ratio times the percent of the current period that has elapsed
   2. The sum of each trade ratio in the set except the most recent one times the position size
   3. The farthest back issuance trade ratio times the position size times the percent of the period that elapsed between when the position was modified and when the farthest back trade ocurred.

We'll provide an example below:

Position: 100,000 l00XLM liability Position - last updated on 12/12/2021 - 12:00 UTC - Event timestamp is 12/15/2021 - 18:00 UTC

Set of YBX issuance trades for l00XLM

1. &#x20; ratio: 0.5 - 12/13/2021 - 00:00 UTC
2. ratio: 1.5 - 12/14/2021 - 00:00 UTC
3. ratio: 2 - 12/15/2021 - 00:00 UTC

YBX issuance for the position equals:&#x20;

(((18/24)\*100,000\*2+100,000\*1.5+100,000\*0.5+(12/24)\*100,000\*.5 = 375,000

Astute observers will have noticed this can result in users missing out on a small amount of issuance if they modify a position many times during one issuance period. This is an unfortunate side effect of us being unable to overload the Claim contract with API calls.

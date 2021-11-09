# YBX Issuance

YBX issuance is the process by which platform YBX incentives are paid out to protocol lenders (only lenders with collateralized deposits receive YBX incentives), borrowers, and stakers. Issuance is paid out daily and tracked and distributed with 2 different processes, Issuance Tracking and YBX Claims.

### Issuance Tracking

Issuance tracking tracks the amount of YBX that should be distributed to each user on a given issuance period(day). To do so, the protocol uses issuance tracker payments made by the UPDATE operation in the Claim contract. These payments pay issuance tracker assets to the issuance tracker accounts. The payment amount equals the issuance ratio (see math) for the protocol token (pool token or liability token) associated with the issuance tracker asset.

### YBX Claims

Users claim YBX accrued to a given position whenever they modify the position or run the CLAIM operation in the Claim contract. To calculate accrued YBX, the protocol uses the following process

1. Check the last block the claimable balance for the position was modified.
2. Pull every issuance tracker payment made to the issuance tracker account associated with the protocol token representing that position after that block.&#x20;
3. Calculate the pessimistic block-weighted average position size of the user. This is necessary to prevent gaming the issuance system by depositing/borrowing right before issuance and withdrawing/repaying right after.
   1. The contract calculates the pessimistic block-weighted average position size using the block of the earliest issuance payment in the set as the most recent issuance payment block input. See Math.
      1. Contract checks the result meta XDR of the transaction that last modified the position to get the necessary information for this calculation.
4. Multiply the calculated position size by the issuance ratio from the earliest issuance payment in the set. Then add that product to the sum of the products of the last position size times all other issuance ratios in the set. The result is the users pending YBX for the position.

We'll provide an example below:

Most recent position: 100,000 l00XLM liability Position - last updated on block 1000

* Previous position was 50,000 l00XLM - last updated on block 750

Set of YBX issuance payments for l00XLM

1. &#x20;.0005 b00XLM - block 500
2. .0006 b00XLM - block 1250
3. .00065 b00XLM - block 2000
4. .00075 b00XLM - block 2750

YBX issuance for the position equals:&#x20;

((50,000\*(1000-750)+100,000\*(1250-1000))/(1250-750))\*.0006+100,000\*.00065+100,000\*.00075 = 185

Astute observers will have noticed this can result in users missing out on a small amount of issuance if they modify a position many times during one issuance period. This is an unfortunate side effect of us being unable to overload the Claim contract with API calls. We're hopeful that we can improve this system in the future so that this will no longer be a possibility.

### Circulating YBX

Below is a visual of circulating YBX for the first five years. It includes YieldBlox app issuance, initial investor issuance, team issuance, and the YBX airdrop. While not included, the YieldBlox DAO Treasury, bug bounty, and partnership treasury allocations account for 37.33% of total YBX.&#x20;

![](<../.gitbook/assets/ybx circulating 5year@3x.png>)

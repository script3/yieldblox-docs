# YBX Tokens

![](<../../.gitbook/assets/YBX tokens header (1).svg>)

## What are YBX tokens?

YBX tokens are the YieldBlox protocol's utility tokens. They are used to govern the protocol, to direct issuance, and as collateral.

## What is the YBX issuer address?

YBX issuer address is&#x20;

****[**GBUYYBXWCLT2MOSSHRFCKMEDFOVSCAXNIEW424GLN666OEXHAAWBDYMX**](https://stellar.expert/explorer/public/asset/YBX-GBUYYBXWCLT2MOSSHRFCKMEDFOVSCAXNIEW424GLN666OEXHAAWBDYMX)****

## How many YBX tokens are there?

There are a total of 1,500,000,000 YBX tokens to be allocated.

## How do I get YBX tokens?

Users receive YBX tokens just for using the YieldBlox Protocol. They must claim them to receive their issued YBX.

## How do I claim my issued YBX tokens?

If a protocol user has been issued YBX tokens, they can claim them by calling the YieldBlox Protocol claim contract. It is recommend to claim issued YBX weekly.

## Can I buy YBX tokens?

Yes. The main way to receive YBX tokens is to [lend or borrow](../lending-borrowing/) on YieldBlox, but YBX tokens are Stellar tokens, so anyone can trade them on the [Stellar DEX](https://www.stellar.org/tools?locale=en#trade-on-the-stellar-dex).

## What can I do with YBX tokens?

Users can escrow YBX tokens in exchange for veYBX. veYBX allows users to earn a portion of YBX issuance (which may be directed to escrows), as well as [vote](../governance.md#how-does-voting-work) on and create governance [proposals](../governance.md#how-are-protocol-change-proposals-created), there is also a mechanism by which veYBX accrues protocol fees.

## How are YBX tokens distributed?

YBX tokens are distributed daily to users for [lending](../lending-borrowing/), [borrowing](../lending-borrowing/#how-does-borrowing-work-on-yieldblox), or [escrowing](../escrowing.md) on the YieldBlox Protocol. **Only lenders who collateralize the lent asset are eligible for YBX issuance.**

![](<../../.gitbook/assets/dist scheme @3x.png>)

The YBX issuance equation is used to calculate the number of YBX tokens to distribute. Once this equation finds this distribution number, each lender, borrower, or escrower will be allocated a percentage of YBX tokens based on the issuance allocation percentage for an asset. Each asset's issuance allocation percentage is a set constant controlled by YBX token holders. After the protocol knows an assets lending and borrowing allocation percentage, lenders or borrowers of that asset can claim YBX tokens proportionally based on the percent of all lending or borrowing they contribute for that asset. It should be noted that YBX issuance to escrows is sent directly to the escrow pool where it is claimed after the user unlocks their YBX escrow. See the Technical Documentation on [YBX Issuance](../../technical-docs/ybx-issuance.md) for more information on how this process functions.

_**Example visualized:**_

A user lent or borrowed on YieldBlox the week prior to _date x_. The issuance equation finds that 100,000 YBX tokens are to be issued on _date x_.

![](<../../.gitbook/assets/ybx issuance exampl - simple@3x (1).png>)

Now there are 100,000 YBX tokens to be allocated. Let's say there are four assets being lent in YieldBlox on _date x_, and they all have equal allocation percentages (25%) (in this example we assume no issuance is directed to escrows or borrowers). The user is lending and collateralizing _Asset 1_, and they contributed 5% of the total amount of Asset _1_ lent and collateralized. Then the total number of YBX tokens the user would be eligible to claim is:

(YBX-issued) \* (Lending Asset 1's allocation percentage) \* (User percentage contributed to the lent and collateralized amount of Asset 1)

\= (100,000) \* (25%) \* (5%)

\= 1,250 YBX tokens

![](<../../.gitbook/assets/issuance example@3x.png>)

The user in this example would receive 1,250 YBX tokens on the distribution date of _date x_. These numbers are for explanatory purposes and may or may not reflect real YBX token issuance.

## What is the issuance equation?

The issuance equation is used to calculate the total tokens (YBX) to be issued for a given period. This equation is a negative inverse proportion function.

The number of tokens issued decreases as the number of outstanding tokens increases. The curve also adjusts for any additional issuance or burning of YBX tokens. Though, additional issuance can only occur through a governance proposal. See the issuance equation below:

$$
I=(T-O) * R
$$

Where:\
$$I=$$ the YBX issuance of the current period\
$$T=$$ the total number of YBX tokens to be issued; 1,500,000,000\
$$O=$$ the number of YBX tokens outstanding\
$$R=$$ the YBX issuance rate; initially 0.0075

## Is there an initial YBX token distribution?

Yes, there will be an initial distribution of YBX tokens. The distribution will be a total of 69,000,000 YBX tokens. It will be distributed to the YieldBlox DAO, early contributors to the YieldBlox protocol, a bug bounty, marketing efforts, and Stellar ecosystem members! The initial investor token allocation will be locked for a year, and the initial team allocation will be locked for 4 years following a linear unlock schedule with a one year cliff. The YieldBlox DAO Treasury allocation is directly controlled by the YieldBlox [governance system](../governance.md).

After the initial distribution, the remaining 810,000,000 YBX tokens will be distributed to protocol lenders and borrowers. So overall, 92% of all YBX tokens will be distributed directly to the community!

![](<../../.gitbook/assets/YBX allocation final@3x (1).png>)

## How much YBX will be in circulation?

Below is a visual of circulating YBX for the first five years. It includes YieldBlox Protocol issuance, initial investor issuance, team issuance, and the YBX airdrop. While not included, the YieldBlox DAO Treasury, bug bounty, and partnership treasury allocations account for 37.33% of total YBX.

**Please Note:** This is a "pessimistic" estimate as it assumes no YBX issuance will be paid to YBX escrows. Which likely will not be the case.

![](<../../.gitbook/assets/image (25).png>)

## Was there a YBX airdrop?

Yes. The initial distribution allocated to ecosystem user marketing was partially distributed through an airdrop. The rest will be distributed through various giveaways.

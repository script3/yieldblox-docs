# Governance

![](<../.gitbook/assets/governance header (1).svg>)

## How does governance work on YieldBlox?

The YieldBlox protocol is updated and maintained using a DAO governance token model. Users receive [YBX tokens](ybx-tokens/) for [lending or borrowing](lending-borrowing/), and these tokens can be escrowed for veYBX. veYBX tokens have governance power that can be used to make and vote on protocol updates and changes.

While veYBX holders have the real governance power, there is also a YieldBlox security council that holds gYBX tokens. These tokens carry voting power like veYBX tokens do. In addition, they can be used to create and vote on signer swap and freeze contract proposals. These proposals are limited in their functionality, they exist to provide an additional security layer that protects YieldBlox from smart contract bugs or malicious signers. More details on these proposal types can be found in the Governance Proposals section.

## How does the protocol change?

The YieldBlox protocol is controlled by [YBX token](ybx-tokens/) escrows, who hold veYBX tokens and makeup the YieldBlox DAO. Holders of veYBX tokens can propose, vote on, and implement changes to the protocol. Proposals can modify existing protocol parameters or add entirely new functionalities to the protocol. To create a proposal, a user must control at least 0.001% of total outstanding voting power (the sum of veYBX and gYBX outstanding).

Once a user submits a proposal to change the protocol, users have three days to vote on whether to implement or reject the proposal. If the proposal is accepted for implementation, it is queued with a 2-day time delay before being implemented.

![](<../.gitbook/assets/gov flow@3x.png>)

## How does voting work?

Users have three days to vote on proposals. They vote 'YES' or 'NO' on proposed protocol updates or changes using the VOTE smart contract function. The number of votes each user has is equal to the amount of veYBX they hold.

If the vote passes (60% of votes are YES at the end of the voting period), the proposal status data entry is changed to _approved_. If it does not pass, the proposal account is deleted. A proposal vote must reach a quorum of at least 5% of outstanding voting power to pass. The proposal has 5 days to reach quorum. If it does not reach it in that time period it is deleted. This quorum percentage can be adjusted through a governance proposal.

## Who can vote?

Anyone who [escrows YBX tokens](escrowing.md) can vote.

## How are governance proposals created?

Governance proposals are created using the [governance functions](../technical-docs/protocol/governance-contract.md) of the YieldBlox smart contract.

## Who can create a proposal?

Governance proposals can be created by any user account with more than 0.001% of the total voting power. This percentage can be adjusted through a governance proposal.

## What is the YieldBlox security council?

It takes 5 days at minimum to implement a standard governance proposal. This is slow by design to combat malicious proposals. However, this means that YieldBlox governance is unable to quickly respond to turret failures or uncovered smart contract vulnerabilities. Therefore, the YieldBlox governance system also includes a security council that can quickly submit Swap Signer or Freeze Contract proposals. Members of this council receive gYBX which can vote on these two unique proposal types in addition to normal governance proposals.

The YieldBlox security council should be elected every six months using a standard governance proposal, their membership can also be revoked at any point using a standard governance proposal.

## Governance Proposals

### Standard

Standard governance proposals are the basic proposals used to modify protocol parameters or functionality. Proposer's submit XDR's that carry out all proposed changes, if the proposal is accepted the XDRs are approved for submission. Any user with more than 0.001% of total outstanding voting power can submit a proposal, they must also deposit 1000 XLM into the account that stores the proposal to cover transaction fees. Once the proposal is submitted or rejected they will be able to delete the proposal account and reclaim the XLM.

Standard proposals follow the voting procedure described above.

### YBX Issuance Allocations

YBX issuance allocations are set by governance proposals. These proposals are initiated using a `incentiveAllocation` operation in the governance smart contract. These governance proposals differ from standard governance proposals in that instead of voting `YES` or `NO` they vote on allocating incentives for lending or borrowing a certain asset. For example, if a user wants more incentives to be allocated to XLM lenders, they will use their veYBX to submit `LENDING_XLM` votes. At the end of the voting period, the governance proposal shifts incentive allocation to match the distribution of votes. For example, say USDC and XLM are the only assets supported by the protocol and at the end of the voting period there are 600 votes for `LENDING_XLM` 400 votes for `BORROWING_XLM` 500 votes for `LENDING_USDC` and 500 votes for `BORROWING_USDC`. 30% of YBX incentives will be allocated to XLM lenders, 20% will be allocated to XLM borrowers, 25% will be allocated to USDC lenders, and 25% will be allocated USDC borrowers. This creates a strong incentive for users to vote for whatever assets they are currently lending or borrowing so make sure you vote on these proposals! Any user may submit an allocation proposal regardless of how much voting power they have.

Incentive allocation proposals differ in that the voting period for these proposals is 7 days to give every veYBX holder a chance to vote and there is no queue period. After voting ends the proposal is immediately implemented! Furthermore, only one of these proposals can exist at a time and a new one can be created as soon as the old one is concluded.

### Swap Signer

One risk of the [Stellar Turrets](https://tss.stellar.org) protocol is bad turrets popping up. One way YieldBlox mitigates against this risk is with swap signer proposals. In emergencies, this can be used to remove one turret's signing key and replace it with a different turret's key. These proposals can only be submitted and voted on by gYBX holders (members of the YieldBlox security council).

Unlike custom proposals, signer swap proposals do not have voting or queue periods. As soon as the proposal account reaches 70% of gYBX tokens voting YES, the proposal will be implemented. Signer swap proposals can only be submitted once per day to prevent abuse.

### Freeze Contract

Another main risk of the YieldBlox protocol is a bug in the YieldBlox smart contracts. While our team has thoroughly tested our smart contracts and is having them audited, it is still possible a bug slips through the cracks. To protect against this possibility, gYBX holders can create and vote on freeze contract proposals. This freezes a specified smart contract operations and prevents it from being ran. This contract gives users the ability to quickly freeze a smart contract if a bug is found in it to minimize damage.

Like signer swap proposals, this proposal does not have a voting or queue period. As soon as the proposal account reaches 70% of gYBX tokens voting YES, the proposal will be implemented. This operation can be reversed using either a governance function or a freeze protocol operation. To prevent a rouge security council from perpetually freezing the protocol, freeze contract proposals are unable to freeze governance smart contract functions.

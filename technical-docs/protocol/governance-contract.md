# Governance Contract

Governance Proposals are submitted and managed using the Governance Contracts. There are two governance contracts, the Proposal Create contract and the Proposal Update contract.

### Proposal Create

Handles governance proposal creation.

**Request**

```
{
    userPublicKey: string,
    timestamp: number,
    type: ProtocolEventTypes,
    fee: string,
    proposalAccountId: string,
    proposalType: ProposalType
    params: CouncilLockParams | CouncilSwapParams | undefined

}
```

&#x20;_**Fields:**_

- proposalAccountId: The public key of the account being created as the proposal account.
- proposalType: Represents the governance proposal type using the following enum

  ```
  ProposalType {
   ALLOCATION = 0,
   CUSTOM = 1,
   COUNCIL_SWAP_SIGNER = 2,
   COUNCIL_LOCK_CONTRACT = 3
  }
  ```

- params: undefined if the proposal is custom or an allocation proposal, otherwise related to council lock or swap proposals.

  ```
  CouncilLockParams: {
     lockedContracts: ProtocolEventTypes[]
     }
  ```

  - lockedContracts: array of enums that represent the different protocol event types (Mint, Burn, etc...)

  ```
  CouncilSwapParams: {
     addTurret: string;
     addSigner: string;
     removeSigner: string;
     }
  ```

  - addTurret: Public key of the turret sponsor account being added
  - addSigner: Public key of the turret signer account being added
  - removeSigner: Public key of the signer being removed

#### High-Level Contract Process Flow

This contract has been modified recently, an updated Contract Flow will be added shortly

### Proposal Update

Handles updating proposals by tallying their votes, submitting them, or deleting them.

**Request**

```
{
    userPublicKey: string,
    timestamp: number,
    fee: string,
    type: ProtocolEventTypes,
    proposalAccountId: string,
    proposalType: ProposalType
}
```

**Fields:**

- proposalAccountId: The public key of the account being created as the proposal account.
- proposalType: Represents the governance proposal type using the following enum

  ```
  ProposalType {
   ALLOCATION = 0,
   CUSTOM = 1,
   COUNCIL_SWAP_SIGNER = 2,
   COUNCIL_LOCK_CONTRACT = 3
  }
  ```

#### High-Level Contract Process Flow (MAY BE OUT OF DATE)

This contract has been modified recently, an updated Contract Flow will be added shortly

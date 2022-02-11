# Vote Contract

### Vote

Users vote on governance proposals through this contract.

**Request**

```
{
    userPublicKey: string,
    timestamp: number,
    type: ProtocolEventTypes,
    fee: string,
    proposalAccountId: string,
    votes: BalanceLine[],
    proposalType: ProposalType
}
```

_**Fields:**_

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

- votes: array of user votes represented by [BalanceLine](README.md#Balance-Line-Objects)'s
  - If user is voting on a non-allocation update the assetCode will be YES or NO
  - If user is voting on an allocation update the assetCode will be a liability token code, pool token code, or YBX
  - amount is the number of votes the user wishes to cast

### High-Level Contract Process Flow (MAY BE OUTDATED)

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. Contract checks that the user has sufficient voting power for the total amount of votes they entered by looking at their veYBX holdings. If they do not the proposal rejects.
5. Contract adds a `allowTrust` operation where the escrow account authorizes the user to hold vYBX.
6. Contract checks how much vYBX the user currently has.
   1. If the user does not have sufficient vYBX to cast their votes the contract adds a `payment` operation where the escrow account pays the necessary vYBX to the user.
   2. If the user has too much vYBX the contract adds a `payment` operation that pays the excess vYBX to the escrow account.
7. Contract adds `manageSellOffer` operations where the user offers to sell vYBX for their input vote assets. Vote assets are assets with the input asset code with the proposal account as the issuer.
8. Contract adds a `allowTrust` operation where the escrow account authorizes the user to maintain vYBX liabilities.
9. Turret builds, signs, and returns the XDR.

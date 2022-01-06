# Governance Contract

Governance Proposals are submitted and managed using the Governance Contract. Governance contract consists of the events PROPOSE, TALLY\_VOTES, IMPLEMENT . PROPOSE has the event subtypes of CUSTOM, REPLACE\_SIGNER, LOCK, ALLOCATION. This smart contract also handles voting, which allows users to vote on governance proposals.

#### Propose

**Request**

```
{    
    userPublicKey: string,
    timestamp: number,
    type: string,
    operation: string,
    proposalAccountKeypair: string,
    event: string

}
```

&#x20;_**Fields:**_

* Operation: 'PROPOSE'
* proposalAccountKeypair: The keypair of the proposal account that will be created
* Event can be either CUSTOM, REPLACE\_SIGNER, LOCK, or ALLOCATION.  They each have custom fields
* CUSTOM fields
  * `proposalXDR:`xdr of the custom proposal, this is the proposed transaction
* REPLACE\_SIGNER fields
  * addSigner: signer to be added to all protocol accounts
  * removeSigner: signer to be removed from all protocol accounts
* LOCK fields:
* tx\_function: target smart contract to lock/unlock (one of the event types listed above)
  * Note: TX\_GOVERNANCE cannot be locked
* lock: LOCKED or UNLOCKED
  * true to lock the contract. False to unlock it&#x20;
* ALLOCATION Fields
  * N/A - follows general constructor

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. Contract adds a `createAccount` operation where the pool creates the proposal account.
5. Contract adds a `setOptions` operations where the proposal account swaps its signers for the protocol's turret signer structure.
6. If the proposal is not an allocation proposal the contract checks that the user has sufficient voting power to create a proposal. If they do not the proposal rejects.
7. If the proposal is a custom proposal the contract fragments the XDR and adds `manageData` operations where the proposal account stores the fragmented XDR in its data entries.
8. If the proposal is a swapSigner proposal the contract adds `manageData` operations where the proposal account stores the signer being removed and the signer being added in its data entries.
9. If the proposal is a lock proposal the contract adds a `manageData` operation where the proposal adds the contract to be locked or unlocked to the proposal accounts data entries.
10. The contract adds a `manageData` operation where the proposal account adds a Proposal Status data entry with the value Voting.
11. Turret builds transaction builder into an XDR and returns it along with a signature.

#### Tally Votes

Handles the counting of votes after the 3 day voting period.

**Request**

```
{    
    userPublicKey: string,
    timestamp: number,
    type: string,
    operation: string,
    proposalAccount: string
}
```

_**Fields:**_

* proposalAccount: account ID of the proposal votes are being tallied for

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object
   1. This is the object operations will be added to throughout the rest of the contract process flow
4. In the case that the proposal is a custom proposal
   1. The contract checks that the proposal account has existed for three days. If it has not the contract rejects the request
   2. The contract pulls the orderbooks for vYBX and the assets with the codes YES and NO with the proposal account as the issuer
   3. The contract tallies yes and no votes by counting the size of the asks with price 1 in the orderbook for each asset
   4. Contract checks if the proposal has enough votes to reach quorum. If it does not the proposal rejects the request
   5. Contract checks if 60% of votes are yes. If not, the contract adds operations to delete the proposal account and returns the XDR
   6. Contract adds a `manageData` operation where the proposal account changes the proposal status data entry to Approved
5. In the case that the proposal is an allocation proposal
   1. The contract checks that the proposal account has existed for seven days. If it has not the contract rejects the request
   2. The contract pulls the orderbook for vYBX and all assets that have pool or liability token codes and the proposal account as the issuer
   3. The contract tallies all votes for each asset and adds `manageData` entries where the pool account updates underlyingAssetData entries to match the new proposals
   4. The contract adds operations that delete the proposalAccount
6. If the proposal is a different proposal type
   1. **TBD This process is changing**
7. The turret builds, signs, and returns the XDR

#### Implement

Handles the implementation of proposals that have reached quorum. This only applies to custom proposals as other proposal types are implemented in Tally Votes.

**Request**

```
{    
    userPublicKey: string,
    timestamp: number,
    type: string,
    operation: string,
    proposalAccount: string
}
```

_**Fields:**_

* proposalAccount: account ID of the proposal being implemented or deleted

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object
   1. This is the object operations will be added to throughout the rest of the contract process flow
4. Contract checks that it has been two days. If it has not been the contract rejects the request.
5. Contract decodes the proposed XDR and adds all proposed operations
6. Contract adds operations to delete the proposal account
7. Turret builds transaction builder into an XDR and returns it along with a signature.

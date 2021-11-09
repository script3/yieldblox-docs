# Vote Contract

### Vote

Users vote on governance proposals through this contract.&#x20;

**Request**

```
{    
    userPublicKey: (userPublicKey), 
    timestamp: (currentTimestamp), 
    type: (protocolEventType), 
    proposalAccount: (amount), 
    votes: [{ 
        assetCode: string,
        amount: string,
        }],
    allocationUpdate: boolean
}
```

_**Fields:**_

* proposalAccount: account ID of the proposal being voted on
* votes: array of user votes
  * If user is voting on a non-allocation update the assetCode will be YES or NO
  * If user is voting on an allocation update the assetCode will be a liability token code, pool token code, or YBX
  * amount is the number of votes the user wishes to cast
* allocation updates: true if the user is voting for an allocation update. False if they are not

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. Contract checks that the user has sufficient voting power for the total amount of votes they entered by looking at their sYBX holdings. If they do not the proposal rejects.
5. Contract adds a `allowTrust` operation where the staking pool authorizes the user to hold vYBX.
6. Contract checks how much vYBX the user currently has.
   1. If the user does not have sufficient vYBX to cast their votes the contract adds a `payment` operation where the staking pool pays the necessary vYBX to the user.
   2. If the user has too much vYBX the contract adds a `payment` operation that pays the excess vYBX to the staking pool.
7. Contract adds `manageSellOffer` operations where the user offers to sell vYBX for their input vote assets. Vote assets are assets with the input asset code with the proposal account as the issuer.&#x20;
8. Contract adds a `allowTrust` operation where the staking pool authorizes the user to maintain vYBX liabilities.
9. Turret builds, signs, and returns the XDR.







\





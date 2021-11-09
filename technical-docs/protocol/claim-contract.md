# Claim Contract

Users will claim their governance rewards using this contract. Any time a claimable balance is touched, Claim will be invoked in order to keep proper track of issuance. This contract also handles updating YBX issuance amounts for each daily period. Any other contracts that manipulate claimable balances will have the Claim contract invoked to keep proper track of issued pool incentives.

**Request**

```
{    
    userPublicKey: string,
    timestamp: number,
    type: string,
    operation: string,
}
```

\
_**Fields:**_

* operation: Update or Claim, update sends issuance tracker payments for a period. Claim claims YBX for users.

#### Calculations:

* _Issuance Amount_
  * the amount of YBX to issue per asset
* _Claim Amount_
  * the amount of YBX the user can claim over the unclaimed periods

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. If the contract is performing a UPDATE operation.
   1. Contract checks if UPDATE has been ran today. If it has been it rejects the request.
   2. Contract calculates the YBX issuance ratio for each asset. See YBX Issuance section.
   3. Contract send YBX issuance ratio payments to all YBX issuance trackers.
   4. Contract adds a `payment` operation where the issuance account pays all YBX to be distributed this period to the distribution account.
   5. Contract adds a `payment` operation where the distribution account pays all YBX allocated to YBX stakers to the staking pool.
5. If the contract is performing a CLAIM operation.
   1. Contract identifies all user positions that have unclaimed YBX issuance accrued to them.&#x20;
   2. Contract creates `claimClaimableBalance` operations where the pool claims all user positions that have YBX to claim.&#x20;
      1. Contract calculates the YBX to be issued for each of these positions.
         1. See YBX Issuance section.
      2. Contract calculates accrued interest for all liability positions.
   3. Contract adds `createClaimableBalance` operations where the pool recreates all user positions.
      1. The user sponsors these claimable balances.
   4. Contract adds a `payment` operation where the distribution account pays all earned YBX to the user.
   5. Contract adds Utilization Tracker operations. See Average Utilization Ratios section.
6. Turret builds transaction builder into an XDR and returns it along with a signature.

###

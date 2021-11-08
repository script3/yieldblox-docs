# Rate Contract

Loan rate rebalancing and rate swaps are done through the Rate contract. Users lending will use this contract to ensure that they get the correct interest accrued on the funds being lent out. Rebalancing can only occur when the stable interest rate is below the current floating rate. Users who are borrowing will use this contract to swap from stable or floating rates on their loans.

**Request**

```
{    
    userPublicKey: string,
    timestamp: number,
    type: string,
    claimableBalanceId: string,
    targetRate: string,
}
```

\
_**Fields:**_

* Claimable Balance Id: ID of the claimable balance representing the loan that needs to have its interest rate swapped.
* Target Rate: Target interest rate for the loan (fixed or floating)

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. If the user is not the owner of the liability balance the contract verifies that the balance is fixed rate and that its interest rate is lower than the current floating interest rate. If either of these things are not the case the contract rejects.
5. Contract adds a `claimClaimableBalance` operation where the pool claims the specified liabiliity balance.
   1. The contract calculates accrued interest and adds it to the liability balance.
   2. The contact calculates all unclaimed YBX issuance associated with this liability balance.
6. Contract adds a `createClaimableBalace` operation where the pool creates a liability balance with the target interest rate.
   1. If the user is the owner they sponsor the liability balance. If they are not the owner the staking pool sponsors the liability balance.
      1. The rebalancer must pay the staking pool the necessary minimum reserve for sponsoring the liability balance.
7. Contract creates a `payment` operation where the distribution account pays any unclaimed YBX to the user.
8. Contract adds all necessary Utilization Tracker operations.
9. Turret builds transaction builder into an XDR and returns it along with a signature.

### Diagram

![](<../../.gitbook/assets/image (19).png>)

**User Account:  **The** **pool claims the liability claimable balance and recreates it with a floating interest rate.

# Mint Contract

Lending, collateralizations, and borrowing take place through the Mint contract. Users can deposit assets and collateralize them in the same transaction.

**Request**

```
{
    userPublicKey: string,
    timestamp: number,
    type: string,
    deposit?: {
        asset: string,
        amount: string
        },
    borrow?: {
        asset: string,
        amount: string
        },
    collateralization?: [{
        asset: string,
        amount: string
        }]
}
```

**Fields:**

* Deposit (Optional): The asset and amount of the asset the user would like to deposit into the lending pool.
* Borrow (Optional): The asset and the amount of the asset the user would like to borrow.
  * Note: If the user attempts to borrow an amount that would put their health factor below 1.1, their request is rejected.
* Collateralizations (Optional): The pool tokens and the amount of the pool tokens the user would like to collateralize

#### Calculations:

* Pool Token Issuance - _depositing_
  * the amount of pool tokens to issue for a deposit for the current price of the pool token
* Account Health Factor - _borrowing_
  * check that the assumed health factor post borrow is valid and above 1.1

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. If the user is depositing the contract handles deposits.
   1. The contract adds a `payment` operation to the transaction builder where the user pays the pool their deposit and a `payment` operation where the pool pays the user pool tokens.
      1. If the user is missing a poolToken trustline the contract first adds a `changeTrust` operation where the user creates one.
5. If the user is collateralizing the contract handles collateralizations&#x20;
   1. Contract checks if the user currently has collateral balances of the assets they are attempting to collateralize. If they do the contract adds `claimClaimableBalance` operations where the pool claims the balances so they can be consolidated with the new collateralizations.
      1. The contract will also calculate any unclaimed YBX the user has accrued to these positions.
   2. Contract adds `createClaimableBalance` operations where the user creates collateral deposit claimable balances.
6. If the user is borrowing the contract handles the borrow.
   1. Contract adds a `payment` operation where the pool pays the user the borrowed asset.
   2. If the user already has a liability balance associated with the asset the user is borrowing the contract adds a `claimClaimableBalance` operation where the pool claims the liability balance so it can be consolidated with the additional borrowed assets.
      1. The contract will also record all interest accrued by this liability balance and add it to the user's total liability for the asset.
      2. The contract will also calculate any unclaimed YBX the user has accrued to this position.
   3. Contract adds a `createClaimableBalance` operation where the pool creates liability claimable balance to record the users total liabilty for the borrowed asset.
      1. The user sponsors this claimable balance.
7. Contract checks the users new health factor. If it is below 1.1 the contract throws a rejection.
8. If the user has any unclaimed YBX associated with the refreshed balances the contract adds a `payment` operation where the distribution account sends the total unclaimed YBX to the user.
9. The contract performs all necessary utilization delta payments and corrections. See Average Utilization Ratios section.
10. Turret builds transaction builder into an XDR and returns it along with a signature.

### Diagram

![Diagram may be out of date](<../../.gitbook/assets/image (28).png>)

**Lender A:** Lends 50,000 XLM to the pool and receives 50,000 y00XLM in exchange. Lender A can burn these tokens later when the pool has accumulated fees and receive their proportion of the pool back.

**Borrower B:** Deposits 30,000 XLM to the pool and collateralizes the received pool tokens to take out a 10,800 USDC loan. Also, deposits pool tokens from a previous uncollateralized deposit as collateral for a 1,800 XLM loan.

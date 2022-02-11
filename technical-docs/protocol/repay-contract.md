# Repay Contract

User repayments are handled using the Repay contract. Users also can repay a loan using collateral instead of the borrowed asset. The user's health factor must have been improved by the request or it will be rejected.

**Request**

```
{
   userPublicKey: string,
   timestamp: number,
   type: string,
   repayments: BalanceLine,
   targetPool: string,
   collateralRepayments?: RepayPath[]
}
```

\
**Fields:**

- repayments:[BalanceLine](README.md#Balance-Line-Objects) that represents the assets and amounts being repaid. [assetId](README.md#AssetId-entries)'s are expected to be liability tokens.
- targetPool: Id of the pool associated with the assets being repaid.
- collateralRepayments (OPTIONAL): Array of [RepayPath](README.md#Repay-Path-Objects)'s describing how to structure the pathPayments that will be used to liquidate collateral withdrawn. These are only input if the user is partially or fully repaying with collateral.

### High-Level Contract Process Flow (MAY BE OUT OF DATE)

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. If user is withdrawing the contract handle withdrawals.
   1. Contract adds `claimClaimableBalance` operations where the pool claims the withdrawn collateral balances.
      1. Contract calculates all unclaimed YBX issuance associated with these collateral balances.
   2. If the user is not fully withdrawing the contract adds a `createClaimableBalance` operation where the user recreates the collateral position with the remaining collateral.
   3. If the user is not repaying with collateral the contract adds `payment` operations where the pool pays all withdrawn pool tokens to the user.
   4. If the user is repaying with collateral the contract burns all withdrawn pool tokens.
      1. It first calculates the pool tokens' value including the withdrawal fee .
         1. Contract adds `payment` operations which pathPayments the withdrawal fees from the pool to the escrow account (the destination asset is YBX).
      2. Contract adds `payment` operations which send the value of the pool token from the pool to the user.
5. If the user is repaying the contract handles repayments.
   1. Contract adds `payment` operations where the user pays the repayment to the pool.
      1. If the user is repaying with collateral the contract instead adds `pathPaymentStrictReceives` that pay the withdrawn assets to the pool (destination asset is the asset being repaid).
   2. Contract adds a `claimClaimableBalance` operation where the pool claims the associated liability balance.
      1. Contract accrues interest to the relevant liability balance.
      2. Contract also calculates all unclaimed YBX issuance associated with these collateral balances.
      3. If the liability was not fully repaid the contract adds a `createClaimableBalance` operation where the pool creates a liabilty claimable balance representing the remaining asset liability.&#x20;
         1. The user sponsors this claimable balance.
      4. Contract calculates the YBX repurchases associated with the interest paid in the repayments and adds `pathPaymentStrictSend` operations that have the user purchase and send YBX to the escrow account with a portion of their interest payment.
6. Contract checks user health factor after withdrawals and repayments. If it has decreased and is below 1.1 the contract rejects.
7. Contract adds a `payment` option where the distribution account pays any unclaimed YBX from the previous calculations to the user.
8. Contract adds all necessary Utilization Tracker operations. See Average Utiization Ratios section.
9. Turret builds transaction builder into an XDR and returns it along with a signature.

### Diagram

![](<../../.gitbook/assets/image (23).png>)

#### In the base repayment scenario (no repay with collateral)

**User Account:** pays the pool 100 USDC and withdraws 345 yXLM from their collateral claimable balance (the pool claims it and pays it to the user). The pool deletes the user's liability claimable balance to reflect the repayment.

#### In the repay with collateral liquidation scenario <a href="#in-the-repay-with-collateral-liquidation-scenario-1" id="in-the-repay-with-collateral-liquidation-scenario-1"></a>

**User Account:** withdraws 345 yXLM from their collateral claimable balance (the pool claims it and pays it to the user); this is then converted to XLM and sold for 102 USDC, which is paid to the pool. The pool deletes a portion of the liquidated user's liability claimable balance to reflect the repayment. The liquidated user's new liability balance will be 263.58 USDC, and their new collateral balance will be 901.635 y00XLM.

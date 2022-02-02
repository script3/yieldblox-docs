# Liquidate Contract

Users use the liquidate contract to liquidate underwater accounts where the health factor has dropped below 1. Users will be able to liquidate loans by selling the liquidated users collateral or by repaying the borrowed asset normally.&#x20;

**Request**

```
{
    userPublicKey: (userPublicKey), //string
    timestamp: (currentTimestamp), //number
    type: (protocolEventType) //string
    liquidateeId: (Liquidatee public key), //string
    repayments: [{
        asset: (assetCode):(assetIssuer), //string
        amount: (amount), //string
        interestType: (interestType) //string
        }],
    withdrawals?: [{
        asset: (poolTokenCode):(poolTokenIssuer), //string
        percent: (withdrawalPercent) //string
    }],
    repayWithCollateral: (boolean), //string
    acceptableSlippage?: (acceptable slippage percentage) //number
}
```

\
**Fields:**

- liquidatee Id: public key of the account being liquidated
- repayments: assets and amounts being repaid as well as the interest type('FIXED' or 'VARIABLE') of the loan being repaid
- withdrawals (Optional): pool tokens and percentage of total repaid value to withdraw as the specified asset
  - &#x20;Example: If, in total, the user repaid $1000 and they input XLM with 50%, we will attempt to withdraw $500 worth of XLM.
  - Note: If a user's collateral deposit is not sufficient to withdraw the input percentage, we will withdraw the maximum amount of that asset then withdraw the rest in other collateral deposits.
  - Note: If withdrawals are not input, the smart contract will proportionally withdraw from all collateral assets the user holds.
- repay with collateral: true if the user decides to repay with collateral
  - This means they will burn the withdrawn pool tokens and use a pathPayment to repay the borrow
- acceptable slippage (Optional): acceptable slippage for the path payments used when repaying with collateral

#### Calculations:

- _Max Liquidation_
  - the max amount the liquidator can liquidate till the delinquent account's health factor reaches 1.02

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. Contract populates all withdrawals and repayments for the liquidation based on the maxLiquidation calculations and the users repayment and withdrawal inputs. It also calculates whether or not a backstop repayment is necessary.
5. Contract handle withdrawals.
   1. Contract adds `claimClaimableBalance` operations where the pool claims the withdrawn collateral balances.
      1. Contract also calculates all unclaimed YBX issuance associated with these collateral balances.
   2. If the user is not fully withdrawing the contract adds a `createClaimableBalance` operation where the user recreates the collateral position with the remaining collateral.
      1. Escrow account sponsors these. The contract also adds `payment` operations where the user pays XLM to the escrow account so they have the funds to sponsor the claimable balances.
   3. If the user is not repaying with collateral the contract adds `payment` operations where the pool pays all withdrawn pool tokens to the user.
   4. If the user is repaying with collateral the contract burns all withdrawn pool tokens.
      1. It first calculates the pool tokens' value including the withdrawal fee.
         1. Contract adds `pathPayment` operations where the pool uses the withdrawal fees to repurchase YBX and sends it to the escrow account.
      2. Contract adds `payment` operations where the pool sends the value of the pool token from the pool to the user.
6. The contract handles repayments.
   1. Contract adds `payment` operations where the user pays the repayment to the pool.
      1. If the user is repaying with collateral the contract instead adds `pathPaymentStrictReceives` where the user uses the withdrawn assets to repurchase the repayment asset and sends it to the pool.
   2. Contract adds a `claimClaimableBalance` operation where the pool claims the associated liability balance.
      1. Contract adds accrued interest to the relevant liability balance.
      2. Contract also calculates all unclaimed YBX issuance associated with these collateral balances.
      3. If the liability was not fully repaid the contract adds a `createClaimableBalance` operation where the pool creates a liabilty claimable balance representing the remaining asset liability.
         1. Escrow account sponsors these. The contract also adds `payment` operations where the user pays XLM to the escrow account so they have the funds to sponsor the claimable balances.
      4. Contract calculates the YBX repurchases associated with the interest paid in the repayments and adds `pathPaymentStrictSend` operations that have the user purchase and send YBX to the escrow account with a portion of their interest payment.
7. If backstop repayments are necessary contract creates `pathPaymentStrictReceive` operations where the escrow account and issuing account sell YBX for the repayment asset and send it to the pool account.
8. Contract adds a `payment` option where the distribution account pays any unclaimed YBX from the previous calculations to the liquidated user.
9. Contract adds all necessary Utilization Tracker operations. See Average Utiization Ratios section.
10. Turret builds transaction builder into an XDR and returns it along with a signature.

### Diagram

![](<../../.gitbook/assets/image (17).png>)

#### In the base liquidation scenario (no repay with collateral)

**Liquidator Account:** pays the pool 236.42 USDC and withdraws 716.015 yXLM from the liquidatee's collateral claimable balance (the pool claims it and pays it to the user, then remakes the claimable balance). The pool deletes a portion of the liquidated user's liability claimable balance to reflect the repayment. The liquidated user's new liability balance will be 263.58 USDC, and their new collateral balance will be 901.635 y00XLM.

#### In the repay with collateral liquidation scenario

**Liquidator Account:** withdraws 716.015 yXLM from the liquidatee's collateral claimable balance (the pool claims it and pays it to the user, then remakes the claimable balance). This is then converted to XLM and sold for 236.42 USDC, which is paid to the pool. The pool deletes a portion of the liquidated user's liability claimable balance to reflect the repayment. The liquidated user's new liability balance will be 263.58 USDC, and their new collateral balance will be 901.635 y00XLM.

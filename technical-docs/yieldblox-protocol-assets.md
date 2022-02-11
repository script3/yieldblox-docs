# YieldBlox Protocol Assets

Yieldblox uses a variety of custom protocol assets to track protocol information. These assets are all issued by the YieldBlox pool account and represent specific underlying assets. They are all clawback enabled so the pool can manipulate claimable balances containing them. The tokens follow the following naming convention

`{Token Key}{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}`

Where:

- Token Key: Character that identifies protocol asset
  - y = Pool Token
  - l = Liability Token
  - i = Accrued Interest Tracker Token
  - a = Pool Issuance Ratio Tracker Token
  - b = Pool Issuance Shift Tracker Token
  - c = Liability Issuance Ratio Tracker Token
  - d = Liability Issuance Shift Tracker Token
- Underlying Asset Issuer Key: base 64 character that identifies the issuer of the underlying asset associated with the protocol token. It corresponds to a pool data entry that holds the issuer account id.
- Underlying Asset Overlap Key: base 64 character that identifies the last 3 characters in an asset code. It corresponds to a pool data entry that holds the last 3 characters of the asset code

### Pool Tokens

Pool tokens are used to track user deposits in the YieldBlox Protocol. They represent proportional ownership of a YieldBlox lending pool. Their value is calculated using the Pool Token Value equation ([see math section](math.md#pool-token-value)). Users receive them when they deposit assets into a lending pool and burn them when they withdraw assets from a lending pool.

Sample Asset Code for an XLM pool token: `y00XLM`

---

### **Liability Tokens**

Liability Tokens are used to track user borrowing liabilities. One Liability Token corresponds to one of the underlying asset. When a user borrows from the pool, the protocol creates a claimable balance of liability tokens that tracks the loan. As interest accrues, more liability tokens are added to the claimable balance. When the loan is repaid, the claimable balance is deleted.

Sample Asset Code for an XLM liability token: `l00XLM`&#x20;

### Accrued Interest Tracker Tokens

Accrued interest tracker tokens are used to track the interest accrued to outstanding underlying asset liabilities over time. This is done by paying them to accrued interest tracker accounts in the process outlined in the [Accrued Interest Tracking section](accrued-interest-tracking.md).

Sample Asset Code for an XLM utilization tracker token: `i00XLM`&#x20;

#### Pool Issuance Ratio Tracker Tokens

Pool Issuance Ratio Tokens track YBX Incentive payouts for collateralized pool tokens by trading the mantissa amount of the [issuance ratio](math.md#Issuance-Ratio) for a given pool token for a given period for an amount of Pool Issuance Shift Tracker Tokens equal to the exponential associated with that mantissa. So if there are 100 pool tokens collateralized and 50 YBX tokens are being issued, the issuance ratio will be 0.5 and the amount of Pool Issuance Ration Tokens sold will be 5.

Sample Asset Code for an XLM pool issuance ratio token: `a00XLM`&#x20;

#### Pool Issuance Shift Tracker Tokens

Pool Issuance Ratio Tokens track YBX Incentive payouts for collateralized pool tokens by trading the exponential associated with the mantissa of the [issuance ratio](math.md#Issuance-Ratio) for a given pool token for a given period for an amount of Pool Issuance Ratio Tracker Tokens equal to the mantissa. To avoid negative numbers the exponential is added to 15. So if there are 100 pool tokens collateralized and 50 YBX tokens are being issued, the issuance ratio will be 0.5 and the amount of Pool Issuance Shift Tokens sold will be 16.

Sample Asset Code for an XLM pool issuance ratio token: `b00XLM`&#x20;

#### Liability Issuance Ratio Tracker Tokens

Liability Issuance Ratio Tokens track YBX Incentive payouts for liability tokens by trading the mantissa amount of the [issuance ratio](math.md#Issuance-Ratio) for a given liability token for a given period for an amount of Liability Issuance Shift Tracker Tokens equal to the exponential associated with that mantissa. So if there are 100 liability tokens and 50 YBX tokens are being issued, the issuance ratio will be 0.5 and the amount of Liability Issuance Ration Tokens sold will be 5.

Sample Asset Code for an XLM liability issuance ratio token: `c00XLM`&#x20;

#### Liability Issuance Shift Tracker Tokens

Liability Issuance Ratio Tokens track YBX Incentive payouts for liability tokens by trading the exponential associated with the mantissa of the [issuance ratio](math.md#Issuance-Ratio) for a given liability token for a given period for an amount of Liability Issuance Ratio Tracker Tokens equal to the mantissa. To avoid negative numbers the exponential is added to 15. So if there 100 liability tokens and 50 YBX tokens are being issued, the issuance ratio will be 0.5 and the amount of Liability Issuance Shift Tokens sold will be 16.

Sample Asset Code for an XLM pool issuance ratio token: `d00XLM`&#x20;

### vYBX

vYBX is issued to veYBX escrows to allow them to vote on governance proposals. Their maximum vYBX allowance is the amount of veYBX they hold. veYBX is non-transferable by the user.

### gYBX

gYBX is issued to the initial contributors of the YieldBlox Protocol instead of veYBX. gYBX has voting power but, it does not receive YBX issuance to escrows like veYBX does.

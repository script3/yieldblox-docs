# YieldBlox Protocol Assets

Yieldblox uses a variety of custom protocol assets to track protocol information. These assets are all issued by the YieldBlox pool account and represent specific underlying assets. The tokens follow the following naming convention

`{Token Key}{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}`

Where:

* Token Key: Character that identifies protocol asset
  * y = Pool Token
  * l = Liability Token
  * i = Accrued Interest Tracker Token
  * a = Pool Issuance Ratio Tracker Token
  * b = Liability Issuance Ratio Tracker Token
* Underlying Asset Issuer Key: base 64 character that identifies the issuer of the underlying asset associated with the protocol token. It corresponds to a pool data entry that holds the issuer account id.
* Underlying Asset Overlap Key: base 64 character that identifies the last 3 characters in an asset code. It corresponds to a pool data entry that holds the last 3 characters of the asset code

#### Pool Tokens

Pool tokens are used to track user deposits in the YieldBlox Protocol. They represent proportional ownership of a YieldBlox lending pool. Their value is calculated using the Pool Token Value equation ([see math section](math.md#pool-token-value)). Users receive them when they deposit assets into a lending pool and burn them when they withdraw assets from a lending pool.

Sample Asset Code for an XLM pool token: `y00XLM`&#x20;

**Liability Tokens**

Liability Tokens are used to track user borrowing liabilities. One Liability Token corresponds to one of the underlying asset. When a user borrows from the pool, the protocol creates a claimable balance of liability tokens that tracks the loan. As interest accrues, more liability tokens are added to the claimable balance. When the loan is repaid, the claimable balance is deleted.

Sample Asset Code for an XLM liability token: `l00XLM`&#x20;

#### Accrued Interest Tracker Tokens

Accrued interest tracker tokens are used to track the interest accrued to outstanding underlying asset liabilities over time. This is done by paying them to accrued interest tracker accounts in the process outlined in the [Accrued Interest Tracking section](accrued-interest-tracking.md).

Sample Asset Code for an XLM utilization tracker token: `i00XLM`&#x20;

#### Pool Issuance Ratio Tokens

Pool Issuance Ratio Tokens track YBX Incentive payouts for collateralized pool tokens by being sent in payments that track the Issuance Ratio for a given pool token for a given period (Number of YBX Tokens Issued/Collateralized Pool Token). So if there are 100 pool tokens collateralized and 50 YBX tokens are being issued, the issuance ratio will be 0.5 and the amount of Pool Issuance Ration Tokens sent will be 0.5.

Sample Asset Code for an XLM pool issuance ratio token: `a00XLM`&#x20;

#### Liability Issuance Ratio Tokens

Liability Issuance Ratio Tokens track YBX Incentive payouts for liability tokens by by being sent in payments that track the Issuance Ratio (Number of YBX Tokens Issued/Liability Token). So if there are 100 liability tokens outstanding and 50 YBX tokens being paid out, the amount of Liability Issuance Ratio Tokens sent will be 0.5.&#x20;

Sample Asset Code for an XLM liability issuance ratio token: `b00XLM`&#x20;

#### vYBX

vYBX is issued to veYBX escrows to allow them to vote on governance proposals. Their maximum vYBX allowance is the amount of veYBX they hold. veYBX is non-transferable by the user.

#### gYBX

gYBX is issued to the initial contributors of the YieldBlox Protocol instead of veYBX. gYBX has voting power but, it does not receive YBX issuance to escrows like veYBX does.

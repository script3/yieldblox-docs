# Underlying Asset Data

Each underlying asset supported by YieldBlox has a set of protocol-specific data stored in the pool accounts data entries. &#x20;

## Data Entries:

### Interest Accrual Tracker Account

Address of the account that tracks interest accrual for the underlying account.

**Date Entry Key:** `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Tracker`

**Data Entry Value:** `{Interest Accrual Tracker Account Public Key}`

### Interest Data

Variables used in asset [interest rate equations](#math.md#Interest-Rate-Calculations).

**Date Entry Key:** `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Interest`&#x20;

**Data Entry Value:** `{Base Interest Rate}_{Interest Rate Slope 0}_{Interest Rate Slope 1}_{Interest Rate Slope 2}_{Interest Rate Slope 3}_{Interest Rate Threshold 1}_{Interest Rate Threshold 2}_{Interest Rate Threshold 3}`

**Where:**

- Base Interest Rate: Base interest rate constant in the interest rate equation (see math). Multiplied by 100 before being encoded.
- Interest Rate Slope 0: Interest rate slope when below the first interest rate threshold. Multiplied by 10 before being encoded.
- Interest Rate Slope 1: Interest rate slope when above the first interest rate threshold. Multiplied by 10 before being encoded.
- Interest Rate Slope 2: Interest rate slope when above the second interest rate threshold. Multiplied by 10 before being encoded.
- Interest Rate Slope 3: Interest rate slope when above the third interest rate threshold. Multiplied by 10 before being encoded.
- Interest Rate Threshold 1: If the utilization rate is above this threshold Interest Rate Slope 1 kicks in. Multiplied by 100 before being encoded.
- Interest Rate Threshold 2: If the utilization rate is above this threshold Interest Rate Slope 2 kicks in. Multiplied by 100 before being encoded.
- Interest Rate Threshold 3: If the utilization rate is above this threshold Interest Rate Slope 3 kicks in. Multiplied by 100 before being encoded.

### Asset Loan-to-Value Ratio

Loan to value ratio for the underlying asset, used to calculate (health factors)[../user-docs/lending-borrowing/health-factors.md].

**Date Entry Key:** `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_LTV`

**Data Entry Value:** `{Underlying Asset Loan-to-Value Ratio}`

**Where:**

- Loan to Value: Used in the health factor equation, loan to value ratio for the underlying asset. Multiplied by 100 before being encoded.

### Fee Data

Data pertaining to fees related to the underlying asset.

**Date Entry Key:** `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Fee`

**Data Entry Value:** `{Liquidation Incentive}_{Liquidation Fee}_{YBX Fee Allocation}_{Withdrawal Fee}`

**Where:**

- Liquidation Incentive: Used in liquidations. This is the 'discount' the liquidator receives on the collateral they withdraw when they repay a loan. Multiplied by 100 before being encoded.
- Liquidation Fee: Used in liquidations. This is the portion of the liquidation incentive that is paid to the escrow pool. Multiplied by 100 before being encoded.
- YBX Fee Allocation: Percent of interest rate fees that are used to repurchase YBX. Multiplied by 100 before being encoded.
- Withdrawal Fee: Fee for withdrawing from the protocol. Multiplied by 100 before being encoded.

### Allocation Data

Data pertaining to the ybx issuance allocation for assets

**Date Entry Key:** `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Allocation`

**Data Entry Value:** `{Collateral Incentive Allocation}_{Liability Incentive Allocation}`

**Where:**

- Collateral Incentive Allocation: Percent of YBX incentive issuance that is allocated to users who collateralize this asset. Multiplied by 100 before being encoded.
- Liability Incentive Allocation: Percent of YBX incentive issuance that is allocated to users who borrow this asset. Multiplied by 100 before being encoded.

### Price Feed Data

Data pertaining to the price feeds used to track the price of underlying assets

**Date Entry Key:** `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Exchange`

**Data Entry Value:** `{Exchange Primary}_{Binance}_{Coinbase}_{FTX}_{Asset Ticker}`

**Where:**

- Exchange Primary: Denotes whether the preferred price for the asset is centralized exchange prices or the Stellar DEX. 1 for exchange primary, 0 for DEX primary.
- Binance: Denotes whether Binance is used as an oracle price source for this asset. 1 for yes 0 for no.
- Coinbase: Denotes whether Coinbase is used as an oracle price source for this asset. 1 for yes 0 for no.
- FTX: Denotes whether FTX is used as an oracle price source for this asset. 1 for yes 0 for no.
- Underlying asset ticker: The ticker used in price feed API calls.

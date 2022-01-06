# Underlying Asset Data

Each underlying asset supported by YieldBlox has protocol-specific data stored in the pool accounts data entries.&#x20;

Data entry key: `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Data`&#x20;

Data entry value: `{Base Interest Rate}_{Interest Rate Slope 0}_{Interest Rate Slope 1}_{Interest Rate Slope 2}_{Interest Rate Slope 3}_{Interest Rate Threshold 1}_{Interest Rate Threshold 2}_{Interest Rate Threshold 3}_{Loan to Value}_{Liquidation Incentive}_{Liquidation Fee}_{Collateral Incentive Allocation}_{Borrowing Incentive Allocation}_{YBX Fee Allocation}_{Price Feed}_{Underlying Asset Ticker}`

where:

* Base Interest Rate: Base interest rate constant in the interest rate equation (see math). Multiplied by 100 before being encoded.
* Interest Rate Slope 0: Interest rate slope when below the first interest rate threshold. Multiplied by 10 before being encoded.
* Interest Rate Slope 1: Interest rate slope when above the first interest rate threshold. Multiplied by 10 before being encoded.
* Interest Rate Slope 2: Interest rate slope when above the second interest rate threshold. Multiplied by 10 before being encoded.
* Interest Rate Slope 3: Interest rate slope when above the third interest rate threshold. Multiplied by 10 before being encoded.
* Interest Rate Threshold 1: If the utilization rate is above this threshold Interest Rate Slope 1 kicks in. Multiplied by 100 before being encoded.
* Interest Rate Threshold 2: If the utilization rate is above this threshold Interest Rate Slope 2 kicks in. Multiplied by 100 before being encoded.
* Interest Rate Threshold 3: If the utilization rate is above this threshold Interest Rate Slope 3 kicks in. Multiplied by 100 before being encoded.
* Loan to Value: Used in the health factor equation, loan to value ratio for the underlying asset. Multiplied by 100 before being encoded.
* Liquidation Incentive: Used in liquidations. This is the 'discount' the liquidator receives on the collateral they withdraw when they repay a loan. Multiplied by 100 before being encoded.
* Liquidation Fee: Used in liquidations. This is the portion of the liquidation incentive that is paid to the escrow pool. Multiplied by 100 before being encoded.
* Collateral Incentive Allocation: Percent of YBX incentive issuance that is allocated to users who collateralize this asset. Multiplied by 100 before being encoded.
* Liability Incentive Allocation: Percent of YBX incentive issuance that is allocated to users who borrow this asset. Multiplied by 100 before being encoded.
* YBX fee allocation: Percent of interest rate fees that are used to repurchase YBX. Multiplied by 100 before being encoded.
* Price Feed: Price feed this underlying asset uses. Possible price feeds are DEX+Coinbase, DEX+Binance, DEX+FTX, DEX+Coinbase+Binance, DEX+Coinbase+FTX, and DEX+Binance+FTX. Encoded as an enum.
* Underlying asset ticker: The ticker used in these price feeds.


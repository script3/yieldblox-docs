# Protocol Accounts

YieldBlox uses a variety of protocol accounts to accomplish its functions.

### Pool Account&#x20;

Public Key: `GCPFDAQGO3QZ6PUCXCPDHV4UEKJVLPKJEYY4BQHZBEJGHDVU6FPIF2VR`

The YieldBlox lending pool holds assets lent using the YieldBlox protocol. It also issues pool and liability tokens and controls collateral and loan claimable balances. Finally, it stores most protocol parameters in its data entries. The smart contracts fetch this informatio from the pool data entries when they require it.

#### Data Entries

Data entry format

* Data Entry Key:Data Entry Value

Data entries for each asset supported by the protocol

* `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Data:{Base Interest Rate}_{Interest Rate Slope 0}_{Interest Rate Slope 1}_{Interest Rate Slope 2}_{Interest Rate Slope 3}_{Interest Rate Threshold 1}_{Interest Rate Threshold 2}_{Interest Rate Threshold 3}_{Loan to Value}_{Liquidation Incentive}_{Liquidation Fee}_{Collateral Incentive Allocation}_{Borrowing Incentive Allocation}_{YBX Fee Allocation}_{Price Feed}_{Underlying Asset Ticker}`
  * See the Underlying Asset Data section for a detailed explanation
* `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Underlying:{Issuer Account Public Key}_{Last 3 characters of underlying asset}`
  * Stores the underlying asset issuer and remaining characters from the underlying asset code so that the protocol can reconstruct the associated underlying asset from a protocol asset.
* `{Underlying Asset Code}_{Underlying Asset Issuer Key}_Utilization_Tracker:{Utilization Tracker Account Public Key}`
  * Public key of the utilization tracker for the underlying asset

For each turret that is a signer on protocol accounts

* `T_{Turret Signer Account}:{Turret URL}`
  * Tracks the url of the signing turret

Other data entries

* `Locked_Contracts:{Locked Contract}_{Locked Contract}_`
  * List of all contracts currently locked by the governance smart contract
* `Dev_Key_Id_1:{Dev wallet 1 public key}`
  * Dev wallet public key 1, will be added as a signer on a developer fund if one is approved in the future.
* `Dev_Key_Id_2:{Dev wallet 2 public key}`
  * Dev wallet public key 2, will be added as a signer on a developer fund if one is approved in the future.
* `Dev_Key_Id_3:{Dev wallet 3 public key}`
  * Dev wallet public key 3, will be added as a signer on a developer fund if one is approved in the future.
* `Governance_Proposal_Creation_Threshold:{Threshold}`
  * Threshold of voting power needed to create a governance proposal
* `Governance_Proposal_Quorum_Threshold:{Threshold}`
  * Governance proposal voting quorum needed to pass a governance proposal
* `Genesis YBX Outstanding:{gYBX outstanding}`
  * The founding team was issued gYBX on their stakes rather than veYBX. This does not come with escrow rewards but does have voting power
* `Genisis YBX Expiration:{expiration timestamp}`
  * The founding team's gYBX expires after one year. The protocol checks this timestamp because after that year it will no longer take gYBX into account when calculating outstanding voting power or user voting power.
* `YBX_Issuance_Rate:{daily issuance rate}`
  * The amount of remaining YBX to issue that is issued every day
* `Withdrawal_Fee:{withdrawal fee}`
  * The withdrawal fee the protocol takes when users withdraw their assets
* `YieldBlox Contract Hash:{Contract Hash}`
  * The hash of the YieldBlox Contract uploaded to its signing turrets. Allows users to verify that the contract is the expected one
* `YBX_Total_Supply:{total ybx supply}`
  * The total supply of YBX (currently 1.5 billion)

### Issuing Account:&#x20;

Public Key: `GBUYYBXWCLT2MOSSHRFCKMEDFOVSCAXNIEW424GLN666OEXHAAWBDYMX`

The YBX Issuing account is controlled by the YieldBlox smart contracts. It issues YBX during YBX issuance and default protection events (if necessary)

### Distribution Account:&#x20;

Publick Key:`GCZIXLOVS6CCBSIORWL5Y3HYZJRUQ65UEHF3SNIZZH6OPN54YXH4AJGX`

The YBX distribution account receives issued YBX from the YBX issuing account and pays it out to users when they run the CLAIM smart contract.

### Escrow Pool:

Public Key:  `GBU2XXS7XGQ34OSJ4QI3DRFIGXI53ROLA77IXPSVXJ4KSWV5VYUJG2PA`

The YBX escrow pool holds YBX rewards that are paid out to YBX escrows and used in the default protection events. It also issues veYBX and vYBX.&#x20;

### Utilization Tracker Accounts&#x20;

(Public keys tbd)

Utilization tracker accounts receive utilization delta payments from the pool account. Their balance is used to calculate aggregated utilization ratios for user positions.

### Issuance Tracker Accounts&#x20;

(Public Keys tbd)

Issuance Tracker accounts receive issuance ratio payments from the pool account. These payment amounts are used to calculate how much YBX a user should receive when they run a CLAIM function.


# Protocol Accounts

YieldBlox uses a variety of protocol accounts in its operations.

### Pool Account&#x20;

Public Key: `GCPFDAQGO3QZ6PUCXCPDHV4UEKJVLPKJEYY4BQHZBEJGHDVU6FPIF2VR`

The YieldBlox lending pool holds assets lent using the YieldBlox protocol. It also issues pool and liability tokens and controls collateral and loan claimable balances. Finally, it stores most protocol asset parameters in its data entries. The smart contracts fetch this information from the pool data entries when they require it.

#### Data Entries

Data entry format

- `Data Entry Key:Data Entry Value`

**Underlying Asset Related Data Entries**

Data entries for each asset supported by the protocol

- Underlying Asset Data - see [underlying asset data](underlying-asset-data.md) section.
- `{Underlying Asset Issuer Key}{Underlying Asset Overlap Key}{First 9 characters of underlying asset}_Underlying:{Issuer Account Public Key}_{Last 3 characters of underlying asset}`
  - Stores the underlying asset issuer and remaining characters from the underlying asset code so that the protocol can reconstruct the associated underlying asset from a protocol asset.

### Issuing Account:&#x20;

Public Key: `GBUYYBXWCLT2MOSSHRFCKMEDFOVSCAXNIEW424GLN666OEXHAAWBDYMX`

The YBX Issuing account is controlled by the YieldBlox smart contracts. It issues YBX during YBX issuance and default protection events (if necessary)

### Distribution Account:&#x20;

Public Key:`GCZIXLOVS6CCBSIORWL5Y3HYZJRUQ65UEHF3SNIZZH6OPN54YXH4AJGX`

The YBX distribution account receives issued YBX from the YBX issuing account and pays it out to users when they run the CLAIM smart contract.

#### Data Entries

Data entry format

- `Data Entry Key:Data Entry Value`

**Turret Related Data Entries**

For each turret that is a signer on protocol accounts

- `T_{Turret Signer Public Key}:{Turret Sponsor Public Key}`

  - Tracks the owners of the turret signers in control of the protocol

- `YieldBlox Contract Hash:{Contract Hash}`
  - The hash of the YieldBlox Contract uploaded to its signing turrets. Allows users to verify that the contract is the expected one

**YBX Issuance Related Data Entries**

- `YBX_Issuance_Rate:{daily issuance rate}`
  - The amount of remaining YBX to issue that is issued every day
- `YBX_Total_Supply:{total ybx supply}`
  - The total supply of YBX (currently 1.5 billion)

**Governance Proposal Related Data Entries**

- `Proposal_Creation_Threshold:{Threshold}`
  - Threshold of voting power needed to create a governance proposal
- `Custom_Quorum_Threshold:{Threshold}`
  - Governance proposal voting quorum needed to pass a custom governance proposal
- `Council_Quorum_Threshold:{Threshold}`
  - Governance proposal voting quorum needed to pass a council governance proposal
- `Locked_Contracts:{Locked Contract}_{Locked Contract}_`
  - List of all contracts currently locked by the governance smart contract

For every custom proposal outstanding

- `P_{Proposal Account Public Key}:{Proposal number}`

  - Tracks every custom proposal currently outstanding. The value is the custom proposal number, so if there are 2 proposals outstanding, 1 will have the number 0 and the other will have the number 1.

- `P_Allocation:{Allocation Proposal Account Public Key}`

  - Tracks the public key of the currently outstanding allocation proposal.

- `P_Council_Lock:{Lock Proposal Account Public Key}`

  - Tracks the public key of the currently outstanding council lock proposal if there is one.

- `P_Council_Swap:{Swap Proposal Account Public Key}`

  - Tracks the public key of the currently outstanding council swap proposal if there is one.

- `LAST_SIGNER_SWAP:{Last signer swap execution timestamp}`
  - Tracks the last time a signer swap was executed

### Escrow Pool:

Public Key: `GBU2XXS7XGQ34OSJ4QI3DRFIGXI53ROLA77IXPSVXJ4KSWV5VYUJG2PA`

The YBX escrow pool holds YBX rewards that are paid out to YBX escrows and used in the default protection events. It also issues veYBX and vYBX.&#x20;

### Interest Accrual Tracker Accounts&#x20;

(Public keys tbd)

Interest Accrual Tracker Accounts receive interest accrual payments from the pool account. Their balance is used to calculate aggregated utilization ratios for user positions.

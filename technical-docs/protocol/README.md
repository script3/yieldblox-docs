# Smart Contracts/Architecture

This section will cover all the smart contracts that YieldBlox uses. These contracts are all sub-contracts in the same master smart contract. But they are each handled independently and entered with a global event handler.

### Global Request Fields

The following fields are shared between all smart contract requests.

- userPublicKey: user public key&#x20;
- timestamp: current timestamp, if it is not from the last 5 minutes the smart contract will reject the request.
- type: Protocol function the user is requesting, stored as the following enum:

```
ProtocolEventTypes {
    TX_BURN = 0,
    TX_CLAIM = 1,
    TX_ESCROW = 2,
    TX_LIQUIDATE = 3,
    TX_MINT = 4,
    TX_PROPOSAL_CREATE = 5,
    TX_PROPOSAL_UPDATE = 6,
    TX_REPAY = 7,
    TX_VOTE = 8
}
```

### Other general contract information

#### Balance Line Objects

The BalanceLine object is often used to represent an asset (using an [assetId](#AssetId-Entries)) and an amount of that asset. It is the following object:

```
BalanceLine {
    assetId: string,
    amount: string
}
```

#### Repay Path Objects

The RepayPath object is used in repayments and liquidations to represent a path payment that should be taken to liquidate user collateral during a liquidation with collateral. The [assetId](#AssetId-Entries) fields in the object should represent underlying assets. The asset is as follows:

```
RepayPath {
  sendAssetId: string; // Expects underlying asset Id
  sendAmount: string;
  destAssetId: string;
  destAmount: string;
  path: string[];
}
```

NOTE: The object in the smart contract uses BigNumber objects for the amounts represented in the object. However, users should still input strings in their requests. The contract will handle transforming the object when it ingests the request.

#### AssetId Entries

assetId entries are strings that represent asset objects. They are structured as {assetCode}:{assetIssuer}.

#### PathPayment Handling

Whenever a `pathPayment` operation is used the contract first finds the most efficient path first and passes it into the operation.

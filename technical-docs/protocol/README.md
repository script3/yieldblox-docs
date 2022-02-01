# Smart Contracts/Architecture

This section will cover all the smart contracts that YieldBlox uses. These contracts are all sub-contracts in the same master smart contract. But they are each handled independently and entered with a global event handler.

#### Global Request Fields

The following fields are shared between all smart contract requests.

- User Public Key: user public key&#x20;
- Timestamp: current timestamp, if it is not from the last 5 minutes the smart contract will reject the request.
- Protocol Event: Protocol function the user is requesting
- Possible protocol event types:
  - TX_BURN
  - TX_GOVERNANCE
  - TX_LIQUIDATE
  - TX_MINT
  - TX_RATE
  - TX_REPAY
  - TX_CLAIM
  - TX_VOTE

### Other general contract information

- Whenever a `pathPayment` operation is used the contract first finds the most efficient path first and passes it into the operation.

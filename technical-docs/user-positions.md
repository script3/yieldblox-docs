# User Positions

YieldBlox user positions are stored on-chain using [claimable balances](https://developers.stellar.org/docs/glossary/claimable-balance/) that encode information about user positions in claimable balance claimants. To manipulate these balances the pool uses clawback claimable balance operations as both pool and liability tokens are clawback enabled.

### Collateral Claimable Balances

User collateral deposits are stored as claimable balances of pool tokens. Users normally sponsor these claimable balances, but the claimable balance is sponsored by the escrow pool instead if they get liquidated.

Claimants:

- Distribution Account or User - Predicate Never: By default the distribution account is a claimant, however, if a user is liquidated they become the claimant so the protocol knows the collateral belongs to them.

### Liability Claimable Balances

User borrows are stored as claimable balances of liability tokens. Users normally sponsor these claimable balances, but the claimable balance is sponsored by the escrow pool instead if they get liquidated.

Claimants:

- Distribution Account - Predicate Before Absolute Time: This claimant tracks the principal amount of the liability. So the amount that was originally borrowed.
- User - Predicate Never: If the liability balance was liquidated the user is added as a claimant so the protocol knows the liability belongs to them.

### Escrow YBX Claimable Balances

User YBX escrows are stored as claimable balances of YBX. The user typically sponsors these claimable balances. If they are liquidated, the escrow pool will sponsor them instead.

- Claimants:
  - Distribution Account - Predicate Not Before Absolute Time: The distribution account claimant predicate tracks the user's escrow period start date
  - Pool Account or Escrow Account - Predicate Not Before Absolute Time: This claimant tracks the user's escrow unlock date. If the pool account is the claimant the escrow is used as a collateral, if the escrow account is the claimant the escrow is not collateralized.
  - User - Predicate Never: If the escrow is liquidated the user is added as a claimant track that it belongs to them.
  - Issuing Account - Predicate Never: If the escrow is not allowed to be unlocked early the issuance account is added as a claimant to track unlocking early is not permitted.

###

---

# User Positions

YieldBlox user positions are stored on-chain using [claimable balances](https://developers.stellar.org/docs/glossary/claimable-balance/) that encode information about user positions in claimable balance claimants.

### Collateral Claimable Balances

User collateral deposits are stored as claimable balances of pool tokens. Users normally sponsor these claimable balances, but the claimable balance is sponsored by the staking pool instead if they get liquidated.

Claimants:

* User - Predicate Never: The user is added as a claimant on the claimable balance to track that it belongs to them.
* Pool - Predicate Unconditional: The pool is added as a claimant so it can claim the claimable balance if the user is liquidated.

### Liability Claimable Balances

User borrows are stored as claimable balances of liability tokens. Users normally sponsor these claimable balances, but the claimable balance is sponsored by the staking pool instead if they get liquidated.

Claimants:

* User - Predicate Never: The user is always added as a claimant on the claimable balance to track that it belongs to them.
* Pool - Predicate Unconditional: The pool is always added as a claimant so it can claim the claimable balance if the user is liquidated.
* Staking Pool - Predicate Before Absolute Time: Used to store the amount of this liability that needs to be used to repurchase YBX when the borrow is repaid. The accrued YBX purchase is multiplied by 10^7 before being encoded.
* Distribution Account - Predicate Before Absolute Time: This claimant is only added if the borrow is fixed rate. It tracks the assets utilization rate at the time of loan origination. The utilization ratio is multiplied by 10^7 before being encoded.

### Staked YBX Claimable Balances

User YBX stakes are stored as claimable balances of YBX. The user typically sponsors these claimable balances. If they are liquidated, the staking pool will sponsor them instead.

* Claimants:
  * User - Predicate Never: The user is added as a claimant on the claimable balance to track that it belongs to them.
  * Pool Account - Predicate Unconditional: The pool account claims the claimable balance when the user wants to unstake or is liquidated.
  * Distribution Account - Predicate Not Before Absolute Time: The distribution account claimant predicate tracks the users staking unlock date.



### sYBX Claimable Balances

User sYBX associated with YBX stakes are stored as claimable balances of sYBX. The user typically sponsors these claimable balances. If they are liquidated, the staking pool will sponsor them instead.

* Claimants:
  * User - Predicate Never: The user is added as a claimant on the claimable balance to track that it belongs to them.
  * Staking Pool - Predicate Unconditional: The staking pool claims the claimable balance when the user wants to unstake or is liquidated.
  * Distribution Account - Predicate Not Before Absolute Time: The distribution account claimant predicate tracks the users staking unlock date.





###

****




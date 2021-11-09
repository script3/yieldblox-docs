# Staking Contract

### Staking

Users will stake and unstake through this contract. Staking periods are 3 month periods, 6 month periods, or 12 month periods. Users who stake YBX will receive sYBX, which accrues staking fees and has voting power.

**Request**

```
{    
    userPublicKey: string,
    timestamp: number,
    type: string,
    unstakeAmount: string,
    stakeAmount?: string,
    period?: number,
    unstakeEarlyAmount?: string
}
```

**Fields:**

* Unstake Amount: Amount of unlocked YBX the user would like to unstake
  * Note: You cannot unstake an amount that would bring your health factor below 1.1
* Stake Amount (Optional): Amount of YBX being staked
* Period (Optional): 3, 6 or 9 month period to have staked YBX locked up
* Unstake Early Amount (Optional): amount of YBX being un-staked prior to the defined staking period
  * Note: You cannot unstake an amount that would bring your health factor below 1.1

### High-Level Contract Process Flow

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon.
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object.
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. If the user is staking the contract handles staking.
   1. Contract adds a `createClaimableBalance` operation where the user creates a YBX staking claimable balance.
   2. Contract calculates the amount of sYBX the user should receive based on their staking period and staking amount.
   3. Contract adds a `createClaimableBalance` operation where the user creates a sYBX staking claimable balance.
5. If the user is unstaking the contract handles unstaking.
   1. Contract calculates the maximum the user can unstake.
      1. This is necessary because users can borrow against staked YBX. So they cannot unstake an amount that would bring their health factor below 1.
   2. Contract checks how much staked YBX is unlocked for the user.
   3. Contract takes the smallest of the users maximum unstake, the users unlocked YBX, and the users input unstake amount. This is the amount that will be unstaked.
   4. Contract adds `claimClaimableBalance` operations where the pool claims unlocked YBX staking claimable balances until it reaches the unstake amount found in 3.
   5. Contract adds `claimClaimableBalance` operations where the staking pool claims all sYBX stakes associated with the claimed YBX stakes.
      1. This burns the sYBX.
   6. Contract adds `createClaimableBalance` operations where the pool re-creates YBX and the staking pool re-creates sYBX stake claimable balances if it claimed over the unstake amount.
      1. User sponsors these claimable balances.
   7. Contract calculates the value of the claimed sYBX.
   8. Contract adds a `payment` operation where the staking pool pays the user the value of their sYBX (the amount of YBX it's worth).
   9. Contract adds a `payment` operation where the pool pays the user all unstaked YBX.
6. If the user is unstaking early the contract handles unstaking early.
   1. Contract calculates the maximum the user can unstake.
      1. This is necessary because users can borrow against staked YBX. So they cannot unstake an amount that would bring their health factor below.
      2. This takes into account any YBX unstaked through normal unstaking.
   2. Contract takes the smallest of the users maximum unstake and the users input unstake early amount. This is the amount that will be unstaked.
   3. Contract adds `claimClaimableBalance` operations where the pool claims unlocked YBX staking claimable balances until it reaches the unstake amount found in 3.
   4. Contract adds `claimClaimableBalance` operations where the staking pool claims all sYBX stakes associated with the claimed YBX stakes.
      1. This burns the sYBX.
   5. Contract adds `createClaimableBalance` operations where the pool re-creates YBX and the staking pool re-creates sYBX stake claimable balances if it claimed over the unstake amount.
      1. User sponsors these claimable balances.
   6. Contract adds a `payment` operation where the pool pays the user all unstaked YBX.
7. Turret builds transaction builder into an XDR and returns it along with a signature.






# Escrow Contract

### Escrows

Users will lock and unlock escrows through this contract. Escrowing periods are 3 month periods, 6 month periods, or 12 month periods. Users who escrow YBX will receive veYBX, which accrues escrowing fees and has voting power.

**Request**

```
{
    userPublicKey: string,
    timestamp: number,
    fee: string
    type: ProtocolEventTypes,
    unlocks?: {escrowId: string, amount: string}[],
    earlyUnlocks?: {escrowId: string, amount: string}[],
    lockAmount?: string,
    period?: number,
}
```

**Fields:**

- unlocks (OPTIONAL): Array of claimable balance ids tied to unlocked escrows and the amount from each of these escrows that the user would like to unlock.
  - Note: Users cannot unlock an amount that would bring your health factor below 1.1 or leave them with more votes than they have voting power.
- earlyUnlocks (OPTIONAL): Array of claimable balance ids tied to locked escrows and the amount from each of these escrows that the user would like to unlock.
  - Note: You cannot unlock an amount that would bring your health factor below 1.1.
- Lock Amount (OPTIONAL): Amount of YBX being locked
- Period (OPTIONAL): 3, 6 or 9 month period to lock YBX
- Unlock Early Amount (OPTIONAL): amount of YBX being unlocked prior to the defined unlock period
  - Note: You cannot unlock an amount that would bring your health factor below 1.1

### High-Level Contract Process Flow

The escrow contract changed after these docs were written. A revised contract process flow is coming soon!

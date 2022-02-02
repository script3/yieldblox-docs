# Escrow Contract

### Escrows

Users will lock and unlock escrows through this contract. Escrowing periods are 3 month periods, 6 month periods, or 12 month periods. Users who escrow YBX will receive veYBX, which accrues escrowing fees and has voting power.

**Request**

```
{
    userPublicKey: string,
    timestamp: number,
    type: string,
    unlockAmount: string,
    lockAmount?: string,
    period?: number,
    unlockEarlyAmount?: string
}
```

**Fields:**

- Unlock Amount: Amount of unlocked YBX the user would like to unlock
  - Note: You cannot unlock an amount that would bring your health factor below 1.1
- Lock Amount (Optional): Amount of YBX being locked
- Period (Optional): 3, 6 or 9 month period to lock YBX
- Unlock Early Amount (Optional): amount of YBX being unlocked prior to the defined unlock period
  - Note: You cannot unlock an amount that would bring your health factor below 1.1

### High-Level Contract Process Flow

The escrow contract changed after these docs were written. A revised contract process flow is coming soon!

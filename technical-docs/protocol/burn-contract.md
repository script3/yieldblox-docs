# Burn Contract

The burn contract is used to exchange pool tokens for the underlying assets they represent. The calculations used here will find the proportional amount of pool tokens burned in respect to pool tokens outstanding. The request consists of an Amount and the Pool Token Code of the pool token to be burned. Users will receive the respective proportion of the underlying asset after burning pool tokens.

**Request**

```
{
    userPublicKey: string,
    timestamp: number,
    fee: string,
    type: ProtocolEventTypes,
    withdrawal?: BalanceLine,
    burn?: BalanceLine
}
```

#### Fields:

- withdrawal (OPTIONAL): [BalanceLine](README.md#Balance-Line-Objects) representing the pool token being uncollateralized and the amount of the pool token being uncollateralized.
- burn (OPTIONAL): [BalanceLine](README.md#Balance-Line-Objects) representing the pool token being burned and the amount of the pool token being burned.

### High-Level Contract Process Flow (MAY BE OUT OF DATE)

1. User enters the contract through an event handler which transforms their request.
2. Contract prerequisite data from horizon
   1. Pool Account Data
   2. User Account Data
   3. User Position Data
3. Contract builds a transaction builder object
   1. This is the object operations will be added to throughout the rest of the contract process flow.
4. Contract calculates the value of the poolToken, subtracting withdrawal fees.
5. Contract adds a `payment` operation where the pool sends withdrawal fees to the DAO treasury.
6. Contract adds a `payment` operation where the user pays the poolTokens they are burning to the pool (deleting them).
7. Contract adds a `payment` operation where the pool pays the value of the burned pool tokens in underlying to the user.
8. Contract adds operations to handle Utilization Updates and Corrections. See Average Utilization Ratios section.
9. Turret builds, signs, and returns transaction XDR.

### Diagram

![Diagram may be out of daye](<../../.gitbook/assets/image (26).png>)

**Account A:** Lends 2,000 XLM and receives 2,000 y00XLM. Pool takes in 3,000 XLM in fees over the course of time. Account A now decides to withdraw and burn pool tokens in return for the underlying asset. The proportion of the liquidity provided is returned as well as a proportion of interest.

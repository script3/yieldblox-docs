# Interest Rates

## How do loan interest rates work?

Users can borrow from YieldBlox at either fixed or floating [interest rates](../../technical-docs/math.md#interest-rate-calculations). Floating rates are based purely on demand and will fluctuate based on the borrowed assets utilization ratio. Fixed rates are a multiple of the floating rate at loan origination. Fixed rates will always be higher than floating rates, but some borrowers may prefer the stability of fixed rates. Interest rates accrue onto the borrower's liability balance over the lifecycle of their loans, but interest does not need to be repaid until loan repayment.

## What is a Utilization Ratio?

An assets [utilization ratio](../../technical-docs/math.md#utilization-ratio-calculations) is the percentage of deposited assets in the pool that are currently lent out. It is used to calculate the [variable interest rate](../../technical-docs/math.md#interest-rate-calculations) paid by borrowers.

## What if I want to change my rate?

Users can change their interest rates from fixed to floating or vice versa at any time. To do so, a user will go to their Profile page and find their borrowed positions. Once they select the 'Type' edit button, they will be notified they are switching interest types. Then they confirm this switch.

![](<../../.gitbook/assets/image (7).png>)

A loan's fixed rate can be force rebalanced up to the current stable rate if the loan's rate has fallen below the market floating rate.&#x20;

## Where do the interest fees go?

Most (50-90%) of the interest rate fees are sent directly to the lending pool to be distributed to protocol lenders. Lenders will withdraw these fees when they burn their pool tokens. The remaining 10% of fees are used to repurchase YBX tokens on the Stellar DEX, which are redistributed to YBX Stakers. This repurchasing is necessary to support the [YBX backstop](../../technical-docs/protocol/#ybx-backstop).

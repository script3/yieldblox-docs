# Interest Rates

YieldBlox interest rates are calculates using 4 different slopes that step up as different utilization rates are hit. This is designed to improve capital efficiency, allowing the rate to move reflexively with demand and support higher utilization levels while also preventing liquidity crunches in the protocol. As you can see by the graph below, in the final slope interest rates begin moving up extremely fast. This is to prevent a liquidity crunch by either forcing borrowers to quickly repay or enticing lenders to quickly deposit.

### Interest Rate Curve Graphs:

![Note: these numbers may change](<../.gitbook/assets/image (22).png>)

![Note: these numbers may change](<../.gitbook/assets/image (27).png>)

### Sample Interest Rate Calculation:

_**Please Note all Numbers are Examples and not indicative of real Protocol Variables**_

Utilization Rate: .95

Interest Rate Thresholds:

- Threshold 1: .7
- Threshold 2: .9
- Threshold 3: .97

Base Interest Rate: .05

Interest Rate Slopes"

- Slope 0: .2
- Slope 1: 1.5
- Slope 2: 7.5
- Slope 3: 350

In this case the interest rate would be 86.5%

.05+ .7\*.2+1.5\*(.9-.7)+7.5\*(.95-.9) = .865

# Accrued Interest Tracking

In order to track accrued interest on floating rate loans, we must accrue interest to a user's liability every time their borrowing interest rate changes. We accomplish this by tracking users' liabilities with liability tokens that increase in value over time, accruing interest to all outstanding loans.

### Accrued Interest Tracker Overview

Tracking accrued interest for underlying assets is done using an accrued interest tracker account that starts with a balance of 1000 interest tracking tokens and receives interest accrual payments every time the utilization ratio of the asset it's tracking changes. Effectively, this means the account is tracking the liability value of a loan taken out at protocol origination. When a user borrows from the protocol we store their borrowed amount divided by the interest tracker balance, then at all points in the future we can multiply that quotient by the current interest tracker balance divided by the starting interest tracker balance to get the current value of a user's liabilities.

### Accrued Interest Tracker Payments

Every time the utilization ratio of an underlying asset changes, the pool makes an accrued interest payment to the accrued interest tracker account. The payment amount is equal to the per-block interest accrued on the balance of the accrued interest tracker account times the number of blocks between the second to last and last utilization modifying transactions. This means that accrued interest tracking lags one period. The indicator must lag because turret smart contracts do not have an accurate view of the current ledger, so they need to look at past ledger state to ensure truthfulness. See Math for the equation.

To provide an example, we'll outline the utilization delta payment of a sample transaction (transaction 100):

* **Transaction 98 - block 1000 - depositing XLM**
  * Protocol state pre-transaction 98
    * Pool Balance: 90 XLM&#x20;
    * XLM Liabilities: 100 XLM&#x20;
    * XLM Utilization Ratio: .526
    * Accrued interest tracker balance: 100
  * Transaction 98 Action:&#x20;
    * Deposits 10 XLM into lending pool
  * Protocol state post-transaction 98
    * Pool Balance: 100 XLM&#x20;
    * XLM Liabilities: 100 XLM&#x20;
    * XLM Utilization Ratio: .5
* **Transaction 99: Block 1100 - Borrowing XLM**
  * Details irrelevant
* **Transaction 100: Block irrelevant - Borrowing XLM **
  * Details irrelevant
  *   Accrued Interest Payment

      * Makes accrued interest payment of 50 interest tracker assets to the accrued interest tracker account
        * 100\*(.05+.526\*0.2)/(6,307,200)\*(1100-1000) = 0.0002461

      It should be noted that transactions 98 and 99 would also have made accrued interest payments; they just weren't the focus of this example.

### Accrued Interest Corrections

In addition to accrued interest payments, the accruet interest tracker sysrem also makes accrued interest correction clawbacks and payments. These take place in the same transaction as accrued interest payments. This is necessary because the accrued interest tracker can apply an incorrect payment if its ledger view is incorrect and missing the most recent transaction (this commonly occurs when two users interact with the protocol simultaneously).&#x20;

#### Accrued Interest Correction Process

When an accrued interest payment is calculated, the smart contract also checks the last utilization delta payment to see if it was correct. If it was not correct, the tracker calculates what the correction should be (undoing the bad delta and adding the correct one), then repeats the process, checking the next payment back. Once the smart contract finds the total correction, it is applied in either a payment or clawback operation depending on whether the correction was positive or negative.  It should be noted that since there is a 5 minute timebounds on protocol transactions, the utilization tracker assumes that any accrued interest payment 5 minutes newer than the previous one was correct.

To provide an example, we'll outline the accrued interest correction payment of a sample transaction (transaction 100):

* **Transaction 97 - Block 900 - Deposit XLM**
  * Protocol state pre-transaction 97
    * Pool Balance: 60 XLM
    * &#x20;XLM Liabilities: 100 XLM
    * Utilization Ratio: .625
    * Accrued interest tracker balance: 1000
  * Transaction 97 Action
    * Deposit 20 XLM
    * Accrued interest tracker payment of .01
  * Protocol state post-transaction 97
    * Pool Balance: 80 XLM
    * &#x20;XLM Liabilities: 100 XLM
    * Utilizaiton Ratio: .5555556
    * Accrued interest tracker balance: 1000.01
* **Transaction 98- Block 1000 - Deposits XLM**
  * Protocol state pre-transaction 98
    * Pool Balance: 80 XLM
    * &#x20;XLM Liabilities: 100 XLM
    * Utilization Ratio: .5555556
    * Accrued interest tracker balance: 1000.01
  * Transaction 98 action
    * Deposit 20 XLM
    * Accrued interest tracker payment: .01
  * Protocol state post-transaction 98
    * Pool Balance: 100 XLM&#x20;
    * XLM Liabilities: 100 XLM&#x20;
    * Utilization Ratio: .5
    * Accrued interest tracker balance: 1000.02
* **Transaction 99 - Block 1010 - Borrows XLM **
  * Protocol state pre-transaction 99
    * Pool Balance: 100 XLM
    * &#x20;XLM Liabilities: 100 XLM
    * Utilization Ratio: .5
    * Accrued interest tracker balance: 1000.02
  * Transaction 99 action
    * Borrows 100 XLM
    * Makes an accrued interest tracker payment of .002
      * This is incorrect, correct payment is .002774
        * (0.05+0.625\*0.2)/(6,307,200)(1000-900)\*1000 = .002774
  * Protocol state post-transaction 99
    * Pool Balance: 100 XLM&#x20;
    * XLM Liabilities: 100 XLM&#x20;
    * Utilization Ratio: .5
    * Accrued interest tracker balance: 1000.022
* **Transaction 100 - Borrows XLM  **
  * Protocol state pre-transaction 100
    * Accrued interest tracker balance: 1000.022
    * Other information irrelevant
  * Protocol actions
    * Borrow XLM
    * Make a accrued interest correction payment of .000774
      * .002774 - .002 = .000774
    * Make an accrued interest tracker payment of .0002554
      * (0.05+0.555556\*0.2)/(6,307,200)(1010-1000)\*1000 = .0002554
* Protocol state pre-transaction 100
  * Accrued interest tracker balance: 1000.02303
  * Other information irrelevant

#### Using the Accrued Interest Tracker to find the value of a user liability.

To find the value of a users liability the protocol multiplies the number of liability tokens associated with that liability times the accrued interest tracker balance plus the expected next accrued interest tracker payment divided by the starting tracker balance.

For Example:

* User's liability claimable balance contains 99.8 l00XLM tokens
* 00XLM's accrued interest tracker account has 1005.2 i00XLM
  * Next expected payment is .2 i00XLM
* User's liability is 100.33892 XLM
  * (1005.2+.2)/1000 \* 99.8 = 100.33892

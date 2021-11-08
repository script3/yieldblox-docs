# Average Utilization Ratios

In order to calculate correct interest rates on floating rate loans we must track an assets average utilization rate over time so we know what the average utilization rate (and therefore interest rate) was for a users borrow.

### Utilization Tracker Overview

Tracking average utilization ratios for underlying assets is done using a utilization ratio feed which consists of a series of utilization delta payments. The feed is comprised of three parts:

1. &#x20;A utilization tracker account that receives utilization delta payments of the utilization tracker asset payments&#x20;
2. A utilization tracker asset which is paid to the utilization tracker account in utilizatoin delta payments
3. The staking pool account which pays the utilization tracker asset to the utilization tracker account&#x20;

Using these components, the utilization feed tracks a lagging block-weighted utilization ratio which we can use to find the average utilization ratio for a given loan. The indicator must lag because turret smart contracts do not have an accurate view of the current ledger, so they need to look at past ledger state to ensure truthfulness.

### Utilization Delta Payments

Every time the utilization ratio of an underlying asset changes, the staking pool makes a utilization delta payment to the utilization tracker account. The payment amount is equal to the utilization ratio of the asset after the second to last utilization modifying transaction times the number of blocks between the second to last and last utilization modifying transactions. See Math for the equation.

To provide an example, we'll outline the utilization delta payment of a sample transaction (transaction 100):

* Transaction 98 - block 1000 - depositing XLM
  * Protocol state pre-transaction 98
    * Pool Balance: 90 XLM&#x20;
    * XLM Liabilities: 100 XLM&#x20;
    * XLM Utilization Ratio: .526
  * Transaction 98 Action:&#x20;
    * Deposits 10 XLM into lending pool
  * Protocol state post-transaction 98
    * Pool Balance: 100 XLM&#x20;
    * XLM Liabilities: 100 XLM&#x20;
    * XLM Utilization Ratio: .5
* Transaction 99: Block 1100 - Borrowing XLM
  * Details irrelevant
* Transaction 100: Block irrelevant - Borrowing XLM&#x20;
  * Details irrelevant
  * Utilizaiton Delta Payment
    *   Makes a Utilization Delta payment of 50 utilization tracker assets to the utilization tracker account

        * 100/(100+100) \*100 = 50

        It should be noted that transactions 98 and 99 would also have made utilization delta payments; they just weren't the focus of this example.

### Utilization Delta Corrections

In addition to utilization delta payments, the utilization tracker feed also makes utilization correction clawbacks and payments. These take place in the same transaction as utilization delta payments. This is necessary because the utilization tracker can apply an incorrect payment if its ledger view is incorrect and missing the most recent transaction (this commonly occurs when two users interact with the protocol simultaneously).&#x20;

#### Utilization Delta Process

When a utilization delta payment is calculated, the smart contract also checks the last utilization delta payment to see if it was correct. If it was not correct, the tracker calculates what the correction should be (undoing the bad delta and adding the correct one), then repeats the process, checking the next payment back. Once the smart contract finds the total correction, it is applied in either a payment or clawback operation depending on whether the correction was positive or negative.  It should be noted that since there is a 5 minute timebounds on protocol transactions, the utilization tracker assumes that any utilization delta payment 5 minutes older than the following one was correct.

To provide an example, we'll outline the utilization correction payment of a sample transaction (transaction 100):

* Transaction 97 - Block 900 - Deposit XLM
  * Protocol state pre-transaction 97
    * Pool Balance: 60 XLM
    * &#x20;XLM Liabilities: 100 XLM
    * Utilizaiton Ratio: .625
  * Transaction 97 Action
    * Deposit 20 XLM
  * Protocol state post-transaction 97
    * Pool Balance: 80 XLM
    * &#x20;XLM Liabilities: 100 XLM
    * Utilizaiton Ratio: .5555556
* Transaction 98- Block 1000 - Deposits XLM
  * Protocol state pre-transaction 98
    * Pool Balance: 80 XLM
    * &#x20;XLM Liabilities: 100 XLM
    * Utilizaiton Ratio: .5555556
  * Transaction 98 action
    * Deposit 20 XLM
  * Protocol state post-transaction 98
    * Pool Balance: 100 XLM&#x20;
    * XLM Liabilities: 100 XLM&#x20;
    * Utilization Ratio: .5
* Transaction 99- Block 1010 -Borrows XLM and makes a Utilization Delta payment of 37.5 XLM (this is incorrect)
  * Correct payment: 80/(80+100)\*100=55.5555556
  * Other details do not matter
* Transaction 100: Borrows XLM  and makes a Utilization Correction payment of 6.9444444 utilization tracker assets to the utilization tracker account
  * Correction = 44.4444444 - 37.5 = 6.94444444

#### Using the Utilization Tracker to find a loans average Utilization Ratio

To find an average utilization ratio for a loan the protocol finds the original utilization tracker balance using result meta XDRs then validates that it's correct also using result meta XDRs. It then get the originating loan block from the claimable balance object that represents the loan. At this point the protocol has all necessary information to calculate average utilization ratio for a loan. See Math for the equation.

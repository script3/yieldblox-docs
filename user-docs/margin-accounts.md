# Margin Accounts

![](<../.gitbook/assets/margin acc header.svg>)

YieldBlox allows users to open margin accounts to trade on the Stellar DEX with up to 5x leverage. This feature will not be available in the alpha version of YieldBlox. The beta release will include it.

## How do YieldBlox margin accounts work?

Users open YieldBlox margin accounts by opening a new Stellar account with YieldBlox, depositing collateral, and borrowing up to 5x their collateral value from the YieldBlox lending pool. They can then trade on the Stellar DEX with the borrowed assets. They can close the account at any time by repaying their borrowed assets plus accrued interest. They keep any remaining assets in their account. For example, say Trader A opens a margin account by depositing $100 of XLM as collateral. Next, they borrow 500 USDC and trade it for XLM on the Stellar DEX. If the price of XLM increases 10%, they can sell the XLM they bought for 550 USDC, then repay their 500 USDC borrow. They will be left with the $100 of XLM they deposited as collateral and the $50 they made from trading.&#x20;

YieldBlox assumes partial control over margin accounts, so the protocol must approve all trades. This is to ensure margin account users cannot transfer their borrowed tokens out of their margin account.

## What interest rates do margin accounts charge?

Margin accounts use the same [demand-based interest rate](lending-borrowing/interest-rates.md) system as traditional borrowing. In the case of margin accounts **≈40%** of interest fees are used to repurchase YBX and redistribute it to YBX stakers. The remaining amount is sent to the lending pool.

## Can margin accounts be liquidated?

Although the health factor equation varies slightly, margin accounts use a [health factor system](lending-borrowing/health-factors.md) like traditional borrowing does. Other protocol participants can liquidate margin accounts if their health factor drops below 1.00. In these liquidations, a portion of the margin account's holdings may be withdrawn by the liquidator in addition to a portion of their collateral.&#x20;

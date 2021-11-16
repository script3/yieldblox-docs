# Why Stellar?

![](<../.gitbook/assets/why stellar header (1).svg>)

## Stellar & YieldBlox

YieldBlox uses [Stellar's decentralized ledger](https://developers.stellar.org/docs/glossary/ledger/) to support the protocol, and it is the ideal platform for YieldBlox.

In Stellar's words:

> Fundamentally, Stellar is a system for tracking ownership. It uses an accounting ledger, shared across a network of independent computers, to store two important things for every account holder: what they own (their account balances) and what they want to do with what they own (operations on those balances, like buy or sell offers). The computers that run Stellar and publish the ledger are called nodes. They systematically validate the ledger’s contents so it’s always consistent across the network. For example, when you send someone a dollar on a Stellar-built app, the nodes check that the correct balances were debited and credited, and each node makes sure every other node sees and agrees to the transaction.

Stellar's open network allows anyone to submit a transaction to change the ledger. However, the transaction only changes the ledger after the nodes agree it is valid.

In YieldBlox’s case, before a loan is taken out or repaid, the local network of nodes agree upon the transaction's validity. This prevents parties with ill intentions from engaging in illicit behavior on the network. Therefore, Stellar provides a secure financial network with one source of truth and can be instantly accessed and modified by anyone in the world.

## Why we built YieldBlox on Stellar

The Stellar network has some key characteristics which YieldBlox takes advantage of:\


* ****[**Stellar's Consensus Protocol**](https://developers.stellar.org/docs/glossary/scp/)\
  The SCP enables the Stellar Blockchain to offer extremely low fees and settlement times. In addition, it follows a federated byzantine agreement model, which allows the network to remain decentralized and antifragile without requiring a large validator set or economic incentives.\

* **Focus on Finance**\
  Stellar is a non-programmable blockchain by design. It is meant to be used almost exclusively for facilitating financial services. This reduces network bloat and ensures high-performance for the financial infrastructure using the network.\

* **High Capital Efficiency**\
  ****Stellar uses an on-chain DEX that prevents liquidity fragmentation within the ecosystem. When AMM’s are added to the network (currently in the works), trades will execute against both AMM’s and the DEX to preserve capital efficiency. This interleaved execution improves liquidity and reduces in-network arbitrage opportunities, resulting in efficient trading.\

* **Established Ecosystem Standards**\
  ****Building Fintech apps with Stellar is extremely easy due to the strength of Stellar’s ecosystem standards. Multiple cohesive SDKs make it easy to interface an app with Stellar. Additionally, Stellar has excellent specifications for on and off-ramping fiat currencies and handling KYC, making it easy for fintech apps to onboard non-blockchain-native users.\

* ****[**Anchors**](https://developers.stellar.org/docs/anchoring-assets/)\
  Stellar has a multi-asset functionality called anchoring which enables users to create custom assets on its ledger tied to real-world assets. This means YieldBlox can support the lending of any asset.\

* ****[**Stellar Turrets**\
  ](https://tss.stellar.org)Currently in development, Stellar Turrets (Turrets) will be a new feature to the Stellar ecosystem. Turrets are a decentralized network of servers that hold uploaded smart contracts that can then be tied to private keys. Transactions are signed with these private keys if the transactions meet the requirements of the smart contracts. The YieldBlox protocol uses this new tool to manage some of the Turing complete logic surrounding loan processing.



## Stellar's Security Features

![](<../.gitbook/assets/stellar security.svg>)

YieldBlox uses Stellar's security features to ensure loans and collateral accounts associated with the protocol are safe from risks.

* ****[**Stellar Turrets Protocol**\
  ****](https://github.com/tyvdh/turing-signing-server)The Turrets protocol provides YieldBlox with a method of adding Turing complete smart contract logic to transactions without requiring Script3 to control the accounts involved in the transactions. This decentralizes YieldBlox without reducing efficiency.\

* ****[**Multi-Sig**\
  ****](https://developers.stellar.org/docs/glossary/multisig/)YieldBlox margin account users must store borrowed assets in accounts partially controlled by the YieldBlox protocol. This is to ensure they cannot transfer the assets outside of the protocol ecosystem. Stellar’s multi-sig capability allows YieldBlox to add all necessary Turret signers to the margin account and modify account thresholds so that the user does not have complete control over the account. Thus preventing the account from submitting transactions without using Turret functions. This security measure locks borrowed assets in the margin account until margin repayment or liquidation.\

* ****[**Claimable Balances**](https://developers.stellar.org/docs/glossary/claimable-balance/)****\
  ****YieldBlox uses claimable balances to manage user collateral balances. Borrowers must lock their collateral in claimable balances until they repay any loans. The balances are only claimable by the YieldBlox pool account, so the user cannot withdraw collateral without protocol approval.\

* ****[**Path Payments**](https://developers.stellar.org/docs/start/list-of-operations/#path-payment-strict-send)****\
  ****Stellar path payments enable users to atomically repay borrows and perform liquidations with collateral deposits. The transaction attempts to trade collateral assets for the necessary assets to repay the borrow. This allows the transaction to dynamically adjust the amount of assets sold to make the most efficient trade possible. Furthermore, if the trade is not possible, the transaction will revert without causing any harm.\

* ****[**Asset Controls**](https://developers.stellar.org/docs/issuing-assets/control-asset-access/)****\
  ****YieldBlox FX forwards use a credit model that tokenizes each leg of the forward. Users are not allowed to send these assets to other accounts or trade them for non-credit assets. With Stellar's asset controls, YieldBlox can require users to request trade approval for trades from YieldBlox smart contracts before they can be submitted. This enables the protocol to ensure the tokens are only being traded for other tokenized FX forward credits.\

* ****[**Stellar's Consensus Protocol**\
  ****](https://developers.stellar.org/docs/glossary/scp/)The consensus protocol rejects transactions when they do not align with the correct ledger state. For example, a user could not fill a sell offer if their account lacked the necessary funds to complete the trade.



## What are Anchors?

![](../.gitbook/assets/anchors.svg)

[Anchors](https://developers.stellar.org/docs/anchoring-assets/) are on/off ramps to the Stellar network with fiat currencies.

For YieldBlox to ease equitable access globally, anchors need to be readily available within the Stellar ecosystem. To lend or borrow a non-native asset, a third party must already be anchoring that asset.

Here are some non-native assets reputable third parties currently anchor:

* **USDC**\
  US dollar anchor provided by [Centre](https://www.centre.io)\

* **CNY**\
  Chinese yuan anchor provided by [RippleFox](https://ripplefox.com)\

* **EURT**\
  Euro anchor provided by [Tempo](https://tempo.eu.com/home)\

* **NGNT **\
  Nigerian naira anchor provided by [Cowrie](https://www.cowrie.exchange)\

* **BRL**\
  Brazilian real anchor provided by [ntokens](https://www.ntokens.com)\

* **ARST**\
  Argentine pes anchor provided by [Stablex](https://stablex.org)\

* **GOLD**\
  Gold anchor provided by [StellarMetals](https://stellarmetals.org)\

* **BTC**\
  Bitcoin anchor provided by [Papaya](https://apay.io/in)\

* **ETH**\
  Ethereum anchor provided by [Interstellar](https://interstellar.exchange)\

* **DSTOQ**\
  Equities anchor provided by [DSTOQ](https://www.dstoq.com)

More anchors can be viewed on [Stellar Expert](https://stellar.expert/explorer/public/).



### More Information on Stellar

{% embed url="https://www.stellar.org/" %}


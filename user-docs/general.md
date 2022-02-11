---
cover: ../.gitbook/assets/YBX Slide (1).png
coverY: 0
---

# General

## What is YieldBlox?

YieldBlox is a decentralized finance (DeFi) protocol for lending and borrowing built on [Stellar](https://www.stellar.org). Users carry out all protocol functions using YieldBlox's smart contracts hosted on [Stellar Turrets](https://tss.stellar.org). These can be accessed either directly using API calls, or through a front-end such as Script3's [YieldBlox web app](https://www.yieldblox.finance/).

## What is a decentralized finance protocol?

A decentralized finance protocol is a financial application that does not rely on or require its users to trust a central intermediary. This is often achieved by building the protocol using immutable smart contracts that run on a distributed network. In YieldBlox's case, it operates using smart contracts built with the Stellar Turrets smart contract engine. There is no central organization that controls YieldBlox and no organization YieldBlox relies on to continue operating. This means that YieldBlox is non-custodial, trust-minimized, and censorship-resistant.

## What is unique about YieldBlox?

The DeFi money market landscape is competitive. There are a variety of money market protocols built on programmable blockchains like Ethereum and Solana. Nevertheless, YieldBlox has made several improvements on existing money market protocol models and created a unique offering.

**Platform Focus**

Stellar is a unique blockchain in that it's an ideal backend for fintech platforms. It's easy for a small team to spin up a mobile application and plug into the Stellar network to provide their users with payment and trading capabilities. YieldBlox was built with these platforms in mind. Platforms can use YieldBlox to provide their users with lending and borrowing tools without reducing the decentralization of their platform. In addition, platforms can leverage YieldBlox's unique tokenomics model and isolated lending markets to bootstrap growth of their own platform, ease anchor adoption, and build a non-custodial revenue model. A further discussion of this potential can be found in [this article](https://medium.com/script3/yieldblox-will-transform-capital-and-incentives-in-the-stellar-ecosystem-828be5023765) written by Script3.

**High Capital Efficiency**

For money markets, high capital efficiency is directly correlated with high utility. The higher a money market protocol's capital efficiency is, the more useful deposits are for users. The most straightforward way to increase capital efficiency is by increasing the loan-to-value ratios offered by the protocol. However, this comes with an increased risk of underwater positions. YieldBlox's unique [Default Protection](lending-borrowing/default-protection.md) mechanism greatly reduces the risk that underwater positions pose, allowing the protocol to safely offer high loan-to-value ratios.

**Unique Tokenomics**

Tokenomics, when designed correctly, are an invaluable tool for a DeFi protocol. YBX, YieldBlox's utility token utilizes a [five-level tokenomics model](ybx-tokens/ybx-tokenomics.md) that touches every portion of the protocol.

**Built on Stellar**

YieldBlox is the first DeFi protocol built on Stellar. Stellar is an excellent platform for DeFi protocols with extremely fast transactions, low fees, and an ecosystem that is well equipped to tokenize real-world assets. Additionally, Stellar's focus on developing countries means YieldBlox will be able to serve a user base that has traditionally been hard for DeFi protocols to tap into.

## What are the benefits of YieldBlox?

YieldBlox brings a decentralized, on-ledger money market to the Stellar ecosystem.\
Within the ecosystem, this promises to:

- Increase and trading payment liquidity
- Improve capital productivity
- Reduce reliance on lending intermediaries like banks
- Serve a global market with a cost of less than $0.01 per transaction

## How do I use YieldBlox?

Script3 maintains a [web app](https://testnet.yieldblox.finance) that allows users to interact with the protocol.

The web app currently supports the following wallets:

- [**Freighter**](https://www.freighter.app)\*\*\*\*
- \***\*[**Albedo**](https://albedo.link)\*\***

As other interfaces begin to integrate YieldBlox, a list of these integrations will be shown here!

---

More technical users can also use YieldBlox directly through the Turret network that supports it. Please see the [Stellar Turrets documentation](https://turrets.stellar.org) and the technical-docs section for more information.

## Does YieldBlox have fees?

While they are very small, YieldBlox does have four types of fees:

**Network Fees**

YieldBlox users must pay [Stellar Network fees](https://developers.stellar.org/docs/glossary/fees/) and Stellar Turret fees for each transaction. Both of these fees are extremely low. We expect them to amount to less than one cent (< $0.01) per transaction.

**Interest Rates**

Borrowers on YieldBlox must pay [interest fees](lending-borrowing/interest-rates.md) to lenders. These fluctuate based on demand.

**Withdrawal Fees**

YieldBlox users must pay [withdrawal fees](lending-borrowing/lending.md) when they withdraw assets from the protocol. These are paid to the YieldBlox DAO treasury

**Liquidation Fees**

YieldBlox liquidators must pay [liquidation fees](lending-borrowing/liquidations.md) when they liquidate another user. These are a small portion of the liquidation incentive that they receive for the liquidation, they are paid to the YieldBlox escrow pool.

## Can YieldBlox be changed or upgraded?

Yes. The YieldBlox protocol can be changed or updated using the [governance](governance.md) model.

## How does governance work?

The YieldBlox protocol is updated and maintained using a [governance](governance.md) token model. Users receive [YBX tokens](ybx-tokens/) for lending or borrowing, and these tokens can be [escrowed](escrowing.md) and then used to make and vote on protocol updates and changes.

## What's a YBX token?

[YBX](ybx-tokens/) is YieldBlox's platform token. It is issued to those who use the protocol, and can be [escrowed](escrowing.md) to propose and vote on [governance](governance.md) proposals that modify the protocol.

## Are there risks when using YieldBlox?

Using any application involves risk. There are four main risks user's should consider when using YieldBlox.

**Smart Contract Risk**

YieldBlox functions using smart contracts. If a bug was discovered and exploited it could result in loss of user funds. To mitigate this risk, the YieldBlox Protocol is currently seeking third-party audits, and will have a bug bounty to further ensure security.

**Turret Protocol Risk**

Yieldblox's smart contracts are built using the Stellar Turret's protocol. If a vulnerability was discovered in Turrets it could result in loss of user funds. More information on turret risks and an audit of the turret's protocol can be found on the [Stellar Turrets website](https://turrets.stellar.org).

**Malicious Turret Host Collusion**

The Stellar Turret's protocol functions by uploading a smart contract to a set of turret's hosted by trusted organizations in the Stellar ecosystem. Each of these hosts creates a unique signing keypair that is associated with the smart contract. The protocol associated with the uploaded smart contract then adds these keypairs as signers to the protocol accounts that must be controlled by the smart contract using whatever signature structure they deem appropriate. When a user runs the contract by sending a request to a turret the turret builds and signs a Stellar transaction XDR based on the smart contract and returns the XDR and signature to the user. The user then attaches as many signatures as necessary to reach the protocol account's [signing threshold](https://developers.stellar.org/docs/glossary/multisig/#thresholds) to one of the returned XDRs and submits it to the network.

The catch is that turret signing keys can sign transactions without the smart contract being ran. The smart contract is more of an instruction set for turret coordination rather than a strict rule set. Therefore, if turret hosts were to become malicious, they could collude to sign malicious transactions. More information on this risk can be found on the [Stellar Turrets website](https://turrets.stellar.org). YieldBlox mitigates this risk by only using turrets hosted by trustworthy ecosystem organizations and by requiring the majority of turrets to sign a transaction before it can be accepted by the network. Furthermore, the YieldBlox governance system can replace a turret on short notice should the turret become unreliable. More details on the Turrets supporting the YieldBlox protocol can be found in the developer docs section.

**Stellar Decentralized Ledger Risk**

As with all decentralized ledgers Stellar comes with its unique set of risks. You can read more about the Stellar Consensus Protocol and it's risks [here](https://developers.stellar.org/docs/glossary/scp/).

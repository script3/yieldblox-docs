# General

![](<../.gitbook/assets/general header.svg>)

## What is YieldBlox?

YieldBlox is a decentralized finance (DeFi) protocol for lending and borrowing built on [Stellar](https://www.stellar.org). Users carry out all protocol functions using YieldBlox's smart contracts hosted on [Stellar Turrets](https://tss.stellar.org). These can be accessed either directly using API calls, or through a front-end such as the YieldBlox web app.

## What is a decentralized finance protocol?

A decentralized finance protocol is a financial application that does not rely on or require its users to trust a central intermediary. This is often achieved by building the protocol using immutable smart contracts that run on a distributed network. In YieldBlox's case, it operates using smart contracts built with the Stellar Turret smart contract engine. There is no central organization that controls YieldBlox and no organization that YieldBlox relies on to continue operating. This means that YieldBlox is non-custodial, trust-minimized, and censorship-resistant.

## What is unique about YieldBlox?

The DeFi money market landscape has become very competitive. There are a variety of money market protocols built on programmable blockchains like Ethereum and Solana. Nevertheless, YieldBlox has made several improvements on existing money market protocol models and created a unique offering.

**Platform Focus**

Stellar is a unique blockchain in that it's an ideal backend for fintech platforms. It's easy for a small team to spin up a mobile application and plug into the Stellar network to provide their users with payment and trading capabilities. YieldBlox was built with these platforms in mind. Platforms can use YieldBlox to provide their users with lending and borrowing tools without reducing the decentralization of their platform. In addition, platforms can leverage YieldBlox's unique tokenomics model and isolated lending markets to bootstrap growth of their own platform, ease anchor adoption, and build a non-custodial revenue model.

**High Capital Efficiency**

Capital efficiency is crucial for any money market protocol. The most straightforward way to do so is by increasing asset loan-to-value ratios. However, this comes with an increased risk of underwater positions. YieldBlox's [Default Protection](lending-borrowing/default-protection.md) mechanism greatly reduces the risk that underwater positions pose, allowing the protocol to sustain high loan-to-value ratios.

**Unique Tokenomics**

Tokenomics, when designed correctly, can be an invaluable tool for a DeFi protocol. YBX, YieldBlox's utility token utilizes a [five-level tokenomics model](ybx-tokens/ybx-tokenomics.md) that touches every portion of the protocol.

**Built on Stellar**

YieldBlox is the first DeFi protocol built on Stellar. Stellar is an excellent platform for DeFi protocols with extremely fast transactions, low fees, and an ecosystem that is well equipped to tokenize real-world currencies and assets. Additionally, Stellar's focus on developing countries means YieldBlox will be able to serve a user base that has traditionally been hard for DeFi protocols to tap into.

## What are the benefits of YieldBlox?

YieldBlox brings a decentralized, on-ledger money market to the Stellar ecosystem.\
Within the ecosystem, this promises to:

- Increase and trading payment liquidity
- Improve capital productivity
- Reduce reliance on lending intermediaries like banks
- Serve a global market with a cost of less than $0.01 per transaction

## How do I use YieldBlox?

YieldBlox maintains a [web app](https://testnet.yieldblox.finance) that allows users to interact with the protocol.

The web app currently supports the following wallets:

- \***\*[**Freighter\*\*](https://www.freighter.app)
- \***\*[**Albedo\*\*](https://albedo.link)

As other interfaces begin to integrate YieldBlox, we will do out best to keep a list of integrations here!

---

More technical users can also use YieldBlox directly through the Turret network that supports it. Please see the [Stellar Turrets documentation](https://turrets.stellar.org/) for more info about this.

## Does YieldBlox have fees?

While they are very small, YieldBlox does have two types of fees:

**Network Fees**

YieldBlox users must pay [Stellar Network fees](https://developers.stellar.org/docs/glossary/fees/) and Stellar Turret fees for each transaction. Both of these fees are extremely low. We expect them to amount to less than one cent (< $0.01) per transaction.

**Interest Rates**

Borrowers on YieldBlox must pay [interest fees](lending-borrowing/interest-rates.md) to lenders. These fluctuate based on demand.

## Can YieldBlox be changed or upgraded?

Yes. The YieldBlox protocol can be changed or updated using its [governance](governance.md) model.

## How does governance work?

The YieldBlox protocol is updated and maintained using a [governance](governance.md) token model. Users receive [YBX tokens](ybx-tokens/) for lending or borrowing, and these tokens can be [escrowed](escrowing.md) and then used to make and vote on protocol updates and changes.

## What's a YBX token?

[YBX](ybx-tokens/) is YieldBlox's platform token. It is issued to those who use the protocol, and it can be [escrowed](escrowing.md) to earn a portion of protocol revenue and propose and vote on [governance](governance.md) proposals to modify the protocol.

## Are there risks when using YieldBlox?

Every application ever created has some risk. With YieldBlox, the risks are smart contract and liquidation related. A smart contract vulnerability would be a bug in the protocol code. The risk of liquidation is user-specific and an intended function of the protocol. To mitigate risks, our team has taken every imaginable step to ensure the security of our protocol. The YieldBlox protocol is currently seeking third-party audits, and will have a bug bounty to further ensure security.

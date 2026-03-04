**What is Exchange Mode?**

Exchange Mode is a MiCAR-compliant selective-disclosure mechanism built directly into the QRing protocol that allows Tier-1 centralized exchanges (Binance, Coinbase, Kraken, etc.) to satisfy Article 76(3) of the EU Markets in Crypto-Assets Regulation (MiCAR) while preserving the full anonymity and quantum-resistant privacy of the decentralized peer-to-peer network.

MiCAR Article 76(3) explicitly prohibits crypto-asset service providers (CASPs) from listing or trading any asset that has “inbuilt anonymisation functions” unless the exchange can definitively identify token holders and reconstruct historical transaction data for AML/CTF oversight. Legacy privacy coins (Monero, Zcash) were delisted in 2025 precisely because they offered no such pathway. QRing solves this with a mathematically precise middle ground: exchanges receive cryptographic tools that give them perfect visibility into their own custodial wallets only; every other wallet on the network remains completely opaque and unlinkable.

### **How Exchange Mode Works – The Four Core Compliance Mechanisms**

1. **Selective Disclosure via View Keys** Exchanges are issued dedicated cryptographic view keys tied exclusively to the stealth addresses of their internal custodial hot/cold wallets. These keys are standard Monero-style view keys but upgraded to Kyber768 (ML-KEM) under Carrot addressing. With the view key, the exchange’s compliance engine can decrypt and scan every incoming and outgoing transaction that touches its own custodial outputs. It sees exact amounts, timestamps, and origin/destination stealth addresses for its own users — exactly what regulators require — without ever gaining any visibility into non-custodial wallets.  
2. **Cryptographic View Tags (1-byte filter)** Every transaction payload on QRing carries a 1-byte view tag (SHAKE-128 truncation of the shared secret). Custodial wallets scan the entire chain in milliseconds, discarding 99.6 % of irrelevant transactions before any expensive decapsulation. This gives exchanges high-throughput, real-time monitoring of their own flows with negligible compute cost, enabling automated AML reporting and Travel Rule compliance.  
3. **Spend-Authority Proofs (embedded in Carrot)** Carrot — QRing’s quantum-resistant addressing layer — includes specialized zero-knowledge spend-authority proofs. When a user deposits to an exchange, the deposit transaction carries a succinct proof (generated at spend time) that the funds originated from a legitimate, user-controlled output under the exchange’s view key. These proofs are constant-size, aggregable, and verifiable in milliseconds. They give the exchange mathematical evidence (verifiable by regulators) that the funds are not forged or laundered, while revealing nothing about the sender’s other transactions or historical activity.  
4. **Custodial Onboarding APIs \+ LACT+ Tagging** Standardized APIs interface directly with the LACT+ aggregator. During KYC onboarding, the exchange cryptographically binds a user’s real-world identity to the specific ephemeral outputs deposited into its custodial wallet. Because LACT+ commitments are aggregable and prunable, the exchange can prove the entire deposit/withdrawal history of any single KYC’d user without exposing the broader anonymity set.

### **Why Carrot Makes This Possible Without Breaking Privacy**

Carrot is the quantum-resistant addressing and migration protocol that replaces Monero’s dual-key stealth addresses. It provides:

* unconditional forward secrecy for change outputs,  
* switch commitments for the 12-month migration epoch (legacy ECC → Module-LWE),  
* and native support for spend-authority proofs.

These proofs are generated only when spending to a custodial address that has been granted a view key. The proof is embedded in the LACT+ activity proof (49 bytes) and is visible only to the holder of the corresponding view key. No other participant — not even other nodes — can extract any information. Carrot’s design therefore acts as a cryptographic “opt-in” toggle: normal users never generate or attach these proofs, so their wallets remain fully anonymous; only exchange-controlled wallets receive the extra metadata required by MiCAR.

### **How Anonymity of Private Wallets Remains Uncompromised**

* View keys are issued per custodial wallet only — never to the broader network.  
* Private users who never deposit to or withdraw from a CEX never interact with Exchange Mode at all; their transactions contain no spend-authority proofs and are filtered out by view tags.  
* The peer-to-peer network continues to use full MatRiCT+ / FCMP++ ring signatures over 100+ million historical outputs, LACT+ aggregation, and Lantern range proofs. No backdoors, no global deanonymization, no mandatory KYC.  
* Even for users who do interact with an exchange, only the specific deposit/withdrawal flows linked to that exchange’s view key are visible; the rest of their transaction graph remains hidden behind the same quantum-resistant anonymity set as everyone else.

This is mathematically identical to the selective-disclosure model that enabled Salvium (SAL) to secure its 2026 EU listings via an independent Gunnercooke legal opinion. QRing simply implements the same architecture at the protocol level, with the added benefit of post-quantum security.

### **Why This Is Directly Relevant to MiCAR Compliance**

MiCAR does not ban privacy coins outright; it bans them only when exchanges cannot perform the required oversight. By giving CASPs:

* view-key decryption of their own custodial flows,  
* spend-authority proofs for origin verification,  
* and KYC-bound output tagging via LACT+,

QRing allows exchanges to satisfy every clause of Article 76(3) while the decentralized P2P layer remains 100 % private. Regulators receive exactly the data they need (custodial transaction history \+ mathematical proofs of legitimacy) without forcing global deanonymization. This is why Exchange Mode is presented in every QRing whitepaper and listing strategy document as the explicit pathway to Tier-1 liquidity.

In short, Exchange Mode is not a privacy compromise — it is a precision-engineered compliance layer that lives only in custodial interfaces, powered by Carrot’s spend-authority proofs, and designed from day one to unlock regulated exchange listings without touching the anonymity guarantees that make QRing valuable.


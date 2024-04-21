# Proposal for a Solana NFT Launchpad, Marketplace, and Collectors platform.

## 1. Introduction
Project Keep introduces a Solana-based NFT launchpad and marketplace designed to facilitate the creation, minting, and lifecycle management of NFTs that securely store encrypted data. These NFTs will feature unique mechanisms where data is encrypted upon minting and can only be decrypted by the NFT's owner.

## 2. Objectives
- **To Develop a User-Friendly Platform:** Simplifying the creation and management of encrypted data NFTs for creators with varying levels of technical expertise.
- **To Enhance NFT Data Security:** Utilizing Solana’s blockchain capabilities to ensure secure, tamper-proof encryption and storage of sensitive data within NFTs.
- **To Inspire New Novel NFT Usecases:** Our NFT platform aims empower NFTs and NFT creators with unique and innovative features.
- **To Implement Controlled Data Access:** Ensuring that the encrypted data can be accessed only by its owner, and sometimes under specific conditions.

## 3. Technical Framework
### Blockchain Platform: Solana
Rationale: We're choosing to develop Solona as our first supported network for its high throughput, low cost, and fast transaction finality, which are ideal for deploying interactive and high-frequency applications like NFTs.

### Smart Contracts:
**Language:** Rust, for robust and secure Solana smart contracts.
**Features:**
- **Minting Function:** Handles the encryption of input data and the initial creation of the NFT.
- **Trading Function:** Facilitates ownership transfer.
- **Decommission Function:** Designed to decrypt the data for owner retrieval while disabling any further transactions of the NFT to ensure data exclusivity and prevent duplication.
- **Transfer Hooks:** To enforce checks and validations during transfers, ensuring all transactions are secure and intended.

### Encryption/Decryption Mechanism:
**Technology:** Asymmetric cryptography, where the private key for decryption is securely generated and stored, and the public key is embedded within the NFT for encryption.
**Decommissioning Process:** On executing the decommission command, the smart contract utilizes the private key to decrypt the data, making it accessible to the NFT owner, while simultaneously altering the NFT’s trade status to prevent future transactions.

### Data Storage:
**On-chain:** Storing minimal data like references and hashes to ensure transactional integrity and security.
**Off-chain:** Utilizing decentralized storage solutions (e.g., Arweave or IPFS) for storing larger data securely, linked via hashes to the NFTs for verification.

### User Interface:
**Components:** Interfaces for uploading data, minting NFTs, viewing owned NFTs, and decommissioning NFTs to access data.
**Interactivity:** Features to preview encrypted data (in hashed form), manage NFT transactions, and retrieve data post-decommission.

## 4. Unique NFT Features

Below are the key differentiators of our NFTs:

### Unique NFT Features

1. **Private Data Encryption and Safe Access:**
   - Our NFTS allow for encrypted content that can only be accessed by the NFT owner. 

2. **Controlled Data Decommissioning:**
   - Decommissioning disables further NFT transactions, allowing data retrieval while protecting exclusivity.

3. **Standardized JSON For Interoperability:**
   - **Accepting Valid JSON:** Our platform accepts well-structured JSON files to mint NFTs, which allows for the standardization of displays across various marketplaces. This JSON can include metadata that describes the NFT’s content, value, and other details crucial for transparency and usability across platforms.
   - **Robust templating engine:** Different NFTs may require different json structures. Our platform will aim to permit user-created templates as well as use community-published templates.
   - **Standardized NFT JSON data combined structured under templates can offer rich display for NFTs. A platform stretch goal would be to allow displays to also be customized based on expected data contained within the NFT.**

4. **Minting controls for mining multiple NFTs at one time:**
   - **Selective Hiding:** When mining multiple NFTs, the platform will support a variety of features that allow control over how often and where secret contents might be attached.

## 5. Benefits
- Enhanced Security: By leveraging asymmetric encryption, Project Keep ensures that all data embedded within NFTs is protected against unauthorized access throughout its lifecycle.
- Market Flexibility: Using standardized JSON for NFT metadata ensures that NFTs minted on Project Keep are compatible with multiple marketplaces, increasing their liquidity and market potential.
- Innovative Utility: Using NFTs to securely and privately transfer important data.

## 6. Monetization Strategy
Project Keep will implement several revenue-generating mechanisms:
- Fees to Mint: Structure: A fee for every NFT minted on the platform. Rate: (N) SOL per NFT
- Fees on Trades: Structure: A transaction fee for each NFT trade on the secondary market. Rate: 5% of the transaction value
- Fees to Decommission: Structure: A fee to execute the decommission function, which includes data decryption and disabling further trading of the NFT. Rate: (N) SOL

## 7. Phases of Development

1. **Proof of Concept**
   - Basic smart contract development for minting and decommissioning encrypted NFTs; initial encryption tests.

2. **MVP Development**
   - Full smart contract suite development, dynamic key management, UI development, integration with Solana testnet for testing.

3. **Platform Launch**
   - Mainnet deployment, initial user acquisition, marketing campaign initiation.

4. **Expansion and Scaling**
   - Addition of complex features, continuous platform optimization, partnerships development.

## 8. Risk Assessment

- **Security Risks**: Advanced cryptographic practices, regular security audits.
- **Regulatory Risks**: Adapting to blockchain regulations, especially those impacting data privacy, disclosure, and asset registration.
- **Adoption Risks**: Marketing strategies, community engagement, and extensive user education.

## 9. Example User Journeys

### Jonesy’s NFT Adventure

Jonesy, a digital artist, creates an artwork featuring Peely, the playful banana character which Jonsey would like to sell as an NFT on the open market to one of his fans.

This NFT not only includes an original artwork, it also includes a hidden section only accessible only to the NFT owner, filled with exclusive sketches and notes about Peely’s creation. In addition to the additional one-of-a-kind sketches, Jonesy also has added a special coupon for 10,000 V-Bucks (valued at approximately $80) within the NFT to enhance its value as a gift.

Through Project Keep, Jonsey will have the option to sell 100 of these NFTs to his biggest fans so they can keep it in their collections.

### A Brand New Car

A major car manufacturer has minted a magazine into an NFT that goes over their latest model luxury vehicle. Inside this magazine, they have videos of the car, interviews with designers and engineers, and for one lucky purchaser of the Magazine NFT, a certificate redeemable for one of the first 100 vehicles being currently produced.

400 NFTs of the magazine were minted and offered to shareholders and all 400 were purchased within 24 hours with one lucky NFT holder having the secret code attached to their NFT.

## 10. Encryption and Decryption Flow

We were unsuccessful in finding a method for transferring private keys without the assistance of a 3rd party custodial service. For this reason, every NFT minted on the platform that contains encrypted data will have the private key required for reading the data, stored securely on the platform while only being accessible to the NFT holder.

Until a more trustless solution is discovered, this is to be seen as a proprietary feature of the platform. It also will go to say that from a security standpoint, we cannot supply full trustless custody to our NFTs, and the security of their contents will be limited to the trust provided in the platform itself, which would work hard to assure the confidence of its customers through audits and when possible, open source frameworks.

There may be at some later point an API provided by the platform to third-party NFT marketplaces and strategic partners to decrypt and display the contents of an NFT remotely, given ownership is verifiable. This would be a late-stage implementation and assumes we are not able to solve the custody issue related to private keys.

Here’s an example of how our minting, encryption, and decryption setup works:

### Detailed Implementation Steps:

1. **Initial Setup**:
   - **Minting by Jonesy**:
     - The platform generates a unique public-private key pair for the NFT (\(PK_{NFT}\), \(SK_{NFT}\)).
     - Jonesy encrypts the NFT content (\(C_{enc}\)) with the NFT’s public key (\(PK_{NFT}\)).
     - Store \(C_{enc}\) on the blockchain or off-chain securely linked to the NFT.
     - The platform securely stores the corresponding private key (\(SK_{NFT}\)) on the platform server, ensuring it can only be accessed by the NFT owner.

2. **Ownership and Access Management**:
   - The platform controls access to the private key (\(SK_{NFT}\)) through an access control system that verifies NFT ownership via the blockchain.
   - When an NFT is purchased and ownership is transferred, the platform’s system recognizes the new owner based on the transaction recorded on the blockchain.
   - The platform allows the new owner to retrieve the private key (\(SK_{NFT}\)) in a secure manner, enabling them to decrypt the content (\(C_{enc}\)) locally.

3. **Transfer of Ownership**:
   - When the NFT is sold, the blockchain records the transaction and updates the owner’s address.
   - The platform’s access control system ensures that only the current owner, as recorded on the blockchain, can request and retrieve the NFT’s private key (\(SK_{NFT}\)).

4. **Decommissioning (Optional)**:
   - If an NFT is decommissioned in order to reveal its hidden contents, then the smart contract marks the NFT as decommissioned on the blockchain, which prevents further transfer and the platform will allow the decryption of the content.

## 11. Conclusion

Project Keep is designed to be a cutting-edge Solana-based NFT launchpad that not only facilitates the minting of NFTs but also incorporates robust data encryption mechanisms that protect user data until the point of intentional decommissioning, enhancing user control over privacy and content usage.


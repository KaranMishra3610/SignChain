# SignChain – Blockchain-Based OTP Replacement for Fintech Transactions

## Problem

Traditional OTPs (One-Time Passwords) used in financial transactions are:

- Susceptible to phishing, SIM swaps, and malware
- Rely on centralized infrastructure (SMS/email gateways)
- Frequently delayed or lost
- Lacking cryptographic proof of user consent

As high-value digital transactions increase, reliance on insecure OTP systems puts users at serious risk.

## Solution

**SignChain** replaces OTPs with cryptographic digital signatures verified on the Ethereum blockchain.

Instead of receiving an OTP, the user signs a transaction ID using MetaMask. The signature is verified both off-chain (via Ethers.js) and on-chain (via a Solidity smart contract using `ecrecover`).

This approach is:

- Decentralized
- Cryptographically verifiable
- Resistant to phishing, SIM swap, and interception
- Fast and seamless for the user

## How It Works

1. **User enters mock transaction details on the frontend**
2. MetaMask prompts the user to sign the transaction ID (txId)
3. Signature is generated using the user’s private key
4. Frontend sends txId, signature, and address to the backend API
5. Backend verifies the signature off-chain using Ethers.js
6. If valid:
   - Data is saved to MongoDB
   - Signature is sent to the smart contract
7. Smart contract uses `ecrecover` to verify the signer
8. Smart contract returns the result to the backend
9. If invalid, backend responds with an error

### Workflow Diagram

<img width="1814" height="962" alt="hackvortex" src="https://github.com/user-attachments/assets/328c8485-fdd0-42aa-9108-b62559d99fe5" />


## Tech Stack

| Layer           | Technologies                        |
|----------------|-------------------------------------|
| Smart Contract  | Solidity, Hardhat (local testnet)  |
| Wallet          | MetaMask                           |
| Frontend        | React.js, Ethers.js                |
| Backend         | Node.js (Express)                  |
| Database        | MongoDB                            |
| Blockchain      | Ethereum (EVM-compatible)          |

## Features

- OTP-less transaction authorization
- MetaMask signature-based signing
- Smart contract signature verification
- MongoDB-backed transaction logs
- Modular architecture (frontend, backend, contract separated)

## Demo Video

- [YouTube](https://youtu.be/jbMd7GewVb4)

## Use Cases

- Online banking approval flows
- Secure login / MFA replacement
- Fintech apps requiring signature-level control
- E-commerce checkout validation

## Security Benefits

- No reliance on OTP or centralized services
- Resistant to SIM-swaps, phishing, MITM attacks
- Signature stays within the user’s MetaMask wallet
- Full transparency with smart contract enforcement

## Local Setup
git clone https://github.com/KaranMishra3610/SignChain
cd SignChain

Start Frontend
cd client
npm install
npm run dev

Start Backend (in a separate terminal)
cd ../backend
npm install
node server.js
Start MongoDB
Ensure MongoDB is running locally (default port: 27017).

Deploy Smart Contract on Local Hardhat Network (with 20 Test Accounts)
cd ../contracts
npm install
npx hardhat node
This starts a local Ethereum testnet with 20 unlocked, pre-funded test accounts.

In a new terminal, deploy the smart contract:
npx hardhat run scripts/deploy.js --network localhost

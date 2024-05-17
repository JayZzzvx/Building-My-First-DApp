# Building-My-First-DApp

# Token Vesting DApp

## Overview

The Token Vesting DApp allows organizations to create and manage vesting schedules for their tokens. This application is particularly useful for web3 organizations that need to allocate tokens to different stakeholders (e.g., community, investors, pre-sale buyers, founders) with specific vesting periods. The DApp ensures that stakeholders can only claim their tokens after the vesting period has elapsed.

## Features

- Organization Registration: Organizations can register themselves and their ERC20 token.
- Stakeholder Management: Organizations can add stakeholders, specifying the amount of tokens and the vesting period.
- Whitelisting: Organizations can whitelist addresses for different types of stakeholders.
- Token Claiming: Whitelisted stakeholders can claim their tokens once the vesting period is over.

## Tech Stack

- Smart Contracts: Solidity
- Front End: React.js
- Blockchain Interaction: Ether.js
- Deployment: Testnet (e.g., Rinkeby, Ropsten)

## Setup Instructions

### Prerequisites

- Node.js
- npm or yarn
- MetaMask extension for browser
- Testnet ETH for deployment and testing

### Smart Contract Deployment

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/token-vesting-dapp.git
   cd token-vesting-dapp
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Deploy the smart contract using Remix or Hardhat. For Hardhat, follow these steps:

   - Initialize a Hardhat project (if not already done):

     ```bash
     npx hardhat
     ```

   - Compile the smart contract:

     ```bash
     npx hardhat compile
     ```

   - Deploy the contract:

     Create a deployment script (`scripts/deploy.js`):

     ```javascript
     async function main() {
         const OrganizationRegistry = await ethers.getContractFactory("OrganizationRegistry");
         const organizationRegistry = await OrganizationRegistry.deploy();
         await organizationRegistry.deployed();
         console.log("OrganizationRegistry deployed to:", organizationRegistry.address);
     }

     main().catch((error) => {
         console.error(error);
         process.exitCode = 1;
     });
     ```

     Run the deployment script:

     ```bash
     npx hardhat run scripts/deploy.js --network rinkeby
     ```

4. Note down the deployed contract address and update the front-end configuration with this address.

### Front-End Setup

1. Update the contract ABI and address in the React app:

   - Copy the ABI from `artifacts/contracts/OrganizationRegistry.sol/OrganizationRegistry.json` to `src/OrganizationRegistryABI.json`.
   - Update the contract address in `src/AdminPage.js` and `src/UserPage.js`.

2. Start the React application:

   ```bash
   npm start
   ```

3. Open the application in your browser at `http://localhost:3000`.

## Usage Guide

### Connecting Wallet

1. Open the application and connect your MetaMask wallet by clicking the "Connect Wallet" button.

### Admin Functionality

1. Navigate to the "Admin Page".
2. **Register Organization**:
   - Enter the organization address and ERC20 token address.
   - Click "Register" to register the organization.
3. **Add Stakeholder**:
   - Enter the stakeholder type (e.g., "investor").
   - Enter the stakeholder's address.
   - Specify the amount of tokens and the release time.
   - Click "Add Stakeholder" to add the stakeholder with the vesting schedule.

### User Functionality

1. Navigate to the "User Page".
2. **Claim Tokens**:
   - Enter the organization address and stakeholder type.
   - Click "Claim Tokens" to claim the tokens if the vesting period has passed.


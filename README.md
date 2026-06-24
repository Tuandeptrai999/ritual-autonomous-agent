# HomoMimic - Autonomous Sovereign Agent on Ritual Testnet

This repository contains the smart contracts and deployment scripts for **HomoMimic**, an autonomous AI agent deployed on the Ritual testnet.

## Overview
HomoMimic uses the Ritual Sovereign Agent precompile (`0x080C`) to run a recurring execution loop. Driven by on-chain scheduling, the agent wakes up, runs a `See -> Think -> Do` inference loop inside a Trusted Execution Environment (TEE), and delivers its actions back on-chain.

### Key Components
- **`src/HomoMimic.sol`**: The main Solidity smart contract. It handles the scheduling logic, funds the `RitualWallet` for execution fees, and processes Phase 2 asynchronous deliveries from the agent.
- **`deploy-and-start.js`**: A comprehensive deployment script that:
  - Discovers an active TEE executor.
  - Deploys the `HomoMimic` contract.
  - Funds the RitualWallet.
  - ABI-encodes the Sovereign Agent payload (including ECIES-encrypted LLM API keys).
  - Stores the request on-chain.
  - Starts the autonomous scheduler loop.
- **`compile.js`**: Script to compile the Solidity contracts using `solc`.

## On-Chain Information
The agent is actively running on the Ritual Testnet:
- **Contract Address**: `0x9581a0f1710E42643393e9f1cDd9709447c21656`
- **Schedule ID**: `#2727541` (Wakes up every 500 blocks, approx 3 minutes)
- **Model**: `gemini-2.5-flash`

## Setup & Deployment

1. Install dependencies:
   ```bash
   npm install
   ```

2. Create a `.env` file in the root directory:
   ```env
   PRIVATE_KEY=your_private_key_here
   RITUAL_RPC_URL=https://rpc.ritualfoundation.org
   GEMINI_API_KEY=your_gemini_api_key_here # Or OPENAI_API_KEY / ANTHROPIC_API_KEY
   ```

3. Compile the contracts:
   ```bash
   node compile.js
   ```

4. Deploy and start the agent:
   ```bash
   node deploy-and-start.js
   ```

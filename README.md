Meta README for SwoopPon: Liquidity Rewards System


Repo Link: https://github.com/DeluxeRaph/SwoopPon




📝 Project Summary

SwoopPon is a smart contract system integrated with Uniswap V4 that rewards liquidity providers by minting SwoopPon tokens for swaps and offering fee discounts to high-balance users. The system includes a dynamic fee adjustment mechanism and leverages Chainlink oracles for price feeds.

⸻

📚 Documentation Structure

Primary README

The primary README.md provides:
	•	Project Overview: High-level description of SwoopPon’s functionality and use cases.
	•	Contract Breakdown: Details of the two core contracts—SwoopPon.sol and TokenVault.sol.
	•	How It Works: Explanation of earning mechanisms and fee adjustments.
	•	Prerequisites: Requirements for using and deploying the system.
	•	Usage Guide: Step-by-step instructions for deploying contracts and interacting with the system.
	•	Hook Details: Technical insights into hook logic (beforeSwap, afterSwap), conditional logic, and flags.
	•	Deployment Instructions: Commands to deploy contracts via Foundry.

⸻

📂 Folder Structure

SwoopPon/
├── contracts/               # Solidity contracts
│   ├── SwoopPon.sol         # Uniswap V4 hook contract
│   └── TokenVault.sol       # Token balance management contract
├── images/                  # Diagrams and flowcharts
├── script/                  # Deployment scripts
├── test/                    # Test cases for contracts
├── README.md                # Main project documentation
└── foundry.toml             # Foundry configuration



⸻

⚡ Key Insights

🎯 Goal of the System

The primary objective is to incentivize liquidity provision by issuing SwoopPon tokens and offering fee discounts to high-value contributors.

🔁 Hook Points and Conditional Logic
	•	Hook Name: ZeroFeeConditionalHook
	•	beforeSwap: Checks if the swapper has deposited tokens to determine fee behavior.
	•	afterSwap: Mints reward tokens if swap fees exceed a predefined threshold.

⸻

🧠 Design Philosophy

✅ Incentivizing Liquidity Providers
	•	Users accumulate SwoopPon tokens through swaps, encouraging consistent interaction.
	•	Fee waivers apply for users with significant token holdings, fostering long-term liquidity provision.

📊 Dynamic Fee Model
	•	Fees are adjusted dynamically based on vault balances and swap conditions.
	•	Chainlink price oracles ensure accuracy in evaluating ETH and BTC values.

⸻

🛠️ Setup and Configuration

1. Install Dependencies

Ensure Foundry is installed:

curl -L https://foundry.paradigm.xyz | bash
foundryup

2. Deploy Contracts

Run the deployment script:

forge script script/Deploy.s.sol:DeployScript --rpc-url <your_rpc_url> --private-key <your_private_key>



⸻

🧩 Advanced Usage
	•	Custom Fee Configuration: Use setFee() to modify base fees dynamically.
	•	Admin Withdrawal Rights: Vault owners can withdraw deposited tokens.

🔍 Additional Documentation
	•	Uniswap V4 Hook Documentation
	•	Foundry Documentation
	•	Chainlink Price Feeds

⸻

📜 License

This project is licensed under the ISC License.

🚀 Contribution Guidelines

Contributions are welcome! Please submit a pull request with detailed explanations for improvements.


Meta README: Swoupon Tokenomics Calculation Library

Tokenomics: https://github.com/derekmeegan/swoupon_tokenomics

This meta README provides an overview and context for the Swoupon Tokenomics Calculation Library, highlighting its architecture, mathematical foundation, and integration points.

⸻

📚 Project Summary

Swoupon is a tokenomics framework designed to create a sustainable liquidity pool rewards system that incentivizes swappers in decentralized exchanges (DEXs). The system dynamically calculates fees and rewards using fixed-point arithmetic, ensuring on-chain efficiency and economic sustainability.

⸻

🚀 Core Concepts
	1.	Dynamic Fee System:
	•	Swappers pay a fee (TR) that decreases as swap volume increases.
	•	Higher volume transactions benefit from lower fees, promoting larger swaps.
	2.	Swoupon Rewards:
	•	Users receive Swoupons (TI tokens) when paying with regular fees.
	•	Swoupons can be redeemed to offset future swap fees, creating a self-sustaining cycle.
	3.	Reward Cycle Mechanics:
	•	New Swoupons are only issued when fees are paid in regular tokens, preventing dilution.
	4.	Volume-Dependent Adaptation:
	•	The system adapts fee and reward structures dynamically based on market conditions.

⸻

🧠 Mathematical Model Overview

1. Fee Factor Calculation (F(V)):
	•	Fee decreases exponentially with increasing swap volume (V):
F(V) = 0.01 + (0.02 \cdot e^{-0.00005 \cdot V})
	•	Ranges from 0.03 at zero volume to 0.01 at high volume.

2. Swap Cost (TR(V)):
	•	Fees calculated for a swap of volume V:
TR(V) = \frac{F(V) \cdot V}{0.1}

3. Potential Swoupon Reward (potential\_TI(V)):
	•	Rewards increase sub-linearly with swap volume:
potential\_TI(V) = \frac{(1 + V)^{0.3}}{0.1}
	•	Solidity approximates this using $\sqrt{1+V}$ for efficiency.

4. Final Swoupon Reward (TI(V)):
	•	Capped at one-third of the fees collected to ensure sustainability:
TI(V) = \min(potential\_TI(V), \frac{TR(V)}{3})

⸻

⚡️ Technical Architecture

🎯 Solidity Implementation:
	•	Core logic in CalcLib.sol with:
	•	Fee and reward calculation functions
	•	Fixed-point constants using ABDKMath64x64
	•	Efficient min/max operations for reward capping

🐍 Python Reference Implementation:
	•	Provides equivalent calculations in python/swoupon_calc.py for:
	•	Simulations
	•	Verifications
	•	Exact formula-based models

🔬 Testing & Verification:
	•	Hardhat tests ensure:
	•	Accurate function behavior
	•	Consistency with Python model results
	•	Precision in edge cases

⸻

📊 Visualization and Insights
	•	Visualization charts (./assets/charts.png) showcase:
	•	Fee (TR) and reward (TI) behavior across varying swap volumes.
	•	Reward caps and volume scaling effects.

⸻

🛠️ Development Workflow

💡 Setup:

npm install

🔎 Compile:

npx hardhat compile

✅ Testing:

npx hardhat test



⸻

🔗 Integration Guide
	1.	Import Library:
	•	Include CalcLib.sol in the smart contract.
	2.	Fee & Reward Calculation:
	•	Use provided functions to calculate fees and Swoupon rewards.
	3.	ABDKMath64x64 Integration:
	•	Ensure the contract imports ABDKMath64x64 for fixed-point operations.

⸻

📄 License
	•	MIT License: Permits free usage, modification, and distribution.
	•	Disclaimer: Provided “as-is” without warranty or liability.

⸻

📢 Future Enhancements
	•	Gas Optimization: Further reduce on-chain computational costs.
	•	Adaptive Rewards: Implement more complex incentive structures.
	•	Governance Parameters: Introduce configurable parameters for flexibility.

⸻

📝 Conclusion

The Swoupon Tokenomics Calculation Library balances economic incentives with long-term sustainability. It leverages efficient Solidity implementation and fixed-point precision to ensure seamless integration into DEX protocols while rewarding loyal users through a sustainable feedback loop.

App Repo: https://github.com/nolanmak/swoupon/

Meta README: SwouponApp

The SwouponApp is a decentralized application (dApp) built with Vite, React, and Moralis, enabling users to connect their wallets, view blockchain data, and manage their token balances and NFTs in a responsive, user-friendly interface. This meta README provides a high-level overview of the application, its architecture, features, and usage.

⸻

📚 Overview

SwouponApp empowers users by providing an intuitive interface to explore their blockchain assets, with seamless wallet integration and real-time data updates powered by Moralis APIs.

🔥 Core Capabilities:
	•	Wallet Connection: Secure MetaMask integration for connecting wallets.
	•	Token Balances: View native (ETH) and ERC-20 token balances.
	•	NFT Collection: Explore NFT assets associated with the connected wallet.
	•	Responsive UI: Optimized for mobile, tablet, and desktop devices.

⸻

🚀 Key Technologies

Frontend:
	•	React: Component-based UI development.
	•	Vite: Lightning-fast build and development environment.
	•	react-router-dom: Navigation and routing.

Backend:
	•	Express: Node.js backend for API handling.
	•	Moralis API: Fetch blockchain data using the Moralis API.
	•	dotenv: Manage sensitive API keys and environment variables.
	•	cors: Enable secure cross-origin requests.

⸻

🗂️ Project Structure Overview

SwouponApp/
├── public/              # Static assets (HTML, icons)
├── src/                 # Main application source code
│   ├── components/      # Reusable UI components
│   ├── pages/           # Page-level components (Dashboard, NFTs, etc.)
│   ├── App.jsx          # Main application component
│   ├── main.jsx         # Application entry point
│   └── index.css        # Global CSS styles
├── server.js            # Express server to connect with Moralis APIs
├── .env                 # Environment variables (API key, etc.)
├── vite.config.js       # Vite configuration for build and development
└── package.json         # Project dependencies and scripts



⸻

⚡️ Setup & Installation

Prerequisites:
	•	Node.js v14+ (Ensure you have Node.js installed)
	•	npm or yarn (Package manager)
	•	Moralis API Key (Sign up at Moralis to get an API key)

📦 Installation:
	1.	Clone the repository:

git clone https://github.com/your-username/SwouponApp.git
cd SwouponApp


	2.	Install dependencies:

npm install


	3.	Configure environment variables:
	•	Create a .env file in the root directory
	•	Add your Moralis API key:

MORALIS_API_KEY=your_moralis_api_key_here



⸻

🛠️ Usage & Development

Run in Development Mode:
	1.	Start the backend server:

node server.js


	2.	Launch the Vite development server:

npm run dev


	3.	Open the application in your browser:

http://localhost:3000



Build for Production:

To create a production-ready build:

npm run build

The production files will be located in the dist directory.

⸻

🎮 Using SwouponApp
	1.	Connect Wallet: Click “Connect Wallet” to link MetaMask.
	2.	Dashboard Navigation: Access token balances, NFTs, and more.
	3.	Refresh Data: Click “Refresh Data” to fetch the latest blockchain data.

⸻

⚙️ API & Backend Logic

Moralis API Integration
	•	Authentication: Wallets connect securely via MetaMask.
	•	Data Retrieval: Native and ERC-20 token balances, NFT collections, and wallet activity.

Express Backend
	•	API Middleware: Fetches and formats blockchain data.
	•	CORS Handling: Allows secure cross-origin communication.

⸻

🧪 Testing
	•	Manual Testing: Check wallet connection, token balances, and NFT display.
	•	API Validation: Validate backend responses for accuracy and consistency.

⸻

🔗 Integration Guidelines

To integrate SwouponApp with other projects:
	1.	Import API Endpoints: Use Express backend endpoints to fetch blockchain data.
	2.	Component Usage: Leverage modular React components for consistent UI.

⸻

📜 License

ISC License
Permission is granted to use, modify, and distribute the software with appropriate attribution.

⸻

🔮 Future Enhancements
	•	Multi-wallet support
	•	Cross-chain token balances and NFTs
	•	Enhanced analytics and historical data tracking
	•	UI improvements with TailwindCSS integration

⸻

🎉 Conclusion

SwouponApp delivers a seamless, decentralized user experience that empowers users to interact with their blockchain assets effortlessly. With a scalable backend and modular React frontend, the app is well-positioned for future upgrades and feature additions.

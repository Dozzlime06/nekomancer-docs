---
cover: .gitbook/assets/banner.png
coverY: 0
---

# Nekomancer DEX Documentation

<figure><img src=".gitbook/assets/banner.png" alt="Nekomancer Banner"><figcaption></figcaption></figure>

## Overview

Nekomancer is a decentralized exchange (DEX) swap aggregator built on **Monad Mainnet (Chain 143)**. It routes trades through multiple DEXes to find the best prices, collects platform fees, and features a referral system with claimable earnings.

---

## Table of Contents

1. [Features](#features)
2. [Smart Contracts](#smart-contracts)
3. [How Swapping Works](#how-swapping-works)
4. [Fee Structure](#fee-structure)
5. [Referral System](#referral-system)
6. [Staking (Coming Soon)](#staking)
7. [API Endpoints](#api-endpoints)
8. [Supported DEXes](#supported-dexes)
9. [Token Support](#token-support)

---

## Features

- **Multi-DEX Routing**: Automatically finds the best price across Uniswap V2, Uniswap V3, PancakeSwap V2, and Nad.Fun
- **Split Routing**: Large trades can be split across multiple DEXes for better execution
- **1% Platform Fee**: Transparent fee with clear distribution
- **Referral Program**: Earn 20% of fees from users you refer
- **Claimable Earnings**: Referral earnings deposited to vault for claiming anytime
- **On-Chain Transparency**: All swaps and fees recorded on Monad blockchain

---

## Smart Contracts

### SwapAggregator (Main Contract)
| Property | Value |
|----------|-------|
| Proxy Address | `0x6524822e437dcd23d62c77496d7a0ac980fbc81d` |
| Implementation | `0x19332B438Da14Ac5537d499d7e279f45C8A476c6` |
| Type | UUPS Upgradeable |
| Network | Monad Mainnet (Chain 143) |

**Functions:**
- `swapMONForTokens(tokenOut, minOut, deadline, useV3, v3Fee)` - Buy tokens with MON
- `swapTokensForMON(tokenIn, amountIn, minOut, deadline, useV3, v3Fee)` - Sell tokens for MON
- `swapMONForTokensWithReferral(tokenOut, minOut, deadline, v3Fee, referrer)` - Buy with referral
- `swapTokensForMONWithReferral(tokenIn, amountIn, minOut, deadline, v3Fee, referrer)` - Sell with referral
- `nadFunBuy(token, minOut, deadline, v3Fee)` - Buy Nad.Fun tokens
- `nadFunSell(token, amountIn, minOut, deadline, v3Fee)` - Sell Nad.Fun tokens
- `nadFunBuyWithReferral(...)` - Buy Nad.Fun with referral
- `nadFunSellWithReferral(...)` - Sell Nad.Fun with referral

### ReferralVault V2
| Property | Value |
|----------|-------|
| Proxy Address | `0x28e123cfd53EA9B39BCec297eba161F0742764F2` |
| Implementation | `0x141e636B8601e40c74f02b17114FB54A5030E706` |
| Minimum Claim | ~$10 USD in MON |

**Functions:**
- `claim()` - Claim all pending earnings
- `claimAmount(amount)` - Claim specific amount
- `getReferrerStats(address)` - Get pending, claimed, and referral count

### StakingVault (Awaiting MANCER Token)
| Property | Value |
|----------|-------|
| Proxy Address | `0x448317114cf3017fb8e2686c000b70c6a75735dc` |
| Status | Deployed, awaiting token |

---

## How Swapping Works

### 1. User Initiates Swap
User selects tokens and amount on the swap interface.

### 2. Pathfinder Finds Best Route
The backend queries all DEXes to find:
- Best single-DEX route
- Potential split routes for large trades
- V2 vs V3 pool comparisons

### 3. Transaction Execution
1. User approves token (for sells)
2. User confirms swap transaction
3. Contract executes swap through optimal route
4. 1% fee deducted and distributed
5. User receives tokens

### 4. Fee Distribution
Fees are automatically distributed:
- 30% → Platform wallet
- 20% → Referral vault (if referrer exists) or Platform
- 50% → Staking rewards

---

## Fee Structure

| Component | Percentage | Description |
|-----------|------------|-------------|
| Total Fee | 1% | Deducted from each swap |
| Platform | 30% of fee | Operations & development |
| Referral | 20% of fee | Claimable by referrer |
| Staking | 50% of fee | Distributed to stakers |

**Example:**
- Swap: 100 MON → Token
- Fee: 1 MON (1%)
- Platform receives: 0.3 MON
- Referrer receives: 0.2 MON (claimable)
- Staking pool: 0.5 MON

---

## Referral System

### How It Works

1. **Generate Your Code**
   - Go to `/referral` page
   - Connect wallet
   - Click "Generate Referral Code"
   - You get a unique 8-character code (e.g., `NEKOZM3J`)

2. **Share Your Link**
   ```
   https://nekomancer-dex.vercel.app/swap?ref=YOUR_CODE
   ```

3. **Earn From Referrals**
   - When someone uses your link and swaps
   - You earn 20% of the 1% fee
   - Earnings deposited to ReferralVault

4. **Claim Earnings**
   - Go to `/referral` page
   - View your claimable balance
   - Click "Claim Earnings" (minimum ~$10 USD worth)

### Referral Stats
- **Referrals**: Number of unique wallets that swapped using your code
- **Total Earned**: Lifetime earnings in MON
- **Claimable**: Current balance available to claim

---

## Staking

> **Status: Coming Soon** - Awaiting MANCER token deployment

### Planned Features
- Minimum stake: 100,000 MANCER tokens
- Unstake delay: 3 days (request → wait → withdraw)
- Emergency unstake: 20% burned, immediate withdrawal
- Rewards: 50% of all swap fees distributed to stakers

---

## API Endpoints

### Token Discovery
```
GET /api/tokens
```
Returns list of all supported tokens with prices.

### Pathfinder (Best Route)
```
POST /api/swap/pathfinder
Body: {
  "tokenIn": "0x...",
  "tokenOut": "0x...",
  "amountIn": "1000000000000000000"
}
```
Returns best single-DEX route with quote.

### Multi-Hop Routing
```
POST /api/swap/multihop
Body: {
  "tokenIn": "0x...",
  "tokenOut": "0x...",
  "amountIn": "1000000000000000000"
}
```
Returns best route including multi-hop options.

### Referral Lookup
```
GET /api/referral/lookup?code=NEKOZM3J
```
Returns referrer wallet address for a code.

### Referral Stats
```
GET /api/referral/stats?wallet=0x...
```
Returns referral code, count, earnings for a wallet.

---

## Supported DEXes

| DEX | Type | Router Address |
|-----|------|----------------|
| Uniswap V2 | AMM | `0x4B2ab38DBF28D31D467aA8993f6c2585981D6804` |
| Uniswap V3 | Concentrated Liquidity | `0xfE31F71C1b106EAc32F1A19239c9a9A72ddfb900` |
| PancakeSwap V2 | AMM | `0xB1Bc24c34e88f7D43D5923034E3a14B24DaACfF9` |
| Nad.Fun Bonding | Bonding Curve | `0x6F6B8F1a20703309951a5127c45B49b1CD981A22` |
| Nad.Fun DEX | Graduated Tokens | `0x0B79d71AE99528D1dB24A4148b5f4F865cc2b137` |

---

## Token Support

### Native Token
- **MON** - Monad native token (gas & swaps)

### Wrapped Token
- **WMON** - `0x3bd359C1119dA7Da1D913D1C4D2B7c461115433A`

### Popular Tokens
| Token | Address |
|-------|---------|
| WETH | `0xEE8c0E9f1BFFb4Eb878d8f15f368A02a35481242` |
| USDC | `0x754704Bc059F8C67012fEd69BC8A327a5aafb603` |
| CHOG | `0x350035555E10d9AfAF1566AaebfCeD5BA6C27777` |
| SHMON | `0x1B68626dCa36c7fE922fD2d55E4f631d962dE19c` |

### Nad.Fun Tokens
All Nad.Fun tokens are automatically supported:
- **Unbonded**: Traded via Bonding Router
- **Graduated**: Traded via DEX Router with V3 fallback

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Frontend | React, Tailwind CSS, Framer Motion |
| Backend | Express.js, Node.js |
| Blockchain | Viem, Monad RPC |
| Database | PostgreSQL (Neon) |
| Auth | Privy Wallet Connection |
| Contracts | Solidity 0.8.24, OpenZeppelin Upgradeable |
| Deployment | Vercel |

---

## Links

- **App**: [nekomancer.fun](https://www.nekomancer.fun)
- **Monad Explorer**: [monvision.io](https://monvision.io)

---

## Security

- All contracts are UUPS upgradeable for bug fixes
- Owner-only admin functions
- NonReentrant guards on all swap functions
- SafeERC20 for token transfers
- On-chain fee distribution (no custody)

---

*Last updated: November 29, 2025*

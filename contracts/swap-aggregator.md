# SwapAggregator

The main smart contract that handles all token swaps on Nekomancer.

## Overview

SwapAggregator is a UUPS upgradeable contract that:
- Routes swaps through multiple DEXes
- Collects and distributes platform fees
- Integrates with ReferralVault for referral tracking
- Supports V2 AMMs, V3 concentrated liquidity, and Nad.Fun

## Contract Details

| Property | Value |
|----------|-------|
| Proxy | `0x6524822e437dcd23d62c77496d7a0ac980fbc81d` |
| Implementation | `0x19332B438Da14Ac5537d499d7e279f45C8A476c6` |
| Network | Monad Mainnet (Chain 143) |
| Solidity | 0.8.24 |

## Functions

### Swap Functions (Standard)

#### swapMONForTokens
```solidity
function swapMONForTokens(
    address tokenOut,
    uint256 minOut,
    uint256 deadline,
    bool useV3,
    uint24 v3Fee
) external payable returns (uint256)
```
Buy tokens with MON.

#### swapTokensForMON
```solidity
function swapTokensForMON(
    address tokenIn,
    uint256 amountIn,
    uint256 minOut,
    uint256 deadline,
    bool useV3,
    uint24 v3Fee
) external returns (uint256)
```
Sell tokens for MON.

### Swap Functions (With Referral)

#### swapMONForTokensWithReferral
```solidity
function swapMONForTokensWithReferral(
    address tokenOut,
    uint256 minOut,
    uint256 deadline,
    uint24 v3Fee,
    address referrer
) external payable returns (uint256)
```
Buy tokens with referral tracking.

#### swapTokensForMONWithReferral
```solidity
function swapTokensForMONWithReferral(
    address tokenIn,
    uint256 amountIn,
    uint256 minOut,
    uint256 deadline,
    uint24 v3Fee,
    address referrer
) external returns (uint256)
```
Sell tokens with referral tracking.

### Nad.Fun Functions

#### nadFunBuy
```solidity
function nadFunBuy(
    address token,
    uint256 minOut,
    uint256 deadline,
    uint24 v3Fee
) external payable returns (uint256)
```
Buy Nad.Fun tokens. Automatically routes to bonding curve or DEX.

#### nadFunSell
```solidity
function nadFunSell(
    address token,
    uint256 amountIn,
    uint256 minOut,
    uint256 deadline,
    uint24 v3Fee
) external returns (uint256)
```
Sell Nad.Fun tokens.

#### nadFunBuyWithReferral / nadFunSellWithReferral
Same as above but with referral tracking.

### View Functions

#### feeBps
```solidity
function feeBps() external view returns (uint256)
```
Returns current fee in basis points (100 = 1%).

#### platformRecipient
```solidity
function platformRecipient() external view returns (address)
```
Returns platform fee recipient address.

#### stakingRecipient
```solidity
function stakingRecipient() external view returns (address)
```
Returns staking vault address.

#### referralVault
```solidity
function referralVault() external view returns (address)
```
Returns referral vault address.

## Fee Distribution

### With Referrer
| Recipient | Share |
|-----------|-------|
| Platform | 30% |
| Referrer (via vault) | 20% |
| Staking | 50% |

### Without Referrer
| Recipient | Share |
|-----------|-------|
| Platform | 50% |
| Staking | 50% |

## Events

```solidity
event SwapExecuted(
    address indexed user,
    address tokenIn,
    address tokenOut,
    uint256 amountIn,
    uint256 amountOut,
    uint256 fee,
    string dex
);

event FeesDistributedWithReferral(
    uint256 platform,
    uint256 referral,
    uint256 staking,
    address referrer
);

event FeesDistributed(
    uint256 platform,
    uint256 staking
);
```

## Security Features

- **ReentrancyGuard**: Prevents reentrancy attacks
- **SafeERC20**: Safe token transfers
- **UUPS Upgradeable**: Owner-controlled upgrades
- **Slippage Protection**: Minimum output enforcement

## Admin Functions (Owner Only)

```solidity
function setFee(uint256 _bps) external onlyOwner
function setRecipients(address _platform, address _staking) external onlyOwner
function setReferralVault(address _vault) external onlyOwner
```

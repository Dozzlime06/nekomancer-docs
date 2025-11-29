# ReferralVault

Smart contract that stores and distributes referral earnings.

## Overview

ReferralVault V2 is a UUPS upgradeable contract that:
- Receives referral fees from SwapAggregator
- Tracks earnings per referrer
- Allows referrers to claim their MON earnings
- Enforces minimum claim amounts

## Contract Details

| Property | Value |
|----------|-------|
| Proxy | `0x28e123cfd53EA9B39BCec297eba161F0742764F2` |
| Implementation | `0x141e636B8601e40c74f02b17114FB54A5030E706` |
| Network | Monad Mainnet (Chain 143) |
| Minimum Claim | ~$10 USD in MON |

## How It Works

### 1. Fee Deposit
When a swap occurs with a referrer:
1. SwapAggregator calculates 20% referral share
2. Calls `deposit(referrer, swapper)` with MON
3. Vault credits referrer's pending balance

### 2. Balance Tracking
The vault tracks for each referrer:
- `pending`: Unclaimed MON earnings
- `claimed`: Total MON already claimed
- `referralCount`: Number of unique swappers

### 3. Claiming
Referrers can claim when:
- Pending balance >= minimum claim amount
- Minimum is ~$10 USD worth of MON

## Functions

### User Functions

#### claim
```solidity
function claim() external
```
Claim all pending earnings. Requires balance >= minClaimAmount.

#### claimAmount
```solidity
function claimAmount(uint256 amount) external
```
Claim specific amount. Amount must be >= minClaimAmount.

### View Functions

#### getReferrerStats
```solidity
function getReferrerStats(address referrer) external view returns (
    uint256 pending,
    uint256 claimed,
    uint256 referralCount
)
```
Get complete stats for a referrer.

#### minClaimAmount
```solidity
function minClaimAmount() external view returns (uint256)
```
Current minimum claim amount in MON wei.

#### pendingBalance
```solidity
function pendingBalance(address referrer) external view returns (uint256)
```
Get pending balance for a referrer.

### Depositor Functions

#### deposit
```solidity
function deposit(address referrer, address swapper) external payable
```
Deposit referral fee. Only callable by authorized depositors (SwapAggregator).

### Admin Functions (Owner Only)

#### setMinClaimAmount
```solidity
function setMinClaimAmount(uint256 amount) external onlyOwner
```
Update minimum claim amount.

#### setDepositor
```solidity
function setDepositor(address depositor, bool authorized) external onlyOwner
```
Authorize or revoke depositor addresses.

#### emergencyWithdraw
```solidity
function emergencyWithdraw(address to, uint256 amount) external onlyOwner
```
Emergency fund recovery.

## Events

```solidity
event ReferralDeposited(
    address indexed referrer,
    address indexed swapper,
    uint256 amount
);

event ReferralClaimed(
    address indexed referrer,
    uint256 amount
);

event MinClaimAmountUpdated(
    uint256 oldAmount,
    uint256 newAmount
);
```

## Integration

### From SwapAggregator
```solidity
// In _distributeFeesWithReferral
IReferralVault(referralVault).deposit{value: referralShare}(referrer, swapper);
```

### From Frontend
```javascript
// Check stats
const stats = await contract.getReferrerStats(walletAddress);
console.log('Pending:', formatEther(stats.pending));

// Claim earnings
const tx = await contract.claim();
await tx.wait();
```

## Security

- Only authorized depositors can add funds
- Reentrancy protection on claims
- Owner-controlled minimum amounts
- Emergency withdrawal for stuck funds

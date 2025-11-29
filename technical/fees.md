# Fee Structure

Transparent fee breakdown for all Nekomancer swaps.

## Platform Fee

| Component | Amount |
|-----------|--------|
| Total Fee | 1% of swap amount |
| Collected In | MON (native token) |
| Applied To | All swaps except wrap/unwrap |

## Fee Distribution

### With Referrer
When swap uses a referral link:

| Recipient | Share | Amount per 1 MON fee |
|-----------|-------|---------------------|
| Platform | 30% | 0.3 MON |
| Referrer | 20% | 0.2 MON |
| Staking | 50% | 0.5 MON |

### Without Referrer
When no referral link is used:

| Recipient | Share | Amount per 1 MON fee |
|-----------|-------|---------------------|
| Platform | 50% | 0.5 MON |
| Staking | 50% | 0.5 MON |

## Fee Calculation

### Buy (MON → Token)
```
Input: 100 MON
Fee: 1 MON (1%)
Swap Amount: 99 MON
You Receive: ~99 MON worth of tokens
```

### Sell (Token → MON)
```
Sell: 100 tokens
Swap Output: 50 MON (example)
Fee: 0.5 MON (1%)
You Receive: 49.5 MON
```

## Fee-Free Operations

The following have NO platform fee:
- MON → WMON (wrap)
- WMON → MON (unwrap)
- Failed transactions (gas only)

## Gas Fees

Separate from platform fees:

| Operation | Typical Gas |
|-----------|-------------|
| Simple swap | ~0.001 MON |
| Multi-hop | ~0.002 MON |
| Token approval | ~0.0005 MON |

Gas is paid to Monad validators, not Nekomancer.

## Fee Recipients

### Platform
**Address**: `0xE9059B5f1C60ecf9C1F07ac2bBa148A75394f56e`

Used for:
- Development
- Operations
- Marketing
- Infrastructure

### Staking Vault
**Address**: `0x448317114cf3017fb8e2686c000b70c6a75735dc`

Used for:
- Rewards to MANCER stakers
- Accumulates until claimed

### Referral Vault
**Address**: `0x28e123cfd53EA9B39BCec297eba161F0742764F2`

Used for:
- Claimable referral earnings
- Tracks per-referrer balances

## Example Calculations

### Example 1: 1000 MON Buy (No Referrer)
```
Input: 1000 MON
Fee: 10 MON (1%)
├── Platform: 5 MON (50%)
└── Staking: 5 MON (50%)
Swap: 990 MON → Tokens
```

### Example 2: 1000 MON Buy (With Referrer)
```
Input: 1000 MON
Fee: 10 MON (1%)
├── Platform: 3 MON (30%)
├── Referrer: 2 MON (20%)
└── Staking: 5 MON (50%)
Swap: 990 MON → Tokens
```

### Example 3: Sell 10,000 CHOG (With Referrer)
```
Sell: 10,000 CHOG
Swap Output: 100 MON
Fee: 1 MON (1%)
├── Platform: 0.3 MON
├── Referrer: 0.2 MON
└── Staking: 0.5 MON
You Receive: 99 MON
```

## Comparing to Other DEXes

| Platform | Fee |
|----------|-----|
| Nekomancer | 1% (includes routing) |
| Uniswap V2 | 0.3% (LP only) |
| Uniswap V3 | 0.01-1% (LP only) |
| 1inch | Variable |

Note: DEX fees are LP fees. Nekomancer's 1% is on top of DEX fees but includes:
- Best price routing
- Split order execution
- Referral rewards
- Staking rewards

## On-Chain Verification

All fees are visible on-chain:
1. Go to [monvision.io](https://monvision.io)
2. Search your transaction hash
3. View "Internal Transactions" tab
4. See fee distribution transfers

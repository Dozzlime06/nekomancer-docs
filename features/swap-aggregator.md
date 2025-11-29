# Swap Aggregator

Nekomancer's swap aggregator finds the best prices across multiple DEXes on Monad.

## How It Works

### 1. Quote Discovery
When you enter a swap, our pathfinder queries all supported DEXes:
- Uniswap V2
- Uniswap V3 (multiple fee tiers: 0.01%, 0.05%, 0.3%, 1%)
- PancakeSwap V2
- Nad.Fun (for meme tokens)

### 2. Route Optimization
The algorithm compares:
- Direct routes (Token A → Token B)
- Routes through WMON (Token A → WMON → Token B)
- V2 vs V3 pools
- Different V3 fee tiers

### 3. Split Routing
For large trades, we may split across multiple DEXes:
- 60% through Uniswap V3
- 40% through PancakeSwap V2

This reduces price impact and gets you more tokens.

### 4. Execution
The smart contract executes your swap through the optimal route:
- Atomic execution (all or nothing)
- Slippage protection
- MEV-resistant

## Supported Swap Types

### MON → Token
Buy any supported token with MON.

### Token → MON
Sell any supported token for MON.

### Token → Token
Swap between any two tokens (routes through MON/WMON).

### Wrap/Unwrap
- MON → WMON (wrap)
- WMON → MON (unwrap)
- No fees on wrap/unwrap

## Nad.Fun Integration

Nekomancer fully supports Nad.Fun tokens:

### Unbonded Tokens
- Traded on Nad.Fun's bonding curve
- Direct routing to Nad.Fun Bonding Router

### Graduated Tokens
- Tokens that have "graduated" to DEX liquidity
- Routed through Nad.Fun DEX Router or V3 pools
- We compare prices and use the best route

## Fee Structure

| Component | Amount |
|-----------|--------|
| Platform Fee | 1% per swap |
| Gas Fee | Paid in MON (very low on Monad) |

Fee distribution:
- 30% → Platform operations
- 20% → Referrer (if using referral link)
- 50% → Staking rewards

## Smart Contract

The SwapAggregatorV32 contract handles all swaps:

| Property | Value |
|----------|-------|
| Address | `0x6524822e437dcd23d62c77496d7a0ac980fbc81d` |
| Type | UUPS Upgradeable Proxy |
| Network | Monad Mainnet (Chain 143) |

## Best Practices

1. **Check Price Impact**: High impact means you're moving the market
2. **Use Appropriate Slippage**: 0.5% for stable pairs, 1-2% for volatile
3. **Verify Amounts**: Always check the output before confirming
4. **Start Small**: Test with small amounts first

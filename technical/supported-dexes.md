# Supported DEXes

Nekomancer routes trades through multiple decentralized exchanges on Monad.

## DEX Overview

| DEX | Type | Best For |
|-----|------|----------|
| Uniswap V2 | AMM | Standard swaps |
| Uniswap V3 | Concentrated Liquidity | Large trades, stablecoin pairs |
| PancakeSwap V2 | AMM | Alternative liquidity |
| Nad.Fun | Bonding Curve / DEX | Meme tokens |

## Uniswap V2

**Type**: Automated Market Maker (AMM)

**Router**: `0x4B2ab38DBF28D31D467aA8993f6c2585981D6804`

**How It Works**:
- Constant product formula: x * y = k
- 0.3% LP fee per swap
- Simple and gas-efficient

**Best For**:
- Standard token swaps
- Medium-sized trades
- Tokens without V3 pools

## Uniswap V3

**Type**: Concentrated Liquidity AMM

**Router**: `0xfE31F71C1b106EAc32F1A19239c9a9A72ddfb900`
**Quoter**: `0x661E93cca42AfacB172121EF892830cA3b70F08d`
**Factory**: `0x961235a9020B05C44DF1026D956D1F4D78014276`

**Fee Tiers**:
| Fee | Typical Use |
|-----|-------------|
| 0.01% (100) | Stablecoin pairs |
| 0.05% (500) | Correlated pairs |
| 0.30% (3000) | Most pairs |
| 1.00% (10000) | Exotic pairs |

**How It Works**:
- LPs concentrate liquidity in price ranges
- Better capital efficiency
- Multiple fee tiers per pair

**Best For**:
- Large trades
- Major token pairs (WMON/WETH, WMON/USDC)
- Getting best prices

## PancakeSwap V2

**Type**: AMM (Uniswap V2 fork)

**Router**: `0xB1Bc24c34e88f7D43D5923034E3a14B24DaACfF9`

**How It Works**:
- Same as Uniswap V2
- Different liquidity pools
- May have better prices for some pairs

**Best For**:
- Alternative to Uniswap V2
- Tokens with PCS-only liquidity

## Nad.Fun

**Type**: Bonding Curve + DEX

**Contracts**:
| Contract | Address |
|----------|---------|
| Lens | `0x7e78A8DE94f21804F7a17F4E8BF9EC2c872187ea` |
| Bonding Router | `0x6F6B8F1a20703309951a5127c45B49b1CD981A22` |
| DEX Router | `0x0B79d71AE99528D1dB24A4148b5f4F865cc2b137` |

**Token States**:

### Unbonded Tokens
- New tokens on bonding curve
- Price increases with buys
- Uses Bonding Router

### Graduated Tokens
- Tokens that reached graduation threshold
- Liquidity moved to DEX
- Uses DEX Router or V3 pools

**How It Works**:
1. Query Lens to check if token is graduated
2. If unbonded → route to Bonding Router
3. If graduated → compare DEX Router vs V3
4. Execute through best route

**Best For**:
- Meme tokens
- New token launches
- Nad.Fun ecosystem tokens

## Route Selection

Our pathfinder queries all DEXes and selects the best route:

```
1. Get quotes from all DEXes
2. Compare output amounts
3. Consider gas costs
4. Select optimal route
5. For large trades, consider splitting
```

### Split Routing
Large trades may be split across DEXes:
```
1000 MON swap:
- 60% via Uniswap V3 (better price, deeper liquidity)
- 40% via Uniswap V2 (additional liquidity)
= Better overall execution
```

## Adding New DEXes

The aggregator is upgradeable. New DEXes can be added via:
1. Deploy new implementation
2. Upgrade proxy contract
3. New routes available immediately

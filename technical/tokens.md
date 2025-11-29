# Token Support

Nekomancer supports all ERC-20 tokens on Monad with liquidity on supported DEXes.

## Native Token

### MON
| Property | Value |
|----------|-------|
| Symbol | MON |
| Name | Monad |
| Decimals | 18 |
| Type | Native gas token |

MON is used for:
- Gas fees
- Swap input/output
- Referral earnings
- Staking rewards

## Wrapped MON

### WMON
| Property | Value |
|----------|-------|
| Address | `0x3bd359C1119dA7Da1D913D1C4D2B7c461115433A` |
| Symbol | WMON |
| Name | Wrapped MON |
| Decimals | 18 |

WMON is the ERC-20 wrapped version of MON, used for:
- DEX liquidity pools
- Smart contract interactions
- V3 swaps

**Note**: MON ↔ WMON wrapping is free (no platform fee).

## Major Tokens

### WETH
| Property | Value |
|----------|-------|
| Address | `0xEE8c0E9f1BFFb4Eb878d8f15f368A02a35481242` |
| Symbol | WETH |
| Name | Wrapped Ether |
| Decimals | 18 |

### USDC
| Property | Value |
|----------|-------|
| Address | `0x754704Bc059F8C67012fEd69BC8A327a5aafb603` |
| Symbol | USDC |
| Name | USD Coin |
| Decimals | 6 |

## Popular Tokens

| Token | Symbol | Address |
|-------|--------|---------|
| Chog | CHOG | `0x350035555E10d9AfAF1566AaebfCeD5BA6C27777` |
| ShMonad | SHMON | `0x1B68626dCa36c7fE922fD2d55E4f631d962dE19c` |
| Mobots | BOTS | `0x4bEdf5d792DAb4BfeF048d86af4404228DF3F3fb` |
| Anago | ANAGO | `0x99aE2DC76c43979E3BcC0ae8d69F1fca077c8888` |
| Unit | UNIT | `0x788571E0E5067Adea87e6BA22a2b738fFDf48888` |
| Gmonad | GMONAD | `0x1f80C65cC2c37Af84ABbe1ea03183A624a6F8888` |

## Nad.Fun Tokens

All tokens launched on Nad.Fun are automatically supported:
- Query via Nad.Fun Lens
- Route through appropriate router
- Full buy/sell support

## Custom Token Import

Users can import any ERC-20 token by address:

1. Paste token address in search
2. Token info is fetched automatically
3. Swap if liquidity exists

**Warning**: Always verify token addresses. Scam tokens may use similar names.

## Token Discovery

The platform automatically discovers tokens from:
- Known trading pairs
- V3 pool events
- Nad.Fun token list
- User imports

## Price Feeds

Token prices are derived from:
1. V3 pool reserves (primary)
2. V2 pool reserves (fallback)
3. WMON as base pair

All prices shown in USD, calculated via:
```
Token Price = Token/WMON rate × WMON/USD rate
```

## Adding Liquidity

To add a new token:
1. Deploy ERC-20 on Monad
2. Create liquidity pool on any supported DEX
3. Token becomes swappable via Nekomancer

Minimum recommended liquidity: ~$1,000 USD equivalent

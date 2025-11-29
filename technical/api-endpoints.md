# API Endpoints

Nekomancer provides several API endpoints for frontend integration.

## Base URL

**Production**: `https://www.nekomancer.fun/api`

## Endpoints

### GET /api/tokens

Returns list of all supported tokens with current prices.

**Response:**
```json
[
  {
    "address": "0xEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE",
    "symbol": "MON",
    "name": "Monad",
    "decimals": 18,
    "logo": "https://...",
    "price": 0.0336,
    "source": "native"
  },
  {
    "address": "0x350035555E10d9AfAF1566AaebfCeD5BA6C27777",
    "symbol": "CHOG",
    "name": "Chog",
    "decimals": 18,
    "logo": "https://...",
    "price": 0.00337
  }
]
```

### POST /api/swap/pathfinder

Find the best route for a swap.

**Request:**
```json
{
  "tokenIn": "0xEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE",
  "tokenOut": "0x350035555E10d9AfAF1566AaebfCeD5BA6C27777",
  "amountIn": "1000000000000000000"
}
```

**Response:**
```json
{
  "success": true,
  "bestRoute": {
    "dex": "uniswap_v3",
    "dexId": 2,
    "amountOut": "297000000000000000000",
    "v3Fee": 3000,
    "priceImpact": "0.15"
  },
  "allQuotes": {
    "uniswap_v2": "295000000000000000000",
    "uniswap_v3_3000": "297000000000000000000",
    "pancakeswap_v2": "294000000000000000000"
  }
}
```

### POST /api/swap/multihop

Find multi-hop routes for token-to-token swaps.

**Request:**
```json
{
  "tokenIn": "0x350035555E10d9AfAF1566AaebfCeD5BA6C27777",
  "tokenOut": "0xEE8c0E9f1BFFb4Eb878d8f15f368A02a35481242",
  "amountIn": "1000000000000000000000"
}
```

**Response:**
```json
{
  "success": true,
  "route": [
    {
      "tokenIn": "CHOG",
      "tokenOut": "WMON",
      "dex": "uniswap_v3",
      "amountOut": "100000000000000000"
    },
    {
      "tokenIn": "WMON",
      "tokenOut": "WETH",
      "dex": "uniswap_v3",
      "amountOut": "33000000000000"
    }
  ],
  "totalOutput": "33000000000000"
}
```

### GET /api/referral/lookup

Lookup referrer wallet from referral code.

**Request:**
```
GET /api/referral/lookup?code=NEKOZM3J
```

**Response:**
```json
{
  "referrerWallet": "0xa2eb6be3bde7e99a8e68e6252e006ced620ff02f"
}
```

### GET /api/referral/stats

Get referral statistics for a wallet.

**Request:**
```
GET /api/referral/stats?wallet=0xa2eb...
```

**Response:**
```json
{
  "code": "NEKOZM3J",
  "referralCount": 5,
  "totalEarnings": "1.5",
  "claimableEarnings": "1.2"
}
```

### POST /api/referral/generate

Generate a new referral code.

**Request:**
```json
{
  "wallet": "0xa2eb6be3bde7e99a8e68e6252e006ced620ff02f"
}
```

**Response:**
```json
{
  "code": "NEKOZM3J",
  "referralLink": "https://www.nekomancer.fun/swap?ref=NEKOZM3J"
}
```

### GET /api/locks/all

Get all token locks (for TokenLocker feature).

**Response:**
```json
[
  {
    "id": 1,
    "token": "0x...",
    "amount": "1000000000000000000000",
    "unlockTime": 1735689600,
    "owner": "0x..."
  }
]
```

## Error Handling

All endpoints return errors in this format:

```json
{
  "success": false,
  "error": "Error message here"
}
```

Common error codes:
- `400`: Bad request (missing parameters)
- `404`: Not found
- `500`: Server error

## Rate Limits

Currently no rate limits. Subject to change as usage grows.

## CORS

All endpoints support CORS from any origin.

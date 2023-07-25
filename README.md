# FXDX Market Information API

### The following documentation provides information about the FXDX Market Information API, which can be used to get price, orderbook, volume, etc.

## Authentication

The following API needs doesn't need any authentication

## Base URL

https://api.optimism.fxdx.exchange/cmc/

## Endpoints

### `GET /contracts`

Endpoint provides a summary of every single contract traded on the exchange. Describes the specification of the contracts, mainly the pricing of the contract and its type (vanilla, inverse, or quanto)

#### Parameters
No query or route parameters.
#### Response

- Response Body Fields

| Name                        | Description                                                                                             |
| --------------------------- | ------------------------------------------------------------------------------------------------------- |
| ticker_id                   | Identifier of a ticker with delimiter to separate base/quote, eg. BTC-PERP, ETH-PERP. |
| base_currency               | Symbol/currency code of base pair, eg. BTC                                                              |
| product_type                | Type of derivative                                                                                      |
| index_name                  | Name of the index asset                                                                                 |
| index_currency              | Index currency used to price the asset                                                                  |
| creation_timestamp             | Start date of derivative                                                                                  |
| contract_type               | Describes the type of contract - Vanilla, Inverse or Quanto                                            |
| contract_price_currency     | Describes the currency which the contract is priced in (e.g. USDT)                       |
| quote_currency              | Symbol/currency code of quote pair, eg. ETH                                                             |
| last_price                  | Last transacted price of base currency based on given quote currency                                    |
| base_volume                 | 24 hour trading volume in BASE currency                                                                 |
| USD_volume                  | 24 hour trading volume in USD                                                                           |
| quote_volume                | 24 hour trading volume in QUOTE currency                                                                |
| bid                         | Current highest bid price                                                                               |
| ask                         | Current lowest ask price                                                                                |
| high                        | Rolling 24-hour highest transaction price                                                               |
| low                         | Rolling 24-hour lowest transaction price                                                                |
| open_interest               | The number of outstanding derivatives contracts that have not been settled                              |
| index_price                 | Last calculated index price for underlying of contract                                                  |
| expiry_timestamp            | End date of derivative                                                                                  |
| funding_rate                | Current funding rate                                                                                    |
| next_funding_rate           | Upcoming predicted funding rate                                                                         |
| next_funding_rate_timestamp | Timestamp of the next funding rate change                                                               |
| open_interest_usd           | The sum of the Open Positions (long or short) in USD Value of the contract                              |

- Example Response:

```json
[
  {
    "ticker_id": "BTC-PERP",
    "base_currency": "BTC",
    "product_type": "Perpetual",
    "index_name": "BTC",
    "index_currency": "USDT",
    "start_timestamp": 1684497600,
    "contract_type": "Inverse",
    "contract_price_currency": "USDT",
    "quote_currency": "USDT",
    "last_price": 29866.981333333337,
    "base_volume": "0.00000000",
    "USD_volume": "0.0",
    "quote_volume": "0.0",
    "bid": "29730.806764864859677701639425572732",
    "ask": "27281.0",
    "high": "30052.844473684213163050129296457728",
    "low": "29741.995853647680330253733298438144",
    "open_interest": "0.0",
    "index_price": 29866.981333333337,
    "expiry_timestamp": 1690006672,
    "funding_rate": "0.0",
    "next_funding_rate": "0.0",
    "next_funding_rate_timestamp": 1690010272,
    "open_interest_usd": "0.0"
  },
  {
    "ticker_id": "ETH-PERP",
    "base_currency": "ETH",
    "product_type": "Perpetual",
    "index_name": "ETH",
    "index_currency": "USDT",
    "start_timestamp": 1684497600,
    "contract_type": "Inverse",
    "contract_price_currency": "USDT",
    "quote_currency": "USDT",
    "last_price": 1892.1208536585366,
    "base_volume": "0.000000000000000000",
    "USD_volume": "0.0",
    "quote_volume": "0.0",
    "bid": "1896.715479999999882145528384386498",
    "ask": "1884.983162820512903769804138438721",
    "high": "1905.200416666666551407246959443968",
    "low": "1884.82716981132105149378491056128",
    "open_interest": "323.551284239999995905474399960063",
    "index_price": 1892.1278048780487,
    "expiry_timestamp": 1690006672,
    "funding_rate": "0.0",
    "next_funding_rate": "0.0",
    "next_funding_rate_timestamp": 1690010273,
    "open_interest_usd": "323.551284239999995905474399960063"
  }
]
```



### `GET /orderbook`

Provide order book information with at least depth = 100 (50 each side) returned for a given market pair/ticker

#### Parameters
- ticker_id (optional)
   Example : /ETH-PERP
#### Response

- Response Body Fields

| Name                        | Description                                                                                             |
| --------------------------- | ------------------------------------------------------------------------------------------------------- |
| timestamp| Unix timestamp in milliseconds for when the last updated time occurred. |
| ticker_id | A pair such as "BTC-PERP", with delimiter between different cryptoassets |
| bids | An array containing 2 elements. The offer price and quantity for each bid order
| asks | An array containing 2 elements. The ask price and quantity for each ask order



- Exmaple Response:

```json
{
    "BTC-PERP": {
        "timestamp": 1690008552045,
        "asks": [
            [
                "29815.386",
                "0.000000000015815744"
            ],
            [
                "26547.206",
                "0.000000000001961091"
            ],
            [
                "26560.257",
                "0.000000000001960367"
            ],
            [
                "26718.743",
                "0.000000000007459862"
            ],
            [
                "26727.423",
                "0.000000000008523767"
            ]
        ],
        "bids": [
            [
                "29804.146",
                "0.000000000015821708"
            ],
            [
                "26546.368",
                "0.000000000001961153"
            ],
            [
                "26717.982",
                "0.000000000008534551"
            ],
            [
                "26727.423",
                "0.000000000008522492"
            ]
        ]
    },
    "ETH-PERP": {
        "timestamp": 1690008552192,
        "asks": [
            [
                "1891.307",
                "1.388607332714487122"
            ],
            [
                "1892.593",
                "1.528974754246448801"
            ],
            [
                "1737.937",
                "0.183765403437229494"
            ],
            [
                "1736.465",
                "0.114888581111626205"
            ]
        ],
        "bids": [
            [
                "1890.714",
                "1.389042852919182116"
            ],
            [
                "1890.595",
                "1.530590590297525"
            ],
            [
                "1899.89",
                "1.466549488641030731"
            ],
            [
                "1737.715",
                "0.183995840185854929"
            ],
            [
                "1736.151",
                "0.183954445179876817"
            ]
        ]
    }
}
```

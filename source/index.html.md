

# Auro Digital API

## Overview

The Auro Digital API employs WebSockets for communication between the front-end and back-end services, allowing real-time data exchange. For developers aiming to programmatically interact with Auro Digital, a direct WebSocket connection to the back-end service can be established.

Please note, this API was initially designed for internal use, primarily for front-end development. Therefore, it may possess some complex payloads. Furthermore, it is subject to potential changes based on the evolving needs of the front-end application.

# Connection Details

## Base URL

Assuming your Auro Digital URL is `https://test.aurodigital.ai/`, your corresponding WebSocket URL would be: `wss://test-backend.aurodigital.ai/v2`.

The backend service adheres to the same IP whitelist policies as the front-end service. If you need to add (static) IP addresses to the whitelist, please contact our support team.

## JSON-RPC Schema


| Name   | Type   | Description |
--------|--------|-------------
|jsonrpc | string | Only "2.0" is supported |
|id      | string | This will be echoed back in responses or subscription payloads|
|method  | string | Establishing the specific API to connect to. Documented below |
|params  | string | Details regarding the specific API call. Documented below     |


# API_GETWAY

## Subscribe_get_pair

Subscribe to a pair. Returns updates on all metrics of that pair on the given exchanges as well as consolidated order books and other metrics across the given exchanges.

```json
{
    "jsonrpc": "2.0",
    "id": "6c1985bf-80ad-4bbc-86d0-6e682cdb764d",
    "method": "subscribe_get_pair",
    "params": {
        "pair": "BTC/USD",
        "exchanges": [
            "coinbasepro"
        ]   
   }
}

```

### Request

Name | Type | Description
--------- | ------- | -----------
pair | string | The normalized symbol.
exchange | array of object | A list of cryptocurrency exchanges to use.

```json
{
    "jsonrpc": "2.0",
    "id": "6c1985bf-80ad-4bbc-86d0-6e682cdb764d",
    "result": {
        "pair": "BTC/USD",
        "exchanges": [
            "coinbasepro"
        ],
        "order_book": {
            "columns": [
                "Price",
                "Size",
                "Exchange"
            ],
            "bids": [
                [
                    32800562.00007545,
                    10897.2,
                    "coinbasepro"
                ],
                [
                    84791055.49007545,
                    10897.1938683967,
                    "coinbasepro"
                ],
                [
                    150392079.09007546,
                    10897.1878189978,
                    "coinbasepro"
                ]
            ],
            "asks": [
                [
                    32798972.124043528,
                    10897.22,
                    "coinbasepro"
                ],
                [
                    84789656.45404352,
                    10897.2261317227,
                    "coinbasepro"
                ],
                [
                    150391041.25404352,
                    10897.2321811358,
                    "coinbasepro"
                ]
            ],
            "commission": 0.0,
            "timestamps": {
                "coinbasepro": 1600246762328
            },
            "done_at": [
                [
                    "fetch_order_book",
                    1600246763260
                ]
            ],
            "time_elapsed_after": [
                [
                    "fetch_order_book",
                    {
                        "coinbasepro": 932
                    }
                ]
            ]
        },
        "other_info": [
            {
                "title": "Liquidity Metrics",
                "columns": [
                    "bid",
                    "ask",
                ],
                "values": [
                    [
                        10897.2,
                        10897.22,
                    ]
                ]
            }
        ],
        "is_inverse": false,
        "time": 1600246763302
    }
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
pair | string | The normalized symbol.
exchange | array of object | A list of cryptocurrency exchanges to use.
order_book | object | A list of cryptocurrency exchanges to use.
-- columns | array of string | Description of the format in bids and asks.
-- bids | array of string or number | Bids aggregated across the specified exchanges.
-- asks | array of string or number | Asks aggregated across the specified exchanges.
-- commission | number | The administrator-defined fee that is applied on the order book prices.
-- timestamps | number | Unix timestamp in milliseconds.
-- done_at | array of string or number | Internal data structure. Please do not rely on this.
-- time_elapsed_after | array of string or number | Internal data structure. Please do not rely on this.
other_info | array of object | Internal data structure. Please do not rely on this.
is_inverse | boolean | Whether this is an inverse futures contract.
time | number | The Unix timestamp (in milliseconds) when the data in this payload is fetched.

## get_tickers
feed of best bid and ask values for a specified crypto pair on the provided Liquidity venue(s).

```json
{
"id": "b1b61f11-d34b-408b-ba46-cd6c1907252b",
"jsonrpc": "2.0",
"method": "get_tickers",
"params": {

    "pair": "ETH/BTC",
    "exchanges": ["okx-new_test"]

    }
}
```

### Request
Name | Type | Description
--------- | ------- | -----------
pair | string | The normalized symbol.
exchange | array of object | A list of cryptocurrency liquidity venue to use.

```json
{
"id": "b1b61f11-d34b-408b-ba46-cd6c1907252b",
"jsonrpc": "2.0",
    "result": {
    "best_bid": {
    "price": 0.06296,
    "size": 86.378417,
    "exchange": "okx-new_test",
    "timestamp": 1691055448
    },
"display_name": "okx-new_test"
    }
}
```

### Request
Name | Type | Description
--------- | ------- | -----------
best_bid | Object | Contains the best bid data.(price,size,exchange,timestamps).
exchange | array of object | A list of cryptocurrency exchanges to use.


## get_all_markets


Use the get_all_markets method to retrieve a list of all available exchanges and trading symbols. Please note, changes in the availability of symbols on the exchanges may not be immediately reflected in the response, so we recommend calling this method periodically.



```json
{
    "jsonrpc": "2.0",
    "id": "22ad7310-b318-4eee-8618-b3c47ca2f225",
    "method": "get_all_markets"
}
```

### Request




```json
{
    "jsonrpc": "2.0",
    "id": "22ad7310-b318-4eee-8618-b3c47ca2f225",
    "result": [
        {
            "type": "SPOT",
            "normalized_symbol": "BTC/USDT",
            "exchange_id": "binance",
            "base": "BTC",
            "quote": "USDT",
            "is_inverse": false
        }
    ]
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
type | string | SPOT or FUTURES.
normalized_symbol | string | The unique identifier for a symbol in Access.
exchange_id | string | The name of the exchange as configured by your administrator.
base | string | The base currency.
quote | string | The quote currency.
is_inverse | boolean | Whether this is an inverse futures contract.

## get_algo_executions

get  all active orders




```json
{
    "jsonrpc": "2.0",
    "id": "c407195b-4c35-483d-93f5-798b391dc710",
    "method": "get_algo_executions",
    "params": {
        "start_time": "2018-09-07T16:00:00.000Z",
        "end_time": "2020-09-07T16:00:00.000Z",
        "filters": [
            {
                "exchange_id": "coinbasepro",
                "normalized_symbol": "BTC/USD"
            }
        ],
        "algos_only": false,
        "status": "ALL"
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
start_time	|timestamp	|A list of cryptocurrency exchanges to use.
end_time|	timestamp|	The amount of the Auro Digital Trading order.
exchange_id	|string	|The price of the Auro Digital Trading order.
normalized_symbol	|string|	Start datetime of algo processing
algo_only|	Boolean|	End datetime of algo processing
status|	string|	Staus of order that we want("OPEN", "CLOSE", "ALL")



```json
{
    "jsonrpc": "2.0",
    "id": "c407195b-4c35-483d-93f5-798b391dc710",
    "result": {
        "executions": [
            {
                "id": 7333,
                "name": null,
                "algo_type": "LMT",
                "status": "CLOSED",
                "data": {
                    "pair": "BTC/USD",
                    "side": "sell",
                    "price": "9150",
                    "volume": "0.01",
                    "end_time": "2020-07-16T08:05:52.785000+00:00",
                    "exchange": "coinbasepro",
                    "start_time": "2020-07-16T07:06:58.104273+00:00",
                    "active_order_path": [
                        "coinbasepro",
                        "21f1206c-60b6-4323-8d99-233ebbe79c45"
                    ],
                    "active_order_amount": "0.01",
                    "canceled_order_paths": []
                },
                "start_time": 1594883218000,
                "end_time": 1594886752000,
                "exchanges": [
                    {
                        "exchange_id": "coinbasepro",
                        "side": "sell"
                    }
                ],
                "pairs": [
                    {
                        "pair": "BTC/USD",
                        "side": "sell"
                    }
                ],
                "side": "sell",
                "price": 9150.0,
                "price_net": 9150.0,
                "volume": 0.01,
                "leg_room": null,
                "slippage": null,
                "filled": 0.01,
                "average": 9156.02,
                "average_net": 9156.02,
                "updated_at": 1594883227000
            }
        ]
    }
}

```

### Response

Name | Type | Description
--------- | ------- | -----------
id	|number|	The ID of the Auro Digital Trading order.
name|	null|	Currently unused field.
algo_type|	string	|Abbreviated order type.
status|	string|	Status of the algo execution.
data|	object|	Internal data structure, please avoid relying on this.
pair	|string|	The normalized symbol.
side	|string	|The side of the trade (buy or sell).
price	|number	|The price of the Auro Digital Trading order.
volume|	number	|The amount of the Auro Digital Trading order.
start_time	|timestamp	|Start datetime of algo processing
end_time	|timestamp	|End datetime of algo processing
exchange	|string	|The name of the exchange as configured by your administrator.
active_order_path	|list|	Currently working orders
active_order_amount	|string	|Amount of those orders
canceled_order_paths|	list	|Orders canceled by this Algorithm
start_time|	number	|Unix timestamp in milliseconds.
end_time|	number or null	|Unix timestamp in milliseconds.
exchange|	array of object|	A list of cryptocurrency exchanges to use.
exchange_id	|string	|The name of the exchange as configured by your administrator.
side|	string	|buy or sell.
pairs	|array of object|	A list of normalized symbols.
pair|	string	|buy or sell.
side|	string	|buy or sell.
price	|number	|The price of the Auro Digital Trading order.
price_net|	number or null	|The price, net of a fixed commission (if configured).
volume|	number	|The amount of the Auro Digital Trading order.
leg_room|	number or null	|Price adjustment before sending an order to the exchange.
slippage|	number or null	|Slippage, if applicable.
filled	|number	|The filled amount of the Auro Digital Trading order.
average|	number	|The average price of the filled amount.
average_net	|number or null	|The average price, net of a fixed commission (if configured).
updated_at|	number	|Unix timestamp in milliseconds.

## place_orders

The place_orders method allows you to place LIMIT orders on an exchange.

A LIMIT order is an order to buy or sell a cryptocurrency at a specific price or better. It allows you to set a precise price at which you want to trade.


```json
{
  "jsonrpc": "2.0",
  "id": "6c44a8f0-8196-40d0-8f39-620710bae10f",
  "method": "place_orders",
  "params": {
    "orders": [
      {
        "pair": "BTC/USD",
        "side": "BUY",
        "price": 1234,
        "volume": 0.01,
        "exchange": "coinbasepro",
        "end_time": "2020-09-10T10:44:02.187Z"
      }
    ]
  }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
pair	|string	|The trading pair, represented as a normalized symbol
side|	string	|Indicates whether you want to "buy" or "sell".
price|	number	|Specifies the price at which you want to execute the order.
volume	|number	|Represents the amount (in base currency) you want to order.
exchange|	string	|The identifier of the exchange where the order will be placed, as configured by your administrator.
end_time	|timestamp	|The time at which the order will expire if not fulfilled.


```json



{
    "jsonrpc": "2.0",
    "id": "6c44a8f0-8196-40d0-8f39-620710bae10f",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result”



## get_balances

get  all balances for the given exchanges.

```json
{
    "jsonrpc": "2.0",
    "id": "6c1985bf-80ad-4bbc-86d0-6e682cdb764d",
    "method": "get_balances",
    "params": {
        "pair": "BTC/USD",
        "exchanges": ["coinbasepro"],
        "from_mid_agg": 0,
        "cutoff": 1
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
pair	|string	|The normalized symbol.
exchanges|	array of object	|A list of cryptocurrency exchanges to use.
from_mid_agg|	number	|Filter for Consolidated Orderbooks
cutoff	|number|	Filter for Consolidated Orderbooks


```json
{
    "jsonrpc": "2.0",
    "id": "6c1985bf-80ad-4bbc-86d0-6e682cdb764d",
    "result": {
        "pair": "BTC/USD",
        "exchanges": ["coinbasepro"],
        "balances": {
            "coinbasepro": {
                "BTC": {
                    "free": 215.52433665,
                    "used": 0,
                    "total": 215.52433665
                },
                "ETH": {
                    "free": 883.80160773,
                    "used": 0,
                    "total": 883.80160773
                },
                "USD": {
                    "free": 363332.4740171202,
                    "used": 0,
                    "total": 363332.4740171202
                },
                "USDC": {
                    "free": 70000.0,
                    "used": 0,
                    "total": 70000.0
                }
            }
        },
        "is_inverse": false,
        "time": 1600246763302
    }
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
pair|	string|	The normalized symbol.
exchanges|	array of object|	A list of cryptocurrency exchanges to use.
balances|	object|	The balances on the exchanges configured by your administrator.
exchange_id (as key)|	object	|The name of the exchange as configured by your administrator.
currency_id (as key)|	object|	The currency ID.
free	|number	|Money available for trading.
used	|number	|Money on hold due to e.g., open orders.
total|	number	|free + used.
is_inverse|	boolean|	Whether this is an inverse futures contract.
time|	number	|The Unix timestamp (in milliseconds) when the data in this payload is fetched.








# DEX APIs
This document outlines the APIs used to fetch quotes and place orders for token swaps on decentralized exchanges (DEX). The supported algorithm type is SWAP, and the response contains information on the price and slippage.

## Base URL

Assuming your Auro Digital URL is `https://test.aurodigital.ai/`, your corresponding WebSocket URL would be: `wss://test-backend.aurodigital.ai/v1`.

The backend service adheres to the same IP whitelist policies as the front-end service. If you need to add (static) IP addresses to the whitelist, please contact our support team.





## JSON-RPC Schema


| Name   | Type   | Description |
--------|--------|-------------
|jsonrpc | string | Only "2.0" is supported |
|id      | string | This will be echoed back in responses or subscription payloads|
|method  | string | Establishing the specific API to connect to. Documented below |
|params  | string | Details regarding the specific API call. Documented below     |

## place_order_pre_processing_dex (Fetch Quotes)

This API is used to fetch token swap quotes for a given trading pair.



```json
{
    "id": "595d4d5a-fb97-4577-9a0d-edcee13a5e5e",
    "jsonrpc": "2.0",
    "method": "place_order_pre_processing_dex",
    "params": {
        "pair": "USDC/SOL",
        "side": "SELL",
        "amount": 1,
        "exchange_ids": [
            "dex-bnb.admin"
        ],
        "type": "SPOT",
        "unit": "USDC",
        "slippage": 1,
        "algo_type": "SWAP",
        "price": 0
    }
}
```
### Request

| Name   | Type   | Description |
--------|--------|-------------
|jsonrpc | string | Only "2.0" is supported |
|id      | string | This will be echoed back in responses or subscription payloads|
|method  | string | Establishing the specific API to connect to. Documented below |
|params  | string | Details regarding the specific API call. Documented below     |
|params.pair|string | Trading pair (e.g., "USDC/SOL"), specifying the assets involved in the trade|
|params.side|string | The side of the order: "BUY" or "SELL"|
|params.amount| number| The amount of the base currency to trade|
|params.type| string| The type of trade: "SPOT"|
|params.unit| string| Denomination of the base amount|
|params.slippage| number| Maximum allowed slippage percentage                                                                                                                 |
|params.algo_type| string| Type of algorithm used for the trade. In this case, "SWAP" for decentralized swaps|
|params.price| number   | Price limit for the trade (set to 0 for swap orders)|

### Response

```json
{
    "jsonrpc": "2.0",
    "id": "595d4d5a-fb97-4577-9a0d-edcee13a5e5e",
    "result": {
        "base_amount": 1.0,
        "quote_amount": 0.006358516993544726,
        "usd_amount": 1.00008225440979,
        "usd_base_amount": 1.00008225440979,
        "usd_quote_amount": 0.9864042430477954,
        "contract_amount": "1.0000",
        "conversion_price_source": "yahoo finance",
        "plan": [
            {
                "exchange": "BNB",
                "exchange_id": "dex-bnb.admin",
                "step_price": null,
                "step_volume": null,
                "path": [
                    "USDC",
                    100,
                    "PANCAKESWAP_V3",
                    "WBNB",
                    500,
                    "PANCAKESWAP_V3",
                    "USDT",
                    10000,
                    "UNISWAP_V3",
                    "SOL"
                ],
                "base_amount": 0.1,
                "quote_amount": 0.0006374346561208406,
                "gas_amount": 0.0,
                "gas_unit": "BNB",
                "percent": 10,
                "allAmounts": [
                    "100000000000000000",
                    "170782042952549",
                    "100024146180649151",
                    "643809002682049"
                ],
                "tokenPathAddresses": [
                    "0X8AC76A51CC950D9822D68B83FE1AD97B32CD580D",
                    100,
                    "PANCAKESWAP_V3",
                    "0XBB4CDB9CBD36B01BD1CBAEBF2DE08D9173BC095C",
                    500,
                    "PANCAKESWAP_V3",
                    "0X55D398326F99059FF775485246999027B3197955",
                    10000,
                    "UNISWAP_V3",
                    "0X570A5D26F7765ECB712C0924E4DE545B89FD43DF"
                ],
                "slippage": "1.0000",
                "volume": "0.1000",
                "price": "0.0064",
                "unit": "USDC",
                "unit_volume": "0.1000",
                "transaction_amount": "0.1000",
                "transaction_unit": "USDC",
                "base": {
                    "unit": "USDC",
                    "volume": 0.1
                },
                "quote": {
                    "unit": "SOL",
                    "volume": 0.0006374346561208406
                },
                "usd_volume": "0.1000"
            },
            // More plan items here...
        ],
        "total_volume": "1.0000"
    }
}
```

| Name                         | Type    | Description                                                                                                     |
|------------------------------|---------|-----------------------------------------------------------------------------------------------------------------|
| jsonrpc                      | string  | The JSON-RPC version, typically "2.0".                                                                         |
| id                           | string  | The ID from the request, echoed back in the response.                                                           |
| result                       | object  | Contains the results of the fetch quotes operation.                                                             |
| result.base_amount           | number  | The base amount specified for the quote.                                                                        |
| result.quote_amount          | number  | The amount of the quote currency corresponding to the base amount.                                              |
| result.usd_amount            | number  | The equivalent amount in USD for the base amount.                                                               |
| result.usd_base_amount       | number  | The USD equivalent of the base amount.                                                                          |
| result.usd_quote_amount      | number  | The USD equivalent of the quote amount.                                                                         |
| result.contract_amount       | string  | The amount as formatted for the contract, typically shown with fixed decimal places.                           |
| result.plan                  | array   | An array of execution plans used for placing the order, with details for each step.                            |
| result.total_volume          | string  | The total volume of the trade represented as a string.                                                         |
| result.plan[].exchange       | string  | The exchange being used in the step of the execution plan (e.g., "BNB").                                      |
| result.plan[].exchange_id    | string  | The unique identifier for the exchange used in the step.                                                       |
| result.plan[].path           | array   | The path of tokens used in the swap, detailing the sequence of exchanges.                                     |
| result.plan[].base_amount    | number  | The amount of the base currency for this step.                                                                 |
| result.plan[].quote_amount   | number  | The amount of the quote currency for this step.                                                                |
| result.plan[].gas_amount     | number  | The amount of gas required for this step.                                                                      |
| result.plan[].gas_unit       | string  | The unit of gas being used (e.g., "BNB").                                                                     |
| result.plan[].percent        | number  | The percentage of the total volume allocated to this step.                                                     |
| result.plan[].allAmounts     | array   | An array of all amounts involved at each step in the plan.                                                    |
| result.plan[].tokenPathAddresses | array | An array of token addresses in the path of the swap.                                                          |
| result.plan[].slippage       | string  | The slippage percentage for this step, typically as a string.                                                  |
| result.plan[].volume         | string  | The volume for the transaction as a string.                                                                    |
| result.plan[].base           | object  | An object containing base currency details, including unit and volume.                                         |
| result.plan[].quote          | object  | An object containing quote currency details, including unit and volume.                                        |


---

## place_market_orders (Place Orders)

This API is used to place market orders for a token swap, using the quotes fetched in the previous step.

### Request

```json
{
  "id": "c44b40c2-b0fe-4cb5-9097-55d0873d2c86",
  "jsonrpc": "2.0",
  "method": "place_market_orders",
  "params": {
    "orders": [
      {
        "pair": "SOL/USDC",
        "side": "BUY",
        "volume": "0.007",
        "price": 0,
        "exchange": "dex-bnb.admin",
        "end_time": "2024-06-24T10:39:25.341Z",
        "start_time": "2024-06-24T09:39:39.484Z",
        "timezone": "Asia/Calcutta",
        "timestamp": 1719221974802,
        "params": {
          // Use the exact plan received in the quotes response as the plan for this order
          "slippage": 1,
          "plan": {
            "exchange": "BNB",
            "exchange_id": "dex-bnb.admin",
            "step_price": null,
            "step_volume": null,
            "path": [
              "USDC",
              100,
              "PANCAKESWAP_V3",
              "WBNB",
              500,
              "PANCAKESWAP_V3",
              "USDT",
              10000,
              "UNISWAP_V3",
              "SOL"
            ],
            "base_amount": 0.1,
            "quote_amount": 0.0006374346561208406,
            "gas_amount": 0,
            "gas_unit": "BNB",
            "percent": 10,
            "allAmounts": [
              "100000000000000000",
              "170782042952549",
              "100024146180649151",
              "643809002682049"
            ],
            "tokenPathAddresses": [
              "0X8AC76A51CC950D9822D68B83FE1AD97B32CD580D",
              100,
              "PANCAKESWAP_V3",
              "0XBB4CDB9CBD36B01BD1CBAEBF2DE08D9173BC095C",
              500,
              "PANCAKESWAP_V3",
              "0X55D398326F99059FF775485246999027B3197955",
              10000,
              "UNISWAP_V3",
              "0X570A5D26F7765ECB712C0924E4DE545B89FD43DF"
            ],
            "slippage": "1.0000",
            "volume": "0.1000",
            "price": "0.0064",
            "unit": "USDC",
            "unit_volume": "0.1000",
            "transaction_amount": "0.1000",
            "transaction_unit": "USDC",
            "base": {
              "unit": "USDC",
              "volume": 0.1
            },
            "quote": {
              "unit": "SOL",
              "volume": 0.0006374346561208406
            },
            "usd_volume": "0.1000"
          }
        }
      }
      // Add more orders here, each using the exact plan received from the quotes response
    ]
  }
}
```
| Name                         | Type    | Description                                                                                                     |
|------------------------------|---------|-----------------------------------------------------------------------------------------------------------------|
| id                           | string  | A unique identifier for the request.                                                                            |
| jsonrpc                      | string  | The JSON-RPC version, typically "2.0".                                                                         |
| method                       | string  | The API method being invoked; in this case, "place_market_orders".                                             |
| params                       | object  | Contains the parameters for the API method.                                                                     |
| params.orders                | array   | An array of orders to be placed.                                                                                |
| params.orders[].pair        | string  | The trading pair for the order (e.g., "SOL/USDC").                                                             |
| params.orders[].side        | string  | The side of the order: "BUY" or "SELL".                                                                        |
| params.orders[].volume      | string  | The volume of the base currency to trade as a string.                                                          |
| params.orders[].price       | number  | The price limit for the order; set to 0 for market orders.                                                    |
| params.orders[].exchange     | string  | The exchange where the order will be placed (e.g., "dex-bnb.admin").                                          |
| params.orders[].end_time    | string  | The expiration time for the order in ISO 8601 format.                                                          |
| params.orders[].start_time   | string  | The start time for the order in ISO 8601 format.                                                              |
| params.orders[].timezone     | string  | The timezone in which the start and end times are specified (e.g., "Asia/Calcutta").                          |
| params.orders[].timestamp    | number  | The timestamp of when the order is being placed, in milliseconds since epoch.                                  |
| params.orders[].params       | object  | Additional parameters for the order, including slippage and plan details.                                       |
| params.orders[].params.slippage | number  | Maximum allowed slippage percentage for the order.                                                             |
| params.orders[].params.plan   | object  | Copy-paste the exact plan received in the quotes response here.                                                |





# Auro Digital API

## Overview

The Auro Digital API employs WebSockets for communication between the front-end and back-end services, allowing real-time data exchange. For developers aiming to programmatically interact with Auro Digital, a direct WebSocket connection to the back-end service can be established.

Please note, this API was initially designed for internal use, primarily for front-end development. Therefore, it may possess some complex payloads. Furthermore, it is subject to potential changes based on the evolving needs of the front-end application.

# Connection Details

## Base URL

Assuming your Auro Digital URL is https://test.aurodigital.ai/, your corresponding WebSocket URL would be: wss://test-backend.aurodigital.ai/v1.

The backend service adheres to the same IP whitelist policies as the front-end service. If you need to add (static) IP addresses to the whitelist, please contact our support team.

## JSON-RPC Schema


| Name   | Type   | Description |
--------|--------|-------------
|jsonrpc | string | Only "2.0" is supported |
|id      | string | This will be echoed back in responses or subscription payloads|
|method  | string | Establishing the specific API to connect to. Documented below |
|params  | string | Details regarding the specific API call. Documented below     |


# API_GETWAY

## Base URL

Assuming your Auro Digital URL is https://test.aurodigital.ai/, your corresponding WebSocket URL would be: wss://test-backend.aurodigital.ai/v2.

The backend service adheres to the same IP whitelist policies as the front-end service. If you need to add (static) IP addresses to the whitelist, please contact our support team.

## JSON-RPC Schema


| Name   | Type   | Description |
--------|--------|-------------
|jsonrpc | string | Only "2.0" is supported |
|id      | string | This will be echoed back in responses or subscription payloads|
|method  | string | Establishing the specific API to connect to. Documented below |
|params  | string | Details regarding the specific API call. Documented below     |

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

get to all active orders




```json
{
    "jsonrpc": "2.0",
    "id": "c407195b-4c35-483d-93f5-798b391dc710",
    "method": "subscribe_algo_executions",
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



## subscribe_balances

get to all balances for the given exchanges.

```json
{
    "jsonrpc": "2.0",
    "id": "6c1985bf-80ad-4bbc-86d0-6e682cdb764d",
    "method": "subscribe_balances",
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


# Authentication

After you've established a WebSocket connection, you will need to authenticate before you can call the other methods.

## Login

First of all, you will need to log in with your Access credentials. In return, you will receive a token.



```json
{
    "jsonrpc": "2.0",
    "id": "9cc9e382-ba9a-4992-80aa-fc77628a15d9",
    "method": "login",
    "params": {
        "username": "YOUR_USERNAME",
        "password": "YOUR_PASSWORD"
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
username | string | Access username
password | string | Corresponding password

```json
{
    "jsonrpc": "2.0",
    "id": "9cc9e382-ba9a-4992-80aa-fc77628a15d9",
    "result": {
        "token": "YOUR_TOKEN"
    }
}
```
### Response

Name | Type | Description
--------- | ------- | -----------
token | string | Authentication token to be used later

## authenticate_with_token

You will need to pass the token from the previous step to this method. Once you have received a positive confirmation, your WebSocket connection is authenticated.



```json
{
    "jsonrpc": "2.0",
    "id": "6dce2124-20b7-4eac-bb94-960539f027f0",
    "method": "authenticate_with_token",
    "params": {
        "auth_token": "YOUR_TOKEN"
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
auth_token | string | Authentication Token received from login



```json
{
    "jsonrpc": "2.0",
    "id": "6dce2124-20b7-4eac-bb94-960539f027f0",
    "result": "ok"
}
```
### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation.  <br /> Negative confirmation will display an “error” field instead of “result”

# Markets

Markets represent available exchanges and trading symbols. The list of accessible markets will be determined by the configurations set by your administrator. Unsupported symbols or instruments will not appear in the list.

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






## subscribe_tickers

Subscribes to a feed of best bid and ask values for a specified crypto pair on the provided exchange(s).


```json
{
"id": "b1b61f11-d34b-408b-ba46-cd6c1907252b",
"jsonrpc": "2.0",
"method": "subscribe_tickers",
"params": {

    "pair": "ETH/BTC",
    "exchanges": ["okx-new_test"]

    }
}
```

### Request


Name | Type | Description
--------- | ------- | -----------
pair | string | The unique identifier for a symbol in Auro Digital.
exchanges | string | exchanges present in Auro Digital


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

### Response
A JSON object containing the best bid. Here's an example.


Name | Type | Description
--------- | ------- | -----------
type | string | SPOT or FUTURES.
normalized_symbol | string | The unique identifier for a symbol in Access.
exchange_id | string | The name of the exchange as configured by your administrator.
base | string | The base currency.
quote | string | The quote currency.
is_inverse | boolean | Whether this is an inverse futures contract.

## subscribe_pair

Subscribe to a pair. Returns continuous updates on all metrics of that pair on the given exchanges as well as consolidated order books and other metrics across the given exchanges.

```json
{
"id": "b1b61f11-d34b-408b-ba46-cd6c1907252b",
"jsonrpc": "2.0",
"method": "subscribe_pair",
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
exchanges | array of object	 | A list of cryptocurrency exchanges to use.


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

### Response
A JSON object containing the best bid. Here's an example.


Name | Type | Description
--------- | ------- | -----------
exchange | array of object | A list of cryptocurrency exchanges to use.
best_bid | Object | Contains the best bid data.(price,size,exchange,timestamps)

## subscribe_spread

Subscribe to all updates of a spread


```json
{
"id": "bea25a83-89f7-4af5-910a-afd23a55b0aa",
"jsonrpc": "2.0",
"method": "subscribe_spread",
    "params": {
    "long_pair": "BTC/USD",
    "long_exchanges": [
    "gemini"
    ],
    "short_pair": "BTC/USD",
    "short_exchanges": [
    "coinbasepro"
    ],
    "from_mid_agg": 0.0001,
    "cutoff": 0.1,
    "top_level_only": false,
    "net_commission": false
    }
}
```

### Request


Name | Type | Description
--------- | ------- | -----------
long_pair|	string	|The normalized symbol.
long_exchange|	string	|The name of the exchange as configured by your administrator.
short_pair	|string	|The normalized symbol.
short_exchange|	string	|The name of the exchange as configured by your administrator.
from_mid_agg|	number	|Filter for Consolidated Orderbooks
cutoff	|number	|Filter for Consolidated Orderbooks
top_level_only|	Boolean|	If True, you only get the top of the spread orderbook
net_commission|	Boolean|	If True, include fees


```json
{
  "jsonrpc": "2.0",
  "id": "bea25a83-89f7-4af5-910a-afd23a55b0aa",
  "result": {
    "long_pair": "BTC/USD",
    "short_pair": "BTC/USD",
    "long_exchanges": [
      "gemini"
    ],
    "short_exchanges": [
      "coinbasepro"
    ],
    "order_book": {
      "columns": [
        "From Mid",
        "Price",
        "Size",
        "Size Total",
        "Size $",
        "Size Total $",
        "Average Fill",
        "Exchange"
      ],
      "bids": [
        [
          0.0002,
          9.96,
          4.1373563,
          4.1373563,
          237377.853492599,
          237377.853492599,
          9.96,
          "gemini/coinbasepro"
        ],
        [
          0.0001,
          4.46,
          1.3646,
          5.5019563,
          78282.847616,
          315660.701108599,
          8.5958852032,
          "gemini/coinbasepro"
        ],
        [
          -0.0001,
          -3.57,
          0.478,
          5.9799563,
          27417.52074,
          343078.221848599,
          7.6234210521,
          "gemini/coinbasepro"
        ]
      ],
      "asks": [
        [
          0.0002,
          13.36,
          0.0635361,
          0.0635361,
          3645.430754214,
          3645.430754214,
          13.36,
          "gemini/coinbasepro"
        ],
        [
          0.0006,
          34.22,
          0.174329,
          0.2378651,
          10005.8918814,
          13651.322635614,
          28.6480895096,
          "gemini/coinbasepro"
        ],
        [
          0.0007,
          42.91,
          5.00562625,
          5.24349135,
          287325.4069454526,
          300976.7295810666,
          42.2630244376,
          "gemini/coinbasepro"
        ]
      ],
      "commission": 0.0,
      "timestamps": {
        "long": {
          "gemini": null
        },
        "short": {
          "coinbasepro": 1616407232240
        }
      },
      "done_at": {
        "long": [
          [
            "fetch_order_book",
            1616407232631
          ]
        ],
        "short": [
          [
            "fetch_order_book",
            1616407232675
          ]
        ]
      },
      "time_elapsed_after": {
        "long": [
          [
            "fetch_order_book",
            {
              "gemini": null
            }
          ]
        ],
        "short": [
          [
            "fetch_order_book",
            {
              "coinbasepro": 435
            }
          ]
        ]
      }
    },
    "other_info": [],
    "balances": {
      "coinbasepro": {
        "BTC": {
          "free": 245.62032657,
          "used": 0,
          "total": 245.62032657
        },
        "ETH": {
          "free": 893.80160773,
          "used": 0,
          "total": 893.80160773
        },
        "EUR": {
          "free": 63132.31325315,
          "used": 0,
          "total": 63132.31325315
        },
        "USD": {
          "free": 65333.57796164413,
          "used": 123.6969,
          "total": 65457.27486164413
        },
        "USDC": {
          "free": 165000.0,
          "used": 0,
          "total": 165000.0
        }
      },
      "gemini": {
        "BCH": {
          "free": 102000.0,
          "used": 0,
          "total": 102000.0
        },
        "BTC": {
          "free": 2897.07215567,
          "used": 0,
          "total": 2897.07215567
        },
        "ETH": {
          "free": 60041.823332,
          "used": 0,
          "total": 60041.823332
        },
        "LTC": {
          "free": 80000.0,
          "used": 0,
          "total": 80000.0
        },
        "USD": {
          "free": 63893.65,
          "used": 0.002957811149826739,
          "total": 63893.65295781115
        },
        "ZEC": {
          "free": 60000.0,
          "used": 0,
          "total": 60000.0
        }
      }
    },
    "time": 1616407232951
  }
}

```

### Response


Name | Type | Description
--------- | ------- | -----------
long_pair|	string	|The normalized symbol to go long.
short_pair|	string	|The normalized symbol to go short.
long_exchanges	|array of string|	The cryptocurrency exchanges used to construct the order book.
short_exchanges	|array of string	|The cryptocurrency exchanges used to construct the order book.
order_book	|object	|columns	array of string	Description of the format in bids and asks.
bids|	array of array of number or string|	Bids aggregated across the specified exchanges.
asks	array of array of number or string	|Asks aggregated across the specified exchanges.
commission|	number	|The administrator-defined fee that is applied on the order book prices.
timestamps|	object|	Internal data structure. Please do not rely on this.
done_at|	object|	Internal data structure. Please do not rely on this.
time_elapsed_after	|object	|Internal data structure. Please do not rely on this.
other_info|	array of object|	Internal data structure. Please do not rely on this.
balances|	object|	The balances on the exchanges configured by your administrator.
exchange_id	|object|	The name of the exchange as configured by your administrator.
currency_id	|object	|The currency ID.
free|	number|	Money available for trading.
used|	number|	Money on hold due to e.g., open orders.
total	number|number |free + used.
is_inverse	|boolean|	Whether this is an inverse futures contract.
time|	number|	The Unix timestamp (in milliseconds) when the data in this payload is fetched.

## subscribe_option_chain

Subscribe to realtime updates on all tickers in an option chain


```json
{
  "id": "e5825b68-85fe-4631-840a0-a911a7cd",
  "jsonrpc": "2.0",
  "method": "subscribe_option_chain",
  "params": {
    "exchange_id": "auro-deribit-test.admin",
    "base_ccy": "BTC",
    "expiry_date": "2023-12-29",
    "incremental": 1
  }
}
```

### Request


Name | Type | Description
--------- | ------- | -----------
exchange_id	|string|	Auro Digital exchange key id.
base_ccy|	string	|Base currency for option chain (BTC or ETH)
expiry_date|	string	|Option expiry date in yyyy-mm-dd format
incremental|	boolean	|Should response be full snapshots or snapshot + delta updates.


```json
{
  "id": "e5825b68-85fe-4631-840a0-a911a7cd",
  "jsonrpc": "2.0",
  "result": {
    "calls": {
      "BTC-29DEC23-30000-C": {
        "ask_iv": 61.85,
        "ask_price": 0.1895,
        "ask_size": 1.8,
        "bid_iv": 60.51,
        "bid_price": 0.185,
        "bid_size": 18.0,
        "delta": 0.56189,
        "gamma": 0.00003,
        "mark_iv": 59.55,
        "mark_price": 0.1817,
        "open_interest": 1097.3,
        "rho": 79.74308,
        "theta": -10.68694,
        "vega": 96.38734,
        "volume_24h": 0.0
      },
      "BTC-29DEC23-32000-C": {
        "ask_iv": 62.17,
        "ask_price": 0.167,
        "ask_size": 1.7,
        "bid_iv": 60.85,
        "bid_price": 0.1625,
        "bid_size": 8.0,
        "delta": 0.51352,
        "gamma": 0.00003,
        "mark_iv": 60.1,
        "mark_price": 0.1599,
        "open_interest": 18.4,
        "rho": 74.16751,
        "theta": -10.91211,
        "vega": 97.50838,
        "volume_24h": 0.0
      },
      "BTC-29DEC23-34000-C": {
        "ask_iv": 62.8,
        "ask_price": 0.1485,
        "ask_size": 1.8,
        "bid_iv": 61.04,
        "bid_price": 0.1425,
        "bid_size": 23.0,
        "delta": 0.46875,
        "gamma": 0.00003,
        "mark_iv": 60.64,
        "mark_price": 0.1411,
        "open_interest": 34.5,
        "rho": 68.72608,
        "theta": -10.98154,
        "vega": 97.26495,
        "volume_24h": 5.7
      }
    },
    "puts": {
      "BTC-29DEC23-28000-P": {
        "ask_iv": 59.12,
        "ask_price": 0.1895,
        "ask_size": 1.8,
        "bid_iv": 57.9,
        "bid_price": 0.1855,
        "bid_size": 8.0,
        "delta": -0.38632,
        "gamma": 0.00003,
        "mark_iv": 59.02,
        "mark_price": 0.1892,
        "open_interest": 1093.7,
        "rho": -120.72006,
        "theta": -10.28334,
        "vega": 93.57636,
        "volume_24h": 10.6
      },
      "BTC-29DEC23-30000-P": {
        "ask_iv": 0.0,
        "ask_price": 0.0,
        "ask_size": 0.0,
        "bid_iv": 56.32,
        "bid_price": 0.223,
        "bid_size": 13.0,
        "delta": -0.4381,
        "gamma": 0.00003,
        "mark_iv": 59.55,
        "mark_price": 0.234,
        "open_interest": 7705.7,
        "rho": -140.96937,
        "theta": -10.68698,
        "vega": 96.38776,
        "volume_24h": 0.0
      },
      "BTC-29DEC23-32000-P": {
        "ask_iv": 0.0,
        "ask_price": 0.0,
        "ask_size": 0.0,
        "bid_iv": 56.37,
        "bid_price": 0.2695,
        "bid_size": 13.0,
        "delta": -0.48649,
        "gamma": 0.00003,
        "mark_iv": 60.1,
        "mark_price": 0.2823,
        "open_interest": 0.3,
        "rho": -161.26122,
        "theta": -10.91204,
        "vega": 97.50781,
        "volume_24h": 0.0
      },
      "BTC-29DEC23-34000-P": {
        "ask_iv": 0.0,
        "ask_price": 0.0,
        "ask_size": 0.0,
        "bid_iv": 56.35,
        "bid_price": 0.319,
        "bid_size": 8.0,
        "delta": -0.53125,
        "gamma": 0.00003,
        "mark_iv": 60.64,
        "mark_price": 0.3336,
        "open_interest": 17.9,
        "rho": -181.41687,
        "theta": -10.98146,
        "vega": 97.26424,
        "volume_24h": 0.0
      }
    }
  },
  "seq_nr": 1
}

```

### Response


Name | Type | Description
--------- | ------- | -----------
seq_nr	|number|	Seqnr = 1 Full Snapshot; Seqnr > 1 = updates needed on previous snapshot


## get_option_expiries


Returns a list of valid option expiries to use in the option_chain subscription method.


```json
{

"id": "1b35ff94-d82b-11ed-b809-6bb4c1b7c9a6",

"jsonrpc": "2.0",

"method": "get_option_expiries",

"params": {

"exchange_id": "auro-deribit-test.admin",

"base_ccy": "BTC"

}

}

```

### Request


Name | Type | Description
--------- | ------- | -----------
exchange_id	|string|	Auro Digital exchange key id.
base_ccy	|string	|Base currency for option chain (BTC or ETH)


```json
{
  "jsonrpc": "2.0",
  "id": "1b35ff94-d82b-11ed-b809-6bb4c1b7c9a6",
  "result": [
    "2023-05-26",
    "2023-12-29",
    "2023-04-12",
    "2023-04-28",
    "2023-04-21",
    "2023-06-30",
    "2023-04-11",
    "2023-09-29",
    "2023-04-14"
  ]
}

```

### Response


Name | Type | Description
--------- | ------- | -----------
List of option expiry dates available for the given base ccy and exchange


# Trades

In the Auro Digital ecosystem, you can create orders once you've determined the available exchanges and trading symbols. It's crucial to note that an Auro Digital order is a unique concept that exists solely within Auro Digital and might correspond to one or multiple orders on a variety of cryptocurrency exchanges.

Direct manipulation of orders on the cryptocurrency exchanges is not possible through our API; you can only interact with Auro Digital order IDs.

If a proposed order would breach a soft compliance limit, an error message will be returned.

To override this limit, set force to true under params. However, this won't work for hard compliance limits, which can't be bypassed.


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

## place_twap_order

The place_twap_order method allows you to place Time-Weighted Average Price (TWAP) orders on an exchange. A TWAP order strategy breaks down a large order into smaller, evenly distributed slices to be executed at regular time intervals. This is typically done to mitigate the market impact of large trades. For instance, for a one-hour TWAP order with an interval of 6 minutes (360 seconds) and a total order size of 100, there will be ten slices, each of size 10.



```json
{
  "jsonrpc": "2.0",
  "id": "6e777a13-453d-4ba1-9ef8-6bab14907ab2",
  "method": "place_twap_order",
  "params": {
    "pair": "BTC/USD",
    "exchanges": ["coinbasepro", "gemini"],
    "volume": 1234,
    "price": 0.01,
    "interval": 300,
    "start_time": "2020-09-11T09:54:25.085Z",
    "end_time": "2020-09-11T10:54:25.085Z",
    "side": "BUY"
  }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
pair|	string	|The trading pair, represented as a normalized symbol.
exchanges|	array of object	|A list of exchanges where the order will be placed, as configured by your administrator.
volume|	number	|The total amount of the Auro Digital Trading order.
price|	number	|Specifies the price at which you want to execute the order.
interval|	number	|The interval in seconds at which the order slices will be executed
start_time|	timestamp	|The start datetime for the TWAP order execution
end_time|	timestamp	|The end datetime for the TWAP order execution
side|	string	|Indicates whether you want to "buy" or "sell".



```json



{
    "jsonrpc": "2.0",
    "id": "6e777a13-453d-4ba1-9ef8-6bab14907ab2",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result” 

## place_stealth_order

The place_stealth_order method allows you to place a Stealth order on any given exchange. Stealth orders are designed to conceal your entry and exit points in the market. Instead of placing visible limit orders, Stealth orders execute trades at the current market price once the pre-set price level is reached, keeping your strategy hidden from the market.



```json




{
    "jsonrpc": "2.0",
    "id": "bd2d3f49-e7e4-4151-85ff-1e7b8163cfe6",
    "method": "place_stealth_order",
    "params": {
        "pair": "BTC/USD",
        "exchanges": [
            "coinbasepro",
            "gemini"
        ],
        "volume": 1234,
        "price": 0.01,
        "interval": 300,
        "start_time": "2020-09-11T10:01:49.488Z",
        "end_time": "2020-09-11T11:01:49.488Z",
        "side": "BUY"
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
pair | string | The normalized symbol.
exchanges | array of object | A list of cryptocurrency exchanges to use.
volume | number | The amount of the Access Trading order.
price | number | The price of the Access Trading order.
interval | number | Interval in seconds
start_time | timestamp | Start datetime of algo processing
end_time | timestamp | End datetime of algo processing
side | string | buy  or sell.



```json


{
    "jsonrpc": "2.0",
    "id": "bd2d3f49-e7e4-4151-85ff-1e7b8163cfe6",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result” 

## place_route_order

Place a route order on an exchange. This endpoint defaults to the SMART order type(splits quantity into 10 slices). If you would like the CROUCH order type, set "iceberg": false in your request.

Crouch Order: Instead of posting a limit order to exchange, which divulge your trading intentions, limit order is posted within Access. Orders is sent when Crouch’s limit price reached best bid/offer

```json




{
    "jsonrpc": "2.0",
    "id": "24f58091-9bf4-47ef-9efc-9e1d4ac4b5b3",
    "method": "place_route_order",
    "params": {
        "pair": "BTC/USD",
        "exchanges": [
            "coinbasepro",
            "gemini"
        ],
        "volume": 1234,
        "price": 0.01,
        "start_time": "2020-09-11T09:58:10.653Z",
        "end_time": "2020-09-11T10:58:10.653Z",
        "side": "BUY"
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
pair | string | The normalized symbol.
exchanges | array of object | A list of cryptocurrency exchanges to use.
volume | number | The amount of the Access Trading order.
price | number | The price of the Access Trading order.
start_time | timestamp | Start datetime of algo processing
end_time | timestamp | End datetime of algo processing
side | string | buy  or sell.
iceberg | Boolean | Set as false for  CROUCH order type



```json



{
    "jsonrpc": "2.0",
    "id": "24f58091-9bf4-47ef-9efc-9e1d4ac4b5b3",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result” 

## place_vwap_order

The place_vwap_order method allows you to place a VWAP (Volume Weighted Average Price) order on a given exchange.

The place_vwap_order method places a Volume Weighted Average Price (VWAP) order. VWAP is a trading benchmark used by traders that gives the average price a security has traded at throughout the day, based on both volume and price.

VWAP orders execute at the VWAP price of an equity security over a specified period. This method is especially useful in algorithmic trading to break up a large order and execute it based on a specific benchmark to achieve the best execution price.


```json




{
    "jsonrpc": "2.0",
    "id": "0206b9fb-bbae-457e-9751-37cb24af7c7e",
    "method": "place_vwap_order",
    "params": {
        "pair": "BTC/USD",
        "exchanges": [
            "coinbasepro",
            "gemini"
        ],
        "volume": 1234,
        "price": 0.01,
        "interval": 300,
        "start_time": "2020-09-11T09:57:03.931Z",
        "end_time": "2020-09-11T10:57:03.931Z",
        "side": "BUY"
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
pair | string | The normalized symbol.
exchanges | array of object | A list of cryptocurrency exchanges to use.
volume | number | The amount of the Access Trading order.
price | number | The price of the Access Trading order.
interval | number | Interval in seconds
start_time | timestamp | Start datetime of algo processing
end_time | timestamp | End datetime of algo processing
side | string | buy  or sell.



```json



{
    "jsonrpc": "2.0",
    "id": "0206b9fb-bbae-457e-9751-37cb24af7c7e",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result” 

## place_spread6_order

The place_spread6_order method is used to place a Spread6 (Taker Taker spread execution) order on two different exchanges. This order type creates a single trading strategy from individual orders, known as 'legs'.

A Spread6 order aims to profit from the difference in prices for the same asset on two different exchanges. The spread is the price difference between leg 1 bid and leg 2 ask. The order is executed when the spread price meets a pre-set level.

This method is useful for arbitrage strategies, where you aim to profit from price differences for the same asset across different markets.


```json

{
    "jsonrpc": "2.0",
    "id": "6f9763f1-0df2-4017-8a7f-156692435767",
    "method": "place_spread6_order",
    "params": {
        "primary_pair": "BTC/USD",
        "primary_exchange": "coinbasepro",
        "primary_parent": 1,
        "secondary_pair": "BTC/USD-PERPETUAL",
        "secondary_exchange": "deribit",
        "secondary_parent": 10000,
        "spread_price": 100,
        "leg_room": 0,
        "end_time": "2020-09-10T11:03:38.269Z",
        "side": "BUY"
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
primary_pair | string | The normalized symbol.
primary_exchange | string | The name of the exchange as configured by your administrator.
primary_parent | number | Quantity
secondary_pair | string | The normalized symbol.
secondary_exchange | string | The name of the exchange as configured by your administrator.
secondary_parent | number | Quantity
spread_price | number | Leg 1 bid - Leg 2 Ask
leg_room | number or null | Price adjustment before sending an order to the exchange.
end_time | timestamp | End datetime of algo processing
side | string | buy  or sell.



```json
{
    "jsonrpc": "2.0",
    "id": "6f9763f1-0df2-4017-8a7f-156692435767",
    "result": {
        "id": 7362
    }
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
id | number | ID of algo created

## place_market_order

The place_market_order method allows you to place an order using the "MarketAlgo" algorithm. This algorithm is designed to execute market orders in the cryptocurrency market, aiming to buy or sell a specified quantity of a trading pair at the best available prices in the order book. Please note, this method is currently supported only on Deribit, Binance, and OKX exchanges.


```json
{
  "id": "97cb2cd7-f5f9-4494-ae48-43b28684e3b8",
  "jsonrpc": "2.0",
  "method": "place_market_orders",
  "params": {
    "orders": [
      {
        "pair": "ETH/BTC",
        "side": "SELL",
        "price": "0.0000",
        "volume": "1.5000",
        "exchange": "okx-new_test",
        "end_time": "2023-08-04T06:45:02.692Z",
        "start_time": "2023-08-04T05:45:22.771Z",
        "timezone": "Asia/Calcutta",
        "timestamp": 1691127909985
      }
    ]
  }
}

```

### Request

Name | Type | Description
--------- | ------- | -----------
pair|	string	|The trading pair, represented as a normalized symbol.
exchange|	array of object|	exchange where the order will be placed, as configured by your administrator.
volume|	number|	The total amount of the Auro Digital Trading order.
price|	number	|Specifies the price at which you want to execute the order.
start_time|	timestamp	|The start datetime for the Market order execution
end_time|	timestamp	|The end datetime for the Market order execution
side|	string|	Indicates whether you want to "buy" or "sell".
timestamp|	number|	The Unix timestamp (in milliseconds) when the data in this payload is fetched



```json
{
    "jsonrpc": "2.0",
    "id": "97cb2cd7-f5f9-4494-ae48-43b28684e3b8",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
id | number | ID of algo created

## place_best_maker_order


The place_best_maker_order method allows you to place an order using the "Best Maker" algorithm. This algorithm ensures the best position to take advantage of maker fees by joining the top of the order book. The order will be split into multiple slices and the algorithm will work one side of the orderbook on a single exchange and market.


```json
{
    "id": "d6fa1090-d126-4cca-90b4-71b157c52e5f",
    "jsonrpc": "2.0",
    "method": "place_best_maker_order",
    "params": {
        "timezone": "Asia/Calcutta",
        "pair": "ETH/BTC",
        "exchanges": [
            "okx-new_test"
        ],
        "slices": 10,
        "drift": 1,
        "volume": 1,
        "price": 0.06282,
        "start_time": "2023-08-04T06:22:01.338Z",
        "end_time": "2023-08-04T07:22:01.338Z",
        "side": "BUY",
        "timestamp": 1691130142899
    }
}

```

### Request

Name | Type | Description
--------- | ------- | -----------
pair|	string	|The trading pair, represented as a normalized symbol.
exchange|	array of object|	exchange where the order will be placed, as configured by your administrator.
slices|	number	|The total number of slices the order will be split into.
drift|	number	|The number of basis points the best price can move away from the current slice's order price before the order is replaced.
volume|	number|	The total amount of the Auro Digital Trading order.
price|	number	|Specifies the price at which you want to execute the order.
start_time|	timestamp	|The start datetime for the Market order execution
end_time|	timestamp	|The end datetime for the Market order execution
side|	string|	Indicates whether you want to "buy" or "sell".
timestamp	|number	|The Unix timestamp (in milliseconds) when the data in this payload is fetchedfor the Market order execution
end_time|	timestamp	|The end datetime for the Market order execution
side|	string|	Indicates whether you want to "buy" or "sell".
timestamp|	number|	The Unix timestamp (in milliseconds) when the data in this payload is fetched



```json
{
    "jsonrpc": "2.0",
    "id": "be0dc5a9-4252-4cc5-9caf-3f27f64bcc6f",
    "result": {
        "message": "OPEN: BESTMAKER 1085"
    }
}

```

### Response

Name | Type | Description
--------- | ------- | -----------
id | number | ID of algo created

## edit_algo

Edit a currently running algorithm



```json



{
    "jsonrpc": "2.0",
    "id": "1121fea1-e0c0-4679-aca0-5905aed513e0",
    "method": "edit_algo",
    "params": {
        "algo_id": 7357,
        "data": {
            "pair": "BTC/USD",
            "exchanges": [
                "coinbasepro"
            ],
            "volume": 0.02,
            "price": 1234,
            "start_time": "2020-09-10T09:44:20.000Z",
            "end_time": "2020-09-10T10:44:20.000Z"
        }
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
algo_id | number | ID of algo to edit
pair | string | The normalized symbol.
exchanges | array of object | A list of cryptocurrency exchanges to use.
volume | number | The amount of the Access Trading order.
price | number | The price of the Access Trading order.
start_time | timestamp | Start datetime of algo processing
end_time | timestamp | End datetime of algo processing



```json

{
    "jsonrpc": "2.0",
    "id": "1121fea1-e0c0-4679-aca0-5905aed513e0",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result”

## pause_algo

Pause a currently running algorithm



```json
{
    "jsonrpc": "2.0",
    "id": "d0593f4b-636d-4c99-81c6-a1d7e892f39e",
    "method": "pause_algo",
    "params": {
        "algo_id": 7357
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
algo_id | number | ID of algo to edit.



```json
{
    "jsonrpc": "2.0",
    "id": "d0593f4b-636d-4c99-81c6-a1d7e892f39e",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result”

## pause_all_algos

Pause all currently running algorithm



```json
{
    "jsonrpc": "2.0",
    "id": "a3acc6b4-257a-46d7-85c8-305c8a511b0d",
    "method": "pause_all_algos"
}
```

### Request




```json
{
    "jsonrpc": "2.0",
    "id": "a3acc6b4-257a-46d7-85c8-305c8a511b0d",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result"

## resume_algo

Resume a currently running algorithm



```json
{
    "jsonrpc": "2.0",
    "id": "f8e257db-c3ab-40fd-a593-98a95bb55283",
    "method": "resume_algo",
    "params": {
        "algo_id": 7357
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
algo_id | number | ID of algo to resume



```json
{
    "jsonrpc": "2.0",
    "id": "f8e257db-c3ab-40fd-a593-98a95bb55283",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result"

## cancel_algo

Cancel a currently running algorithm



```json
{
    "jsonrpc": "2.0",
    "id": "f96c3b62-1062-4e77-b693-d896b87625ae",
    "method": "cancel_algo",
    "params": {
        "algo_id": 7357
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
algo_id | number | ID of algo to cancel



```json
{
    "jsonrpc": "2.0",
    "id": "f96c3b62-1062-4e77-b693-d896b87625ae",
    "result": "ok"
}
```

### Response

Name | Type | Description
--------- | ------- | -----------
result | string | Confirmation of request. “ok“ indicates positive confirmation. <br /> Negative confirmation will display an “error” field instead of “result"


## subscribe_algo_executions

subscribe to all active orders




```json
{
    "jsonrpc": "2.0",
    "id": "c407195b-4c35-483d-93f5-798b391dc710",
    "method": "subscribe_algo_executions",
    "params": {
        "algo_execution_id": 12,
        "include_tick_level_pretrade_info": false,
        "start_time": "2018-09-07T16:00:00.000Z",
        "end_time": "2020-09-07T16:00:00.000Z",
        "filters": [
            {
                "exchange_id": "coinbasepro",
                "normalized_symbol": "BTC/USD"
            }
        ],
        "algos_only": false
    }
}
```

### Request

Name | Type | Description
--------- | ------- | -----------
algo_execution_id	|id	|ID of algo to edit
include_tick_level_pretrade_info|	Boolean	|The normalized symbol.
start_time	|timestamp	|A list of cryptocurrency exchanges to use.
end_time|	timestamp|	The amount of the Auro Digital Trading order.
exchange_id	|string	|The price of the Auro Digital Trading order.
normalized_symbol	|string|	Start datetime of algo processing
algo_only|	Boolean|	End datetime of algo processing



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




# Accounts
Accounts allow users to interact with all of the exchange accounts.



## subscribe_balances

Subscribe to all balances for the given exchanges.

```json
{
    "jsonrpc": "2.0",
    "id": "6c1985bf-80ad-4bbc-86d0-6e682cdb764d",
    "method": "subscribe_balances",
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

# Portfolio

## subscribe_portfolio_trades

This endpoint, "subscribe_portfolio_trades," fetches portfolio trade data, offering users insights into their investment activities. The "period" parameter specifies the timeframe, allowing selection from options like "DTD," "MTD," "YTD," "ITD," or "Custom." It enables users to monitor portfolio performance over specific time intervals for informed decision-making.


```json
{
  "id": "4feac4e0-3148-453c-ab40-3a487c7f0f94",
  "jsonrpc": "2.0",
  "method": "subscribe_portfolio_trades",
  "period": "YTD"
}

```

### Request

Name | Type | Description
--------- | ------- | -----------
id	|string	|A unique identifier for the request.
period	|string	|Specifies the period for which portfolio trades are requested. Accepts values like "DTD", "MTD", "YTD", "ITD", or "Custom".


```json
{
    "jsonrpc": "2.0",
    "id": "4feac4e0-3148-453c-ab40-3a487c7f0f94",
    "result": {
        "view_type": "trades_paginated",
        "timestamp": 1717484862266,
        "client_id": "demo",
        "parameters": {
            "client_id": "demo",
            "parent_portfolio_id": 20,
            "accounting_currency": "USD",
            "period": "YTD",
            "fiscal_year_end": ""
        },
        "columns": [
            {
                "title": "Trade ID",
                "field_name": "tradeId",
                "description": "AuroPMS Unique Trade ID",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Trade Time",
                "field_name": "trade_date",
                "description": "Venue created time",
                "data_type": "Datetime",
                "aggr_func": null
            },
            {
                "title": "Portfolio",
                "field_name": "portfolio",
                "description": "Venue/Exchange Account",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "........"
            },
            {
                "title": "Theta",
                "field_name": "theta",
                "description": "Theta",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            }
        ],
        "records": [
            {
                "tradeId": 31340,
                "trade_date": "2024-01-17T06:56:18.076000",
                "portfolio": "deribit-6u5",
                "portfolio_id": 22,
                "venueName": "deribit",
                "insName": "ETH/USDT",
                "insType": "SPOT",
                "instrument_id": 67,
                "user": "EXTERNAL",
                "algo": "NA",
                "currency": "USDT",
                "quantity": -0.0001,
                "price": 2562.43,
                "side": "SELL",
                "tradeOriginalExposure": -0.256243,
                "fee": 0,
                "valuationPrice": 3910.490051,
                "currentExposure": -0.391049,
                "fx_adjustment": 1,
                "accCurrency": "USD",
                "tradeOriginalExposureAccCurr": -0.256243,
                "feeAccCurr": 0,
                "currentExposureAccCurr": -0.391049,
                "initialMargin": 0,
                "maintenanceMargin": 0,
                "initialMarginAccCurr": 0,
                "maintenanceMarginAccCurr": 0,
                "delta": 0,
                "gamma": 0,
                "rho": 0,
                "vega": 0,
                "theta": 0
            },
        ],
        "page": "1",
        "end": true
    }
}

```

### Response

Name | Type | Description
--------- | ------- | -----------
view_type	|string	|Type of view for the trades (e.g., "trades_paginated").
timestamp	|number	|Timestamp of the response.
client_id|	string|	The client ID associated with the request.
parameters|	object	|Additional parameters for the request, including client ID, portfolio ID, accounting currency, period, and fiscal year end.
columns	|array of objects	|Descriptions of each column in the trade records.
records|	array of objects|	The trade records, each containing details about a specific trade.
page|	string|Indicates the current page of the response.
end|	boolean	|Indicates if it's the end of the response.

### Columns

Key | Type | Description
--------- | ------- | -----------
title|	string|	The display title of the column.
field_name|	string|	The field name used in the data records.
description	|string|	A description of what the column represents.
data_type|	string|	The type of data stored in the column (e.g., Categorical, Datetime, Numerical-Continuous).
aggr_func|	string|	Aggregation function applied to the column data (if any).

### Records

Name | Type | Description
--------- | ------- | -----------
tradeId	|number|	AuroPMS Unique Trade ID
trade_date|	string	|Venue created time
portfolio	|string	|Venue/Exchange Account
portfolio_id|	number|	Unique identifier for the portfolio
venueName|	string	|Venue where trade occurred
insName	|string|	Normalized instrument name
insType|	string|	Instrument Type
instrument_id|	number|	Unique identifier for the instrument
user|	string|	User that made the trade
algo	|string	|Algo that created the trade
currency	|string	|Trade currency
quantity	|number	|Quantity of instrument traded
price|	number|	Price traded at
side|	string|	Trade side (e.g., BUY, SELL)
tradeOriginalExposure|	number|	Exposure at the time of trade in trade currency
fee	|number|	Fee amount
valuationPrice|	number	|Current market price of the instrument
currentExposure	|number	|Market value of the trade given the current instrument valuation price
fx_adjustment	|number|	Current currency conversion factor to accounting currency
accCurrency|	string	|Accounting currency
tradeOriginalExposureAccCurr	|number	|Exposure at the time of trade in accounting currency
feeAccCurr	|number|	Fee amount in accounting currency
currentExposureAccCurr	|number	|Market value of the trade in accounting currency
initialMargin|	number	|Initial margin in trade currency
maintenanceMargin	|number|	Maintenance margin in trade currency
initialMarginAccCurr	|number	|Initial margin in accounting currency
maintenanceMarginAccCurr	|number|	Maintenance margin in accounting currency
delta	|number	|Delta
gamma|	number|	Gamma
rho|	number|	Rho
vega	|number	|Vega
theta	|number	|Theta

## subscribe_portfolio_transactions
The "subscribe_portfolio_transactions" endpoint delivers transaction details for a portfolio, including transaction date, ID, type, instrument name, user, currency, and various financial metrics. It provides comprehensive insights into portfolio activity, facilitating effective monitoring and analysis of transactions over time.


```json
{
    "id": "c105f94b-1e72-47a4-9b22-0d5ea6551a72",
    "jsonrpc": "2.0",
    "method": "subscribe_portfolio_transactions",
    "period": "MTD"
}


```

### Request

Name | Type | Description
--------- | ------- | -----------
id	|string	|A unique identifier for the request.
period	|string	|Specifies the period for which portfolio trades are requested. Accepts values like "DTD", "MTD", "YTD", "ITD", or "Custom".


```json
{
    "jsonrpc": "2.0",
    "id": "c105f94b-1e72-47a4-9b22-0d5ea6551a72",
    "result": {
        "view_type": "transaction_paginated",
        "timestamp": 1717485202172,
        "client_id": "demo",
        "parameters": {
            "client_id": "demo",
            "parent_portfolio_id": 20,
            "period": "MTD",
            "accounting_currency": "USD"
        },
        "columns": [
            {
                "title": "Portfolio",
                "field_name": "portfolio",
                "description": "Exchange Account",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Transaction Date",
                "field_name": "transactionDate",
                "description": "Transaction Date",
                "data_type": "Datetime",
                "aggr_func": null
            },
            {
                "title": "Transaction ID",
                "field_name": "transactionId",
                "description": "Unique Transaction ID",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Transaction Type",
                "field_name": "type",
                "description": "Transaction Type",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Instrument Name",
                "field_name": "insName",
                "description": "Normalized instrument name",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "User",
                "field_name": "user",
                "description": "User that made the transaction",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Bk Ccy",
                "field_name": "currency",
                "description": "Transaction Currency",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "FX Adjustment",
                "field_name": "fx_adjustment",
                "description": "Current currency conversion factor to accounting currency",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            },
            {
                "title": "Original Exposure (Bk Ccy)",
                "field_name": "value",
                "description": "Transaction Value",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            },
            {
                "title": "Market Price (Bk Ccy)",
                "field_name": "marketPrice",
                "description": "Currency Market Price of Transaction Currency in terms of Accounting Currency",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            },
            {
                "title": "Current Exposure (Acc Ccy)",
                "field_name": "currentValueAccCurr",
                "description": "Transaction Value",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            },
            {
                "title": "Trans Fee",
                "field_name": "fee",
                "description": "Fee amount",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            },
            {
                "title": "Trans Fee (Acc Ccy)",
                "field_name": "feeAccCurr",
                "description": "Fee amount (in accounting currency)",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            },
            {
                "title": "Funding Fee",
                "field_name": "fundingFee",
                "description": "Funding Fee amount",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            },
            {
                "title": "Funding Fee (Acc Ccy)",
                "field_name": "fundingFeeAccCurr",
                "description": "Funding Fee amount (in accounting currency)",
                "data_type": "Numerical-Continuous",
                "aggr_func": null
            }
        ],
        "records": [
            {
                "portfolio": "deribit-6u5",
                "transactionDate": "2024-06-01T08:00:00.044000",
                "transactionId": 374188,
                "type": "INTEREST_PAYMENT",
                "insName": "DERIBIT-ETH/USD-PERPETUAL",
                "user": "NA",
                "currency": "ETH",
                "fx_adjustment": 3674.895061,
                "value": 0,
                "marketPrice": 3674.895061,
                "currentValueAccCurr": 0.001003,
                "fee": 0,
                "feeAccCurr": 0,
                "fundingFee": 0,
                "fundingFeeAccCurr": 0.001003
            },
            {
                "portfolio": "deribit-6u5",
                "transactionDate": "2024-06-02T08:00:00.050000",
                "transactionId": 374210,
                "type": "INTEREST_PAYMENT",
                "insName": "DERIBIT-ETH/USD-PERPETUAL",
                "user": "NA",
                "currency": "ETH",
                "fx_adjustment": 3674.895061,
                "value": 0,
                "marketPrice": 3674.895061,
                "currentValueAccCurr": 0.000794,
                "fee": 0,
                "feeAccCurr": 0,
                "fundingFee": 0,
                "fundingFeeAccCurr": 0.000794
            },
            {
                "portfolio": "deribit-6u5",
                "transactionDate": "2024-06-03T08:00:00.041000",
                "transactionId": 374222,
                "type": "INTEREST_PAYMENT",
                "insName": "DERIBIT-ETH/USD-PERPETUAL",
                "user": "NA",
                "currency": "ETH",
                "fx_adjustment": 3674.895061,
                "value": 0,
                "marketPrice": 3674.895061,
                "currentValueAccCurr": 0.000625,
                "fee": 0,
                "feeAccCurr": 0,
                "fundingFee": 0,
                "fundingFeeAccCurr": 0.000625
            }
        ],
        "page": "1",
        "end": true
    }
}

```

### Response

Name | Type | Description
--------- | ------- | -----------
view_type	|string	|Type of view for the trades (e.g., "trades_paginated").
timestamp	|number	|Timestamp of the response.
client_id|	string|	The client ID associated with the request.
parameters|	object	|Additional parameters for the request, including client ID, portfolio ID, accounting currency, period, and fiscal year end.
columns	|array of objects	|Descriptions of each column in the trade records.
records|	array of objects|	The trade records, each containing details about a specific trade.
page|	string|Indicates the current page of the response.
end|	boolean	|Indicates if it's the end of the response.

### Column

Name | Type | Description
--------- | ------- | -----------
title|	string	|The display title of the column.
field_name|	string	|The field name used in the data records.
description	|string|	A description of what the column represents.
data_type|	string	|The type of data stored in the column (e.g., Categorical, Datetime, Numerical-Continuous).
aggr_func	|string	|Aggregation function applied to the column data (if any).

### Records

portfolio|	string	|The name of the portfolio or exchange account.
transactionDate|	string	|The date and time of the transaction.
transactionId|	number|	The unique identifier for the transaction.
type|	string|	The type of transaction (e.g., INTEREST_PAYMENT).
insName	|string|	Normalized name of the instrument.
user|	string|	The user who made the transaction.
currency|	string	|The currency of the transaction.
fx_adjustment|	number|	The current currency conversion factor to accounting currency.
value|	number|	The value of the transaction in transaction currency.
marketPrice|	number|	The market price of the transaction currency in terms of accounting currency.
currentValueAccCurr|	number|	The current exposure value in accounting currency.
fee|number|	The fee amount for the transaction.
feeAccCurr	|number|	The fee amount in accounting currency.
fundingFee|	number|	The funding fee amount for the transaction.
fundingFeeAccCurr|	number|	The funding fee amount in accounting currency.

## subscribe_portfolio_positions
subscribe_portfolio_positions allows real-time updates on a portfolio's positions, including instrument types, valuation prices, and profit/loss data, enabling informed decision-making.


```json
{
    "id": "84ce81bb-ce15-45a2-9fd1-fee002035c92",
    "jsonrpc": "2.0",
    "method": "subscribe_portfolio_positions",
    "period": "DTD"
}


```

### Request

Name | Type | Description
--------- | ------- | -----------
id	|string	|A unique identifier for the request.
period	|string	|Specifies the period for which portfolio trades are requested. Accepts values like "DTD", "MTD", "YTD", "ITD", or "Custom".


```json
{
    "jsonrpc": "2.0",
    "id": "84ce81bb-ce15-45a2-9fd1-fee002035c92",
    "result": {
        "view_type": "positions",
        "client_id": "demo",
        "timestamp": 1717485286200,
        "parameters": {
            "client_id": "demo",
            "parent_portfolio_id": 20,
            "period": "DTD",
            "accounting_currency": "USD",
            "accounting_method": "FIFO"
        },
        "columns": [
            {
                "title": "Portfolio/Exchange Account",
                "field_name": "portfolio",
                "description": "Exchange Account",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Instrument Name",
                "field_name": "insName",
                "description": "Normalized instrument name",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Instrument Type",
                "field_name": "insType",
                "description": "Instrument Type",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Underlying",
                "field_name": "underlying",
                "description": "Uderlying Instrument for Main Insturment",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Expired",
                "field_name": "expired",
                "description": "Expired (Applicable for options + futures)",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Expiry Date",
                "field_name": "expiryDate",
                "description": "Expiry Date",
                "data_type": "Datetime",
                "aggr_func": null
            },
            {
                "........."
            },
            {
                "title": "Trades",
                "field_name": "trades",
                "description": "List of all trades for this position",
                "data_type": "PMS-List",
                "aggr_func": null
            }
        ],
        "records": [
            {
                "portfolio": "deribit-6u5-2",
                "insName": "DERIBIT-ETH/USD-PERPETUAL",
                "insType": "PERPETUAL",
                "valuationPrice": 3763.48,
                "underlying": "ETH",
                "expired": "False",
                "expiryDate": null,
                "contractSize": null,
                "number": 4,
                "pnlCurrency": "ETH",
                "fx_adjustment": 3674.895061,
                "fundingFees": 0.000021,
                "tradeFees": 0.000002,
                "totalFees": 0.000023,
                "netPosition": -2,
                "side": "SHORT",
                "totalPositionCost": 0.000402,
                "currentExposure": -1881.74,
                "openAveragePositionCost": 2501.2,
                "realized_pnl": -0.00001,
                "unrealized_pnl": -0.000268,
                "total_pnl": -0.000279,
                "currentExposureAccCurr": -6915197.033027,
                "realized_pnlAccCurr": -0.038586,
                "unrealized_pnlAccCurr": -0.985582,
                "total_pnlAccCurr": -1.024168,
                "initialMargin": 0,
                "maintenanceMargin": 0,
                "initialMarginAccCurr": 0,
                "maintenanceMarginAccCurr": 0,
                "dtd_price": 0,
                "dtd_realized_pnl": 0,
                "dtd_unrealized_pnl": -0.000268,
                "dtd_total_pnl": -0.000268,
                "dtd_realized_pnlAccCurr": 0,
                "dtd_unrealized_pnlAccCurr": -0.985582,
                "dtd_total_pnlAccCurr": -0.985582,
                "mtd_price": 0,
                "mtd_realized_pnl": 0,
                "mtd_unrealized_pnl": -0.000268,
                "mtd_total_pnl": -0.000268,
                "mtd_realized_pnlAccCurr": 0,
                "mtd_unrealized_pnlAccCurr": -0.985582,
                "mtd_total_pnlAccCurr": -0.985582,
                "ytd_price": 0,
                "ytd_realized_pnl": -0.00001,
                "ytd_unrealized_pnl": -0.000268,
                "ytd_total_pnl": -0.000279,
                "ytd_realized_pnlAccCurr": -0.038586,
                "ytd_unrealized_pnlAccCurr": -0.985582,
                "ytd_total_pnlAccCurr": -1.024168,
                "trades": []
            }
        ]
    }
}

```

### Response

Name | Type | Description
--------- | ------- | -----------
view_type	|string	|Type of view for the trades (e.g., "trades_paginated").
timestamp	|number	|Timestamp of the response.
client_id|	string|	The client ID associated with the request.
parameters|	object	|Additional parameters for the request, including client ID, portfolio ID, accounting currency, period, and fiscal year end.
columns	|array of objects	|Descriptions of each column in the trade records.
records|	array of objects|	The trade records, each containing details about a specific trade.

### Columns
Key | Type | Description
--------- | ------- | -----------
view_type	|string	|Type of view for the trades (e.g., "trades_paginated").
timestamp	|number	|Timestamp of the response.
client_id|	string|	The client ID associated with the request.
parameters|	object	|Additional parameters for the request, including client ID, portfolio ID, accounting currency, period, and fiscal year end.
columns	|array of objects	|Descriptions of each column in the trade records.
records|	array of objects|	The trade records, each containing details about a specific trade.

### Records

Key | Type | Description
--------- | ------- | -----------
portfolio|	string|	The name of the portfolio or exchange account.
insName|	string|	Normalized name of the instrument.
insType	|string	|The type of the instrument (e.g., PERPETUAL).
valuationPrice|	number	|The current valuation price of the instrument.
underlying	|string	|The underlying asset of the instrument (e.g., ETH).
expired	|string|	Indicates if the instrument has expired ("True" or "False").
expiryDate|	string	|The expiry date of the instrument (if applicable).
contractSize|	number	|The size of the contract (if applicable).
number|	number	|The number of contracts.
pnlCurrency	|string	|The currency in which PnL is calculated.
fx_adjustment	|number	|The foreign exchange adjustment value.
fundingFees|	number	|The fees incurred from funding.
tradeFees	|number	|The fees incurred from trading.
totalFees	|number	|The total fees incurred.
netPosition	|number	|The net position of the instrument.
side	|string	|Indicates whether the position is LONG or SHORT.
totalPositionCost	|number	|The total cost of the position.
currentExposure	|number|	The current exposure of the position.
openAveragePositionCost	|number	|The average cost of opening the position.
realized_pnl|	number|	The realized profit and loss.
unrealized_pnl|	number	|The unrealized profit and loss.
total_pnl	|number|The total profit and loss (realized + unrealized).
currentExposureAccCurr|	number	|The current exposure in accounting currency.
realized_pnlAccCurr	|number	|The realized profit and loss in accounting currency.
unrealized_pnlAccCurr	|number	|The unrealized profit and loss in accounting currency.
total_pnlAccCurr	|number	|The total profit and loss in accounting currency.
initialMargin|	number	| The initial margin required for the position.
maintenanceMargin	|number	|The maintenance margin required for the position.
initialMarginAccCurr	|number|	The initial margin in accounting currency.
maintenanceMarginAccCurr|	number	|The maintenance margin in accounting currency.
dtd_price	|number	|The day-to-date price.
dtd_realized_pnl	|number|	The day-to-date realized profit and loss.
dtd_unrealized_pnl	|number|	The day-to-date unrealized profit and loss.
dtd_total_pnl	|number|	The day-to-date total profit and loss.
dtd_realized_pnlAccCurr	|number|	The day-to-date realized profit and loss in accounting currency.
dtd_unrealized_pnlAccCurr	|number	|The day-to-date unrealized profit and loss in accounting currency.
dtd_total_pnlAccCurr|	number	|The day-to-date total profit and loss in accounting currency.
mtd_price|	number|	The month-to-date price.
mtd_realized_pnl	|number|	The month-to-date realized profit and loss.
mtd_unrealized_pnl|	number	|The month-to-date unrealized profit and loss.
mtd_total_pnl|	number	|The month-to-date total profit and loss.
mtd_realized_pnlAccCurr	|number	|The month-to-date realized profit and loss in accounting currency.
mtd_unrealized_pnlAccCurr	|number	|The month-to-date unrealized profit and loss in accounting currency.
mtd_total_pnlAccCurr	|number	|The month-to-date total profit and loss in accounting currency.
ytd_price|	number	|The year-to-date price.
ytd_realized_pnl	|number|	The year-to-date realized profit and loss.
ytd_unrealized_pnl	|number|	The year-to-date unrealized profit and loss.
ytd_total_pnl|number	|The year-to-date total profit and loss.
ytd_realized_pnlAccCurr	|number|	The year-to-date realized profit and loss in accounting currency.
ytd_unrealized_pnlAccCurr	|number|	The year-to-date unrealized profit and loss in accounting currency.
ytd_total_pnlAccCurr|	number|	The year-to-date total profit and loss in accounting currency.
trades|	array|An array of trades associated with the position.

## subscribe_auro_pms_wallets
The subscribe_auro_pms_wallets endpoint allows users to retrieve wallet information from the portfolio management system. The response includes details such as currency balance, percentage of portfolio, margin balance, instrument, and portfolio.



```json
{
    "id": "908ee8b3-b4bc-4045-a9bd-c32e18d10049",
    "jsonrpc": "2.0",
    "method": "subscribe_auro_pms_wallets"
}


```

### Request

Name | Type | Description
--------- | ------- | -----------
id	|string	|A unique identifier for the request.

```json
{
    "jsonrpc": "2.0",
    "id": "f1986b5d-a8b7-47a2-9333-e2f123dca9b6",
    "result": {
        "view_type": "wallets",
        "timestamp": 1719479343004,
        "parameters": {
            "client_id": "demo",
            "parent_portfolio_id": 20,
            "period": "DTD",
            "accounting_currency": "USD",
            "accounting_method": "FIFO"
        },
        "columns": [
            {
                "title": "",
                "field_name": "type",
                "description": "Trading or Margin view",
                "data_type": "Categorical",
                "aggr_func": null
            },
            {
                "title": "Currency",
                "field_name": "currency",
                "description": "Transaction Portfolio",
                "data_type": "Categorical",
                "aggr_func": null
            },
        ],
        "records": [
            {
                "type": "trading",
                "client": "demo",
                "currency": "USD",
                "trading_original_balance": -209166.831,
                "trading_balanceAccCurr": -209166.831,
                "trading_portfolio_percentage": -76.7521,
                "transactions_balance": -209166.831,
                "transactions_balanceAccCurr": -209166.831,
                "realized_pnl": 0,
                "realized_pnlAccCurr": 0,
                "total_balance": -209166.831,
                "instrument": "",
                "portfolio": "",
                "initialMargin": 0,
                "maintenanceMargin": 0,
                "initialMarginAccCurr": 0,
                "maintenanceMarginAccCurr": 0,
                "underlying_balances": [
                    {
                        "portfolio": "weraefsnlaef21345",
                        "amount": -69722.277
                    },
                    {
                        "portfolio": "21345t324",
                        "amount": -69722.277
                    },
                    {
                        "portfolio": "aps234",
                        "amount": -69722.277
                    }
                ],
                "underlying_transactions": [
                    {
                        "exchange_account": "21345t324",
                        "transaction_date": "2024-06-19T00:00:00",
                        "amount": -69722.277
                    },
                    {
                        "exchange_account": "aps234",
                        "transaction_date": "2024-06-19T00:00:00",
                        "amount": -69722.277
                    },
                    {
                        "exchange_account": "weraefsnlaef21345",
                        "transaction_date": "2024-06-19T00:00:00",
                        "amount": -69722.277
                    }
                ],
                "underlying_positions": []
            },
        ],
        "info": {
            "sum_trading_balance": 272522.4889735035,
            "sum_recon_balance": 272749.95078064,
            "sum_initial_margin": 0,
            "sum_maintenance_margin": 0
        }
    }
}

```

### Response

Name | Type | Description
--------- | ------- | -----------
client_id|string|	Identifier for the client.
parent_portfolio_id	|number	|Identifier for the parent portfolio.
period	|string	|The period for the data (e.g., "DTD").
accounting_currency|	string	|The accounting currency used.
accounting_method	|string|	The accounting method used (e.g., "FIFO").

### Column

Name | Type | Description
--------- | ------- | -----------
title|	string	|The display title of the column.
field_name|	string	|The field name used in the data records.
description	|string|	A description of what the column represents.
data_type|	string	|The type of data stored in the column (e.g., Categorical, Datetime, Numerical-Continuous).
aggr_func	|string	|Aggregation function applied to the column data (if any).

### Records

type|	string|	Trading or Margin view
client|	string	|Client identifier
currency	|string	|Currency
trading_original_balance|	number	|Total currency balance from exchanges
trading_balanceAccCurr|	number|	Total currency balance from exchanges in USD
trading_portfolio_percentage|	number|	Portfolio net deposit/withdrawal percentage
transactions_balance|	number|	Transactions balance
transactions_balanceAccCurr	|number|	Transactions balance in USD
realized_pnl	|number|	Realized profit and loss
realized_pnlAccCurr	|number	|Realized profit and loss in USD
total_balance	|number|	Total balance
instrument|	string	|Instrument
portfolio|	string|	Portfolio
initialMargin	|number|	Initial margin
maintenanceMargin|	number	|Maintenance margin
initialMarginAccCurr|	number	|Initial margin in USD
maintenanceMarginAccCurr	|number|	Maintenance margin in USD
underlying_balances|	array of objects	|List of underlying balances
underlying_transactions	|array of objects	|List of underlying transactions
underlying_positions|	array of objects|	List of underlying positions

## get_pms_performance_metrics
The get_pms_performance_metrics endpoint provides performance metrics based on daily returns. It returns client details, cumulative return chart data, and various performance indicators. This endpoint is useful for analyzing portfolio management system performance.


```json
{
    "id": "342e98db-b700-41f5-8357-f20a581333ce",
    "jsonrpc": "2.0",
    "method": "get_pms_performance_metrics",
    "params": {}
}



```

### Request

Name | Type | Description
--------- | ------- | -----------
id|	string|	A unique identifier for the request.
params	|object	|Parameters for the request (empty object in this example).

```json
{
    "jsonrpc": "2.0",
    "id": "342e98db-b700-41f5-8357-f20a581333ce",
    "result": {
        "client_details": {
            "client_name": null,
            "icon": null,
            "address": null,
            "fund_type": null,
            "strategy_name": null,
            "strategy_description": null
        },
        "chart_data": [

            {
                "Date": "2024-06-01",
                "CumulativeReturn": -5660.511,
                "BtcCumulativeReturn": 78.972
            },
            {
                "Date": "2024-06-02",
                "CumulativeReturn": -5623.416,
                "BtcCumulativeReturn": 79.09
            },
            {
                "Date": "2024-06-03",
                "CumulativeReturn": -5623.464,
                "BtcCumulativeReturn": 81.874
            },
            {
                "Date": "2024-06-04",
                "CumulativeReturn": -5635.132,
                "BtcCumulativeReturn": 82.459
            }
        ],
        "mix": {
            "pnl_mix": {
                "SPOT": 19.365777,
                "OPTION": 0,
                "PERPETUAL": -1.024168
            },
            "dollar_value_mix": {
                "SPOT": {
                    "USDT": 381.272009
                },
                "PERPETUAL": {
                    "USD": 10
                },
                "OPTION": {
                    "USD": 2
                }
            }
        },
        "strategy_metrics": {
            "risk_rate": 0,
            "inception_date": "2023-11-28T00:00:00",
            "cum_return": -5635.132425353831,
            "ytd_return": -5058.35944593617,
            "mtd_return": 0.7284770513123373,
            "irr": null,
            "sharpe_ratio": null,
            "sortino_ratio": null,
            "max_drawdown": -9399.774374397575,
            "longest_dd": 92,
            "average_drawdown": -2824.352767302506,
            "average_dd": 30.634730538922156,
            "volatility": 1326.389611192596,
            "payoff_ratio": 0.7407165753848713,
            "profit_factor": 0.906288515765019,
            "best_month": 36.33,
            "worst_month": -144.07,
            "avg_up_month": 14.093999999999998,
            "avg_down_month": -53.82,
            "win_rate": 0.5473684210526316
        },
        "btc_metrics": {
            "risk_rate": 0,
            "inception_date": "2023-11-28T00:00:00",
            "cum_return": 85.28421788375815,
            "ytd_return": 63.316662797248945,
            "mtd_return": 2.2738887735835656,
            "irr": -23.881687733010924,
            "sharpe_ratio": -0.4343299639582468,
            "sortino_ratio": -0.6833856140723226,
            "max_drawdown": -39.80625280287957,
            "longest_dd": 83,
            "average_drawdown": -10.713290188250713,
            "average_dd": 26.641975308641975,
            "volatility": 54.98512585999415,
            "payoff_ratio": 1.1253711095084709,
            "profit_factor": 1.4201111619987847,
            "best_month": "",
            "worst_month": "",
            "avg_up_month": "",
            "avg_down_month": "",
            "win_rate": 0.5578947368421052
        },
        "strategy_vs_btc": {
            "alpha_itd": -5720.41664323759,
            "alpha_ytd": -5121.676108733419,
            "alpha_mtd": -1.5454117222712282,
            "correlation": 0.0007707642831731058,
            "beta": null
        },
        "return": {
            "roe": {
                "gross_itd": -5635.132425353831,
                "gross_ytd": -505835.944593617,
                "gross_mtd": 72.84770513123374,
                "net_itd": -556820.2083807857,
                "net_ytd": -500814.64253327256,
                "net_mtd": 70.5635432524221
            },
            "roic": {
                "gross_itd": -563513.2425353831,
                "gross_ytd": -505835.944593617,
                "gross_mtd": 72.84770513123374,
                "net_itd": -556820.2083807857,
                "net_ytd": -500814.64253327256,
                "net_mtd": 70.5635432524221
            }
        },
        "alpha": {
            "benchmark": {
                "bitcoin_itd": 82.45866339664863,
                "bitcoin_ytd": 56.283140899616754,
                "bitcoin_mtd": 1.9483324733156038,
                "crypto_index_itd": 84.58492483114344,
                "crypto_index_ytd": 65.11988741810308,
                "crypto_index_mtd": 1.5910538157352578
            },
            "net_alpha_roe": {
                "bitcoin_itd": -5717.59108875048,
                "bitcoin_ytd": -5114.642586835787,
                "bitcoin_mtd": -1.2198554220032665,
                "crypto_index_itd": -5719.717350184975,
                "crypto_index_ytd": -5123.479333354273,
                "crypto_index_mtd": -0.8625767644229205
            },
            "net_alpha_roic": {
                "bitcoin_itd": -5717.59108875048,
                "bitcoin_ytd": -5114.642586835787,
                "bitcoin_mtd": -1.2198554220032665,
                "crypto_index_itd": -5719.717350184975,
                "crypto_index_ytd": -5123.479333354273,
                "crypto_index_mtd": -0.8625767644229205
            }
        },
        "exposure": {
            "standard": {
                "long%": 0.8965527921627269,
                "short%": -15807.228801519295,
                "gross%": 15808.125354311458,
                "net%": -15806.33224872713
            },
            "delta_adjusted": {
                "long%": 0.8965527921627269,
                "short%": -15807.228801519295,
                "gross%": 15808.125354311458,
                "net%": -15806.33224872713
            }
        },
        "risk": {
            "volatility": 1326.389611192596,
            "correlation": 0.0007707642831731058,
            "beta_crypto": 0.72,
            "beta_btc": 0.56,
            "var": 0.37
        },
        "risk_adjusted_return": {
            "gross_sharpe_ratio": -0.006898133386528634,
            "net_sharpe_ratio": -0.0070174757785990485,
            "gross_sortino_ratio": -0.006011455091935431,
            "net_sortino_ratio": -0.006149108620914119,
            "batting_average": 0.5473684210526316,
            "payoff_ratio": 0.7407165753848713,
            "profit_factor": 0.906288515765019
        },
        "drawdown": {
            "max_drawdown": -9399.774374397575,
            "longest_dd": 92,
            "average_drawdown": -2824.352767302506,
            "average_dd": 30.634730538922156
        },
        "win_loss": {
            "batting_average": 0.5473684210526316,
            "payoff_ratio": 0.7407165753848713,
            "profit_factor": 0.906288515765019
        },
        "monthly_returns": {
            "2023-11": "-0.21%",
            "2023-12": "11.99%",
            "2024-01": "0.53%",
            "2024-02": "36.33%",
            "2024-03": "-144.07%",
            "2024-04": "-17.18%",
            "2024-05": "20.88%",
            "2024-06": "0.74%"
        },
        "top_pnl_by_instruments": {
            "itd": [["ETH/USDT", 11.193017], ["ETH/BTC", 8.17276], ["DERIBIT-ETH-31MAY24-3500-P", 0], ["DERIBIT-ETH/USD-PERPETUAL", -1.024168]],
            "ytd": [["ETH/USDT", 11.193017], ["DERIBIT-ETH-31MAY24-3500-P", 0], ["DERIBIT-ETH/USD-PERPETUAL", -1.024168], ["ETH/BTC", -117.548215]],
            "mtd": [["ETH/USDT", 391.440054], ["DERIBIT-ETH-31MAY24-3500-P", 0], ["DERIBIT-ETH/USD-PERPETUAL", -0.985582], ["ETH/BTC", -117.548215]]
        },
        "bottom_pnl_by_instruments": {
            "itd": [["ETH/USDT", 11.193017], ["ETH/BTC", 8.17276], ["DERIBIT-ETH-31MAY24-3500-P", 0], ["DERIBIT-ETH/USD-PERPETUAL", -1.024168]],
            "ytd": [["ETH/USDT", 11.193017], ["DERIBIT-ETH-31MAY24-3500-P", 0], ["DERIBIT-ETH/USD-PERPETUAL", -1.024168], ["ETH/BTC", -117.548215]],
            "mtd": [["ETH/USDT", 391.440054], ["DERIBIT-ETH-31MAY24-3500-P", 0], ["DERIBIT-ETH/USD-PERPETUAL", -0.985582], ["ETH/BTC", -117.548215]]
        },
        "top_pnl_by_exchanges": {
            "itd": [["deribit-6u5-2", 10.438461], ["deribit-6u5", 7.903148]],
            "ytd": [["deribit-6u5-2", 10.438461], ["deribit-6u5", -117.817827]],
            "mtd": [["deribit-6u5-2", 391.23657], ["deribit-6u5", -118.330313]]
        },
        "bottom_pnl_by_exchanges": {
            "itd": [["deribit-6u5-2", 10.438461], ["deribit-6u5", 7.903148]],
            "ytd": [["deribit-6u5-2", 10.438461], ["deribit-6u5", -117.817827]],
            "mtd": [["deribit-6u5-2", 391.23657], ["deribit-6u5", -118.330313]]
        }
    }
}


```

### Client Details

Name | Type | Description
--------- | ------- | -----------
client_name	|strin|g	Name of the client (null).
icon|	string|	Icon (null).
address	|string	|Address (null).
fund_type	|string	|Fund type (null).
strategy_name|	string	|Strategy name (null).
strategy_description	|string	|Strategy description (null).

### Chart Data


Name | Type | Description
--------- | ------- | -----------
Date	|string	|Date of the data point.
CumulativeReturn|	number	|Cumulative return at the date.
BtcCumulativeReturn|	number	|Bitcoin cumulative return at the date.

### PnL Mix
Name | Type | Description
--------- | ------- | -----------
SPOT|	number|	PnL from SPOT instruments.
OPTION|	number|	PnL from OPTION instruments.
PERPETUAL|	number	|PnL from PERPETUAL instruments.

### Strategy Metrics

Name | Type | Description
--------- | ------- | -----------
risk_rate|	number	|Risk rate associated with the strategy.
inception_date|	string	|Inception date of the strategy.
cum_return|	number	|Cumulative return of the strategy.
ytd_return|	number	|Year-to-date return of the strategy.
mtd_return|	number	|Month-to-date return of the strategy.
max_drawdown|	number|	Maximum drawdown of the strategy.
longest_dd	|number	|Longest drawdown period in days.
volatility	|number	|Volatility of the strategy.
win_rate	|number|	Win rate of the strategy.

### BTC Metrics

Name | Type | Description
--------- | ------- | -----------
risk_rate|	number	|Risk rate associated with the strategy.
inception_date|	string	|Inception date of the strategy.
cum_return|	number	|Cumulative return of the strategy.
ytd_return|	number	|Year-to-date return of the strategy.
mtd_return|	number	|Month-to-date return of the strategy.
max_drawdown|	number|	Maximum drawdown of the strategy.
longest_dd	|number	|Longest drawdown period in days.
volatility	|number	|Volatility of the strategy.
win_rate	|number|	Win rate of the strategy.

### Strategy vs. BTC


Name | Type | Description
--------- | ------- | -----------
alpha_itd	number	Alpha of the strategy compared to Bitcoin (inception to date).
alpha_ytd	number	Alpha of the strategy compared to Bitcoin (year-to-date).
alpha_mtd	number	Alpha of the strategy compared to Bitcoin (month-to-date).


### Return


Name | Type | Description
--------- | ------- | -----------
gross_itd|	number|	Gross Return on Equity (ROE) inception to date.
gross_ytd	|number|	Gross Return on Equity (ROE) year-to-date.
gross_mtd|	number|	Gross Return on Equity (ROE) month-to-date.
net_itd|	number	|Net Return on Equity (ROE) inception to date.
net_ytd|	number|	Net Return on Equity (ROE) year-to-date.
net_mtd	|number|	Net Return on Equity (ROE) month-to-date.

### Alpha


Name | Type | Description
--------- | ------- | -----------
bitcoin_itd	|number|	Benchmark alpha against Bitcoin inception to date.
bitcoin_ytd|	number	|Benchmark alpha against Bitcoin year-to-date.
bitcoin_mtd	|number|	Benchmark alpha against Bitcoin month-to-date.

### Exposure


Name | Type | Description
--------- | ------- | -----------
long%|	number|	Percentage of long positions.
short%|	number|	Percentage of short positions.
gross%	|number|	Gross exposure percentage.
net%|	number	|Net exposure percentage.

### Risk


Name | Type | Description
--------- | ------- | -----------
volatility|	number|	Volatility of the strategy.
correlation|	number|	Correlation with Bitcoin.
beta_crypto	|number	|Beta against a crypto index.
beta_btc|	number|	Beta against Bitcoin.
var|	number|	Value at risk.

### Risk Adjusted Return



Name | Type | Description
--------- | ------- | -----------
gross_sharpe_ratio|	number|	Gross Sharpe ratio of the strategy.
net_sharpe_ratio|	number|	Net Sharpe ratio of the strategy.
gross_sortino_ratio|	number|	Gross Sortino ratio of the strategy.
net_sortino_ratio|	number|	Net Sortino ratio of the strategy.
batting_average|	number|	Batting average (win rate) of the strategy.
payoff_ratio|	number|	Payoff ratio of the strategy.
profit_factor	|number	|Profit factor of the strategy.

### Drawdown



Name | Type | Description
--------- | ------- | -----------
max_drawdown|	number|	Maximum drawdown of the strategy.
longest_dd|	number|	Longest drawdown period in days.
average_drawdown|	number|	Average drawdown of the strategy.
average_dd|	number|	Average drawdown period in days.

### Win Loss



Name | Type | Description
--------- | ------- | -----------
batting_average|	number|	Batting average (win rate) of the strategy.
payoff_ratio|	number|	Payoff ratio of the strategy.
profit_factor	|number|	Profit factor of the strategy.

### Monthly Returns

Name | Type | Description
--------- | ------- | -----------
2023-11|	string	|Return percentage for November 2023.
2023-12|	string|	Return percentage for December 2023.





# DEX APIs
This document outlines the APIs used to fetch quotes and place orders for token swaps on decentralized exchanges (DEX). The supported algorithm type is SWAP, and the response contains information on the price and slippage.

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



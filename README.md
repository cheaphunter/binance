# Binance API client in Python

#### Features
- Does not require an api key for public methods
- Code is concise and clean
- Compatible with Python 2.7-3.6

#### Installation
```
pip install binance
```

#### Usage
```
import binance
```

For authenticated API calls, set your API key and secret
```
binance.set("your api key", "your secret key")
```

#### Get prices for all symbols
```
binance.prices()
```
Example response
```
{u'123456': u'0.00030000',
 u'ASTBTC': u'0.00005049',
 u'ASTETH': u'0.00092500',
 ...}
```

#### Get tickers for all symbols
```
binance.tickers()
```
Example response
```
{u'123456': {'ask': u'0.00000000',
  'askQty': u'0.00000000',
  'bid': u'0.00000000',
  'bidQty': u'0.00000000'},
 u'ASTBTC': {'ask': u'0.00005149',
  'askQty': u'3396.00000000',
  'bid': u'0.00004951',
  'bidQty': u'222.00000000'},
 ...}
```

#### Get order book
```
binance.depth("BNBBTC")
```
Example response
```
{'asks': {u'0.00022773': u'83.00000000',
  u'0.00022799': u'3347.00000000',
  u'0.00022800': u'3476.00000000',
  ...},
 'bids': {u'0.00020410': u'2000.00000000',
  u'0.00020450': u'6363.00000000',
  u'0.00020469': u'592.00000000',
  ...}}
```
Get top 5 levels only
```
binance.depth("BNBBTC", limit=5)
```

#### Get klines
```
binance.klines("BNBBTC", "1m")
```
Example response
```
[{'close': u'0.00023780',
  'closeTime': 1508472359999,
  'high': u'0.00023780',
  'low': u'0.00023768',
  'numTrades': 7,
  'open': u'0.00023769',
  'openTime': 1508472300000,
  'quoteVolume': u'0.06964315',
  'volume': u'293.00000000'},
 ...}]
```

#### Get balances for all currencies
```
binance.balances()
```
Example response
```
{u'123': {'free': u'0.00000000', 'locked': u'0.00000000'},
 u'456': {'free': u'0.00000000', 'locked': u'0.00000000'},
 u'ADX': {'free': u'0.00000000', 'locked': u'0.00000000'},
 ...}
```

#### Place order

Place 1000 lot buy order at 0.000001 on BNBBTC
```
binance.order("BNBBTC", binance.BUY, 1000, 0.000001)
```
Example response
```
{u'clientOrderId': u'fud8s7yw8o4wry7',
 u'executedQty': u'0.00000000',
 u'orderId': 123456789,
 u'origQty': u'1000.00000000',
 u'price': u'0.00000100',
 u'side': u'BUY',
 u'status': u'NEW',
 u'symbol': u'BNBBTC',
 u'timeInForce': u'GTC',
 u'transactTime': 1508502448246,
 u'type': u'LIMIT'}
```
Test an order to see if any errors are returned from the API. It will not actually place an order.
```
binance.order("BNBBTC", binance.BUY, 1000, 0.000001, test=True)
```
Example response
```
{}
```
Use a client id to identify the order later
```
binance.order("BNBBTC", binance.BUY, 1000, 0.000001, newClientOrderId="foobar")
```

#### Cancel order
```
binance.cancel("BNBBTC", orderId=123456789)
```
Example response
```
{u'clientOrderId': u'h67362qq3e9eaefe',
 u'orderId': 123456789,
 u'origClientOrderId': u'fud8s7yw8o4wry7',
 u'symbol': u'BNBBTC'}
```
Cancel using client id
```
binance.cancel("BNBBTC", origClientOrderId="foobar")
```

#### Get order status
```
binance.orderStatus("BNBBTC", orderId=123456789)
```
Example response
```
{u'clientOrderId': u'fud8s7yw8o4wry7',
 u'executedQty': u'0.00000000',
 u'icebergQty': u'0.00000000',
 u'orderId': 123456789,
 u'origQty': u'1000.00000000',
 u'price': u'0.00000100',
 u'side': u'BUY',
 u'status': u'NEW',
 u'stopPrice': u'0.00000000',
 u'symbol': u'BNBBTC',
 u'time': 1508502448246,
 u'timeInForce': u'GTC',
 u'type': u'LIMIT'}
```
Get using client id
```
binance.orderStatus("BNBBTC", origClientOrderId="foobar")
```

#### Get all open orders
```
binance.openOrders("BNBBTC")
```
Example response
```
[{u'clientOrderId': u'fud8s7yw8o4wry7',
  u'executedQty': u'0.00000000',
  u'icebergQty': u'0.00000000',
  u'orderId': 123456789,
  u'origQty': u'1000.00000000',
  u'price': u'0.00000100',
  u'side': u'BUY',
  u'status': u'NEW',
  u'stopPrice': u'0.00000000',
  u'symbol': u'BNBBTC',
  u'time': 1508502448246,
  u'timeInForce': u'GTC',
  u'type': u'LIMIT'},
 ...]
```

#### Get open and closed orders
```
binance.allOrders("BNBBTC")
```
Example response
```
[{u'clientOrderId': u'8u9ohoes8ryo',
  u'executedQty': u'10.00000000',
  u'icebergQty': u'0.00000000',
  u'orderId': 987654321,
  u'origQty': u'10.00000000',
  u'price': u'0.00020000',
  u'side': u'BUY',
  u'status': u'FILLED',
  u'stopPrice': u'0.00000000',
  u'symbol': u'BNBBTC',
  u'time': 1508333700089,
  u'timeInForce': u'GTC',
  u'type': u'LIMIT'},
 ...]
```

#### Get trades
```
binance.myTrades("BNBBTC")
```
Example response
```
[{u'commission': u'0.00500000',
  u'commissionAsset': u'BNB',
  u'id': 1484979,
  u'isBestMatch': True,
  u'isBuyer': True,
  u'isMaker': False,
  u'orderId': 987654321,
  u'price': u'0.00020000',
  u'qty': u'10.00000000',
  u'time': 1508333700089},
 ...]
```

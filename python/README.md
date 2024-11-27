# Virtex API Wrapper

This module provides a Python wrapper for the Virtex API, allowing you to interact with the Virtex platform programmatically. It includes methods for placing orders, retrieving market data, and managing WebSocket connections.

## Installation

```sh
pip install virtex
```

If you have cloned the repository, you need to install the required dependencies:

```sh
pip install -r requirements.txt
```

## Usage

### Initialization

To initialize the Virtex class, you need to provide your API key and secret. You can set these as environment variables or pass them directly to the init function.

```sh
export VIRTEX_API_HOST=demo.virtex.co
export VIRTEX_API_KEY=<your_key>
export VIRTEX_API_SECRET=<your_secret>

```python
from virtex import init

# Initialize with environment variables
instance = init()

# Initialize with custom host
instance = init('custom.virtex.co')
```

### Methods

#### new_order

Place a new order.

```python
instance.new_order(
    side="BUY",
    symbol="BTCUSD",
    quantity=1,
    price=50000,
    exDestination="binance",
    target_strategy="DMA",
    account=1
)
```

#### cancel

Cancel an existing order.

```python
instance.cancel(clOrdId="12345")
```

#### get_messages


Retrieve messages received from the WebSocket connection.

```python
messages = instance.get_messages()
print(messages)
```

#### listen_ws

Start listening to the WebSocket for real-time updates.

```python
instance.listen_ws(trace=True)
```

#### instruments

Retrieve information about available instruments.

```python
instruments = instance.instruments(symbol="BTCUSD")
print(instruments)
```

### Example 
Here's an example of how to use the Virtex class:

```python
from virtex import init
import logging

logging.basicConfig(encoding="utf-8", level=logging.INFO)

# Initialize the Virtex instance
instance = init('demo.virtex.co')

# Start listening to the WebSocket
instance.listen_ws()

# Place a new order
order = instance.new_order(
    side="BUY",
    symbol="BTCUSD",
    quantity=1,
    price=50000
)
print(order)

# Cancel an order
cancel_response = instance.cancel(order['orderId'])
print(cancel_response)

# Get messages from WebSocket
messages = instance.get_messages()
print(messages)

# Get instruments
instruments = instance.instruments(query={'base': 'BTC', 'quote': 'USDT'})
print(instruments)

instrument = instance.instruments(symbol="BTC-USD", venue="binance")
print(instrument)
```

## License
This project is licensed under the Apache License 2.0. See the LICENSE file for details.
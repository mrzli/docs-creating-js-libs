- for input parameters
  - have a readonly display, only display a larger form when 'Edit' is clicked (pencil icon, see order or trade item)

- implement forms
  - using react-hook-form
  - use zod for validation
  - implement first for trading parameters
    - all inputs are required
    - inputs
      - initial balance
        - number between 100 and 1,000,000
      - price decimals
        - integer between 0 and 8
      - spread
        - number between 0 and 10000
      - margin
        - number between 0 and 100
      - average slippage
        - number between 0 and 10000
      - pip digit
        - integer between -8 and 8
      - min stop loss
        - number between 0 and 10000
    - have placeholders for the above inputs describing the requirements
    - disable 'Apply' button if any input is invalid
    


- save trade state
  - instrument, resolution, timezone
  - trade inputs
    - parameters
    - manual trade actions
  - replay bar index
  - replay navigation timezone
- ui
  - have input name, then save, then 'Open'
  - 'Open' should toogle a 'open display' below the button
    - it should be a list of saved trade states
    - each item should have a 'Load' and 'Delete' buttons, maybe as a checkmark and a cross



- display logs



- create stub components
  - log
    - TradeLogList
    - TradeLogItem
      - each one will have
        - id
        - time (displayed as yyyy-MM-dd HH:mm in selected time zone)
      - manual-order
        - price
        - stopLoss
        - limit
        - amount
        - direction (Buy/Sell)
      - cancel-order
        - orderId
      - close-trade
        - tradeId
        - open time
        - close time
        - open price (from trade)
        - close price
        - amount
        - Buy/Sell
        - pnl points (calculate by using open and close price)
        - pnl (calculate by using open and close price, and amount)
      - adjust-order
        - orderId
        - old price, stopLoss, limit, amount
        - new price, stopLoss, limit, amount
      - adjust-trade
        - tradeId
        - old stopLoss, limit (price, not offset)
        - new stopLoss, limit (price, not offset)
      - order-fill
        - orderId
        - price
        - stopLoss (price, not offset)
        - limit (price, not offset)
        - amount
        - direction (Buy/Sell)
      - stop-loss
        - tradeId
        - open time
        - close time
        - open price (from trade)
        - close price
        - stopLossPrice (price, not offset)
        - amount
        - Buy/Sell
        - pnl points (calculate by using open and close price)
        - pnl (calculate by using open and close price, and amount)
      - limit
        - tradeId
        - open time
        - close time
        - open price (from trade)
        - close price
        - limitPrice (price, not offset)
        - amount
        - Buy/Sell
        - pnl points (calculate by using open and close price)
        - pnl (calculate by using open and close price, and amount)

  

- action log
  - make market order (manual)
  - make limit order (manual)
  - cancel limit order (manual)
  - close trade (manual)
  - adjust order (manual)
  - adjust trade (manual)
  - limit order triggered -> trade opened (automatic)
  - limit or stop-loss triggered in trade -> trade closed (automatic)









- example flow
  - open trade
    - trade shows in list of orders, or directly in trades if it is a market order
    - once the trade is filled, it shows in the list of trades, if it is a limit order
  -  cancel order
    - order is cancelled, and removed from the list of orders, not visible any more
  - close trade
    - trade is closed, and removed from the list of trades, not visible any more
    - trade is added to the list of completed trades
    - result is adjusted


- controls
  - implement tab control
    - Sequence
      - TradeSequenceInputs
    - Trading
      - ability to make order
      - list of open orders and trades
    - Result
      - list of completed trades
      - result display
  - order entry
    - buy/sell toggle button, at first, both are disabled
  - order item
    - created time (ts first, later timezoned date)
    - type (buy, sell)
    - price
    - amount
  - open trade item
    - open/close time (ts first, later timezoned date)
    - type (buy, sell)
    - open price
    - amount
  - completed trade item
    - open/close time
    - type (buy, sell)
    - open price
    - close price
    - amount
    - pnl points
    - pnl
  - result
    - see below

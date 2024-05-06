- from outside
  - input
    - canvas
    - data
  - state
    - position: SeriesPosition
    - priceRange: Range
  



- priceAxisPipeline
  - input
    - position
    - axisLength
    - data
    - timezone

  - pipeline
    - get tick values
    - filter tick values, so t





- canvas chart
  - input
    - chart dimensions
      - padding
      - chart width/height
      - x-axis height (number or auto)
        - should be a simple calculation based on font size (maybe exactly equal to font size)
      - y-axis width (number or auto)
        - if auto, calculate based on below description
        - number for calculation
          - maybe use last price times 10, and round up to the nearest 5 pixes (experiment and see what works)
    - data
      - array of ohlc data
        - time
        - ohlc
        - volume (can be undefined)
    - position on chart
      - right item (fractional)
      - item width (fractional, but use a whole number for rendering) OR item span (fractional)
        - calculate the other for the first and chart area width
      - y-range in price


- grid adjustments
  - price
    - min y-distance is 30
    - examples:
      - YM (Dow Jones Future):
        - 10000, 5000, 4000, 2500, 2000, 1000, 500, 400, 250, 200, 100, 50, 40, 25, 20, 10, 5, 4, 2, 1
          - on tradingview, there is no fraction for this instrument, so no division beyond 1
      - EUR/USD:
        - 10, 5, 4, 2.5, 2, 1, 0.5, 0.2, 0.1, 0.5, 0.2, 0.1, 0.05, 0.02, 0.01, 0.005, 0.002, 0.001, 0.0005, 0.0002, 0.0001, 0.00005, 0.00002, 0.00001
          - no division beyond 0.00001
  - time
    - min x-distance is 80
    - details:
      - accept
        - bar offset and span
        - axis length
        - data
        - interval
        - timezone
      - notes
        - intervals at 1D and above are not affected by the timezone, UTC is used
      - algorithm
        - take the data range visible, extend it to the right if necessary
        - if interval is Y
          - simply show years starting from first fully visible bar, such that the min x-distance is satisfied
        - if interval is M
          - same as above
          - if each year is shown
            - check whether
              - 1 month is greater than min x-distance
                - show each month
              - or only 3 months is greater than min x-distance
                - show April, July, October (checking for each that it is greater than min x-distance on both ends, because in theory there could be missing months)
              - 6 months is greater than min x-distance
                - show July (with check as above)
        - if interval is W
          - checks same as above for year/month
          - if each month is shown
            - check whether you can show first available day inside week so that min x-distance is satisfied
        - if interval is D
          - same as for week, although you don't need to look for start of week, check for first day where min x-distance is satisfied on both ends etc
        - if interval is h
          - same as for week and day, for hours just do sequenatial as available
        - if interval is m
          - same as for week, day
          - for 30 minutes
            - check whether the first interval is at the quarter hour (could happen due to timezone)
              - if yes, just do sequential
            - if no
              - check if you can show
                - check min amount of bars that are over min x-distance
                - use that to determine whether to show 30m, 1h, 2h, 3h, 4h, 6h, 8h or 12h ticks
                - for each tick, additionally check, to make sure that any missing bar don't condense the display too much
          - for 15m
            - same as for 30m (without tz issues), but additionally check for 15m ticks
          - for 10m
            - same as for 30m, but additionally check for 10m ticks
          - for 5m
            - same as for 15m, but additionally check for 10m and 5m ticks
          - for 1m
            - same as for 5m, but additionally check for 2m and 1m ticks
        - if interval is s
          - same as for 1m, put in s as space allows, sequentially
            


- check performance of 'measure string'
  - if it is too slow, you can use the following heuristic
    - for 12px font
      - 1 digit is 7px width
      - space and dot is 3px width
      - height is 12px
    - if you use other font sizes, you can calculate the ratio
    - if you use pipette of smaller font size
      - try using the same measurement as above
      - if that is not accurate enough, do a separate measurement for the pipette font size




- implement just the visual chart
  - keep it as simple as possible
  - have event handlers
  - have padding
  - have fixed (provided) x-axis area height and y-axis area width
  - have x-axis ticks
    - just the position (relative x-coord) and label
  - have y-axis ticks
    - just the position (relative y-coord) and label
  - have visual candle data
    - just x, y1-y4, color


- internal chart control
  - implement vertical ticks
    - 0.1, 0.2, 0.5, 1, 2, 5, 10, 25, 50, 100, 250, 500, 1000
    - min height 30px
  - update horizontal ticks
    - implement dynamic grid/axis tick spacing, based on width
    - show data
      - reduce grid and axis tick density
        - stops
        - 1/2/5/10/15/30 min
        - 1/2/3/4/6/8/12 h
        - 1/2/3/5/10/15 days
        - 1/2/3/4/6 months
        - 1/2/5/10 years
      - determine minimum width between ticks
        - additionally remove ticks to match stops
        - for example, if we have 15 day steps, and looking at Jan,
          you probably want to have a step for beginning of Jan ('Jan', then +15 days for '16', and then instead of '31', have it at 'Feb')



- improve the component
  - change how chart works
	  - chart should just show 50 by default
	  - try to render all of them at first, and see the performance
	    - later see where they fit on the screen and simply avoid rendering the ones that are outside of bounds on x-axis
	- add option for setting a date of the chart
	  - it should return 1000+ entries before and after
	  - put the candle on the date at position 30 or so (slighly more to the right),
	- later on, limit chart zoom to at most show 200 entries at once


  - implement dragging while not adding anx x-ticker other than the existing
    - but properly seeing y-tickers change
  
  - improve chart navigation
    - https://www.tradingview.com/chart/aDGjCOdC/?symbol=SKILLING%3ADE40
	- you will probably need to make the chart navigation continous (smooth), instead of discrete
	  - this will allow better scrolling and zooming
	- you will need to be able to drag the chart on x and y
	- change width with mouse scroll
	- change width by drag-drop on the bottom axis (this has the same effect as mouse scroll, and is anchored to the right of the chart)
	  - change the mouse pointer when over to left-right
	- change height by drag-drop on the y-axis, anchored to the middle of the chart
	  - change the mouse pointer when over to up-down
- 
  


- on the backend, implement an endpoint for fetching data
  - input for fetching data
    - ticker
    - interval (for now just 1-minute, 15-minute, 1-day)
    - start date (optional, default is beginning of time)
    - end date (optional, default is end of time)
  - return is an array of csv rows




- structure ticker data
  - 5000 entries is the cutoff for the data per file, roughly speaking
  - by default I have 1-minute, 15-min, 1-day data
  - I need to expand to get 5-minute, 10-minute, 30-minute, 1-hour, 4-hour, 1-week, 1-month
  - types
    - 1-minute
      - by day
    - 5-minute
      - by-day
    - 10-minute
      - by-month
    - 15-minute
      - by-month
    - 30-minute
      - by month
    - 1-hour
      - by year
    - 4-hour
      - by year
    - 1-day
      - by year
    - 1-week
      - by decade
    - 1-month
      - by decade
- functionality
  - have data downloader
  - have function to get list of files
    - input directory, the search all csv files that are direct ancestors
  - have function to join data
    - simply concatenates lists of rows in each file in the subfolder
  - have function to split data
    - accept data list
    - returns a list of lists
  - have function to merge data list with existing data
    - need to take just the last file in existing data
    - merge it with new data list (which will have 1 or more files)
  - have a function to convert smaller interval data to larger interval
  - have a repository that stores the data

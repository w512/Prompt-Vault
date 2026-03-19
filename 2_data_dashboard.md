# Live data dashboard

Create a single self-contained `index.html` file — a live stock market dashboard using the **Alpha Vantage API**.

**API key placeholder:** put `YOUR_API_KEY` as a constant at the very top of the script so it's easy to replace.

**Dashboard should include:**

1. **Search bar** — user types a stock ticker (e.g. AAPL, TSLA, MSFT) and hits Enter or clicks "Search"

2. **Stock header card** showing:
   - Company ticker & name
   - Current price
   - Price change (absolute + percentage), colored green/red accordingly
   - Volume

3. **Interactive price chart** (use Chart.js from CDN):
   - Line or area chart showing intraday price data (use `TIME_SERIES_INTRADAY`, interval `5min`)
   - Smooth curve, gradient fill under the line
   - Tooltips on hover showing exact price and timestamp

4. **Auto-refresh** every 60 seconds with a visible countdown timer showing when the next refresh happens

5. **Multi-ticker watchlist** on the side:
   - User can add/remove tickers
   - Each watchlist item shows current price + % change (green/red)
   - Clicking a ticker loads it into the main chart

6. **Top bar with market status** — show whether the US market is currently open or closed based on time (Eastern Time)

**Design requirements:**
- Dark theme (deep navy / charcoal background)
- Glassmorphism cards with subtle borders and shadows
- Clean modern font (use Google Fonts — Inter or Manrope)
- Smooth transitions and hover effects
- Fully responsive layout

All in one HTML file. Use Chart.js and any other needed libraries from CDN. The dashboard must work correctly in a browser by simply opening the file and replacing `YOUR_API_KEY`.



# Cryptocurrency Trading Bot

This repository contains a cryptocurrency trading bot that uses the Coinbase API, TradingView technical analysis, and the Stochastic RSI strategy to automate buying and selling of cryptocurrencies. The bot operates on a custom backtesting framework and uses real-time data from Coinbase and TradingView to make trading decisions.

## Project Overview

This project is designed to automate cryptocurrency trading based on technical analysis indicators. The bot leverages the **Stochastic RSI (Stoch RSI)** indicator, a popular tool used in technical analysis to identify overbought or oversold conditions. It then executes market orders on Coinbase based on these indicators, with the help of the **Coinbase API**.

### Key Features:
- **Stochastic RSI Strategy**: The bot uses the Stochastic RSI to generate buy or sell signals based on overbought and oversold conditions.
- **Coinbase API Integration**: The bot connects to Coinbase for real-time price data and executes buy/sell orders.
- **TradingView Integration**: The bot retrieves market analysis data from TradingView to enhance the trading decisions.
- **Excel Logging**: Every transaction, including price, Stoch RSI values, and action, is logged into an Excel file for record-keeping.
- **Customizable Investment**: Users can specify their initial investment and trade size.

## File Structure

```plaintext
.
├── indicator_calculations/
│   └── tradinvview_tester.py
├── coinbase_advanced_trade_bot/
│   ├── backtesting_functions/
│   │   └── calculate_stoch_rsi.py
│   ├── coinbase_functions/
│   │   ├── backend_purchase_functions/
│   │   │   ├── market_order_buy.py
│   │   │   └── market_order_sell.py
│   │   ├── get_product_price.py
│   │   └── main/
│   │       └── cb_auth.py
├── trading_bot.py
└── market_data.xlsx
```

## Installation

### Prerequisites:
Before running the bot, ensure you have the following Python packages installed:
- `coinbase`
- `tradingview-ta`
- `pandas`
- `openpyxl`
- `requests`
- `time`

You can install these dependencies using `pip`:

```bash
pip install coinbase tradingview-ta pandas openpyxl requests
```

### Setting Up the Project:
1. Clone the repository to your local machine.
   
   ```bash
   git clone https://github.com/yourusername/cryptocurrency-trading-bot.git
   ```

2. Navigate to the project directory.

   ```bash
   cd cryptocurrency-trading-bot
   ```

3. Create a new API key and secret from your Coinbase account and keep them handy for later use.

## Usage

### Running the Trading Bot:
1. In the terminal, navigate to the project folder.
2. Run the trading bot by executing the following command:

   ```bash
   python trading_bot.py
   ```

3. The bot will prompt you for the following information:
   - **Coinbase API Key**: Your API Key from Coinbase.
   - **Coinbase API Secret**: Your API Secret from Coinbase.
   - **Crypto Market**: The market you want to trade (e.g., `BTC-USDC`).
   - **Initial Investment**: The amount of money you want to start trading with.

4. The bot will begin checking signals, executing trades, and logging actions to an Excel file.

### Example Output:
The trading bot will print actions, amounts, prices, and Stoch RSI values to the console. Example:

```plaintext
Action: BUY, Amount: 100.0, Price: 20000.0, Stoch RSI K: 25.7
```

### Logging:
All market data and trades are logged to an Excel file (`market_data.xlsx`). This file contains columns:
- **Timestamp**: The time of the transaction.
- **Market**: The market pair (e.g., BTC-USDC).
- **Price**: The price at which the trade was executed.
- **Stoch RSI K**: The value of the Stochastic RSI K at the time of the trade.
- **Action**: The action performed (BUY/SELL).
- **Amount**: The amount of cryptocurrency bought or sold.

### TradingView Integration:
The bot uses TradingView's technical analysis API to fetch technical indicator data. You can view the specific indicators and their values using the `tradinvview_tester.py` script within the `indicator_calculations/` folder. This is mainly for testing purposes and to analyze which indicators are being used.

#### Example of usage in `tradinvview_tester.py`:
```python
from tradingview_ta import TA_Handler, Interval

class CryptoAnalysis:
    def __init__(self, symbol='BTCUSDT', screener='crypto', exchange='Coinbase', interval=Interval.INTERVAL_1_HOUR):
        self.handler = TA_Handler(
            symbol=symbol,
            screener=screener,
            exchange=exchange,
            interval=interval
        )

    def get_indicator_values(self):
        indicators = self.handler.get_analysis().indicators
        for key, value in indicators.items():
            print(f'{key}: {value}')

    def indicator_summary(self):
        summary = self.handler.get_analysis().summary
        print(summary)

crypto_analyzer = CryptoAnalysis()
crypto_analyzer.indicator_summary()
crypto_analyzer.get_indicator_values()
```

## Backtesting

For backtesting the **Stochastic RSI** strategy, you can refer to the `calculate_stoch_rsi.py` file under `coinbase_advanced_trade_bot/backtesting_functions/`. This file contains functions to calculate the Stochastic RSI values for historical market data.

### Backtest Example:
The bot can be extended with a backtesting framework by importing and using the `get_stoch_rsi()` function to evaluate the strategy using historical data before live trading.

```python
from coinbase_advanced_trade_bot.backtesting_functions.calculate_stoch_rsi import get_stoch_rsi
```

## Contributing

If you'd like to contribute to this project, please feel free to submit a pull request. Here are a few ways you can contribute:
- **Bug Fixes**: If you spot a bug, feel free to create an issue or fix it yourself and submit a pull request.
- **Enhancements**: Suggest and implement new features to improve the bot's performance or functionality.
- **Documentation**: Help improve the project documentation.

## License

This project is open-source and available under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Disclaimer

Use this bot at YOUR OWN RISK. Cryptocurrency trading is HIGHLY speculative and involves substantial risk. The creator is not responsible for any financial loss incurred through the use of this bot. Always do your own research before making any trades.

---

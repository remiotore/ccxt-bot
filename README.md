# Crypto Trading Bot

A Python-based automated cryptocurrency trading bot that uses technical analysis indicators (RSI and Bollinger Bands) to execute trades on Binance exchange with Telegram notifications.

## Features

- **Automated Trading**: Executes trades based on RSI and Bollinger Bands strategy
- **Multiple Timeframes**: Supports 1m, 5m, and 15m timeframes
- **Risk Management**: Configurable take profit (TP) and stop loss (SL) percentages
- **Telegram Integration**: Real-time notifications for trade entries, exits, and status updates
- **Data Persistence**: Saves historical data and current trade state
- **Logging**: Comprehensive logging for debugging and monitoring

## Strategies

The bot uses a combined RSI and Bollinger Bands strategy:

### Entry Conditions
- **Long Entry**: RSI(6) < 30 AND RSI(12) < 30 AND price < Bollinger Band Lower
- **Short Entry**: RSI(6) > 70 AND RSI(12) > 70 AND price > Bollinger Band Upper

### Exit Conditions
- **Take Profit**: Configurable percentage gain (default: 1.5%)
- **Stop Loss**: Configurable percentage loss (default: 0.75%)
- **RSI Cross**: Exit when RSI(6) crosses RSI(12) in opposite direction

## Installation

### Prerequisites
- Python 3.8 or higher
- TA-Lib library (requires compilation)

### Install TA-Lib
```bash
# Ubuntu/Debian
sudo apt-get install build-essential
wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz
tar -xzf ta-lib-0.4.0-src.tar.gz
cd ta-lib/
./configure --prefix=/usr
make
sudo make install

# macOS
brew install ta-lib

# Windows
# Download and install from: https://github.com/cgohlke/talib-build/releases
```

### Install Python Dependencies
```bash
pip install ccxt ta-lib pandas requests
```

## Configuration

### Telegram Bot Setup
1. Create a Telegram bot by messaging [@BotFather](https://t.me/botfather)
2. Get your bot token
3. Get your chat ID by messaging [@userinfobot](https://t.me/userinfobot)

### Bot Configuration
The bot can be configured with the following parameters:

```python
bot = CryptoBot(
    symbol="BTC/USDT",           # Trading pair
    timeframe="5m",              # Candle timeframe (1m, 5m, 15m)
    telegram_token="YOUR_TOKEN", # Telegram bot token
    telegram_chat_id="YOUR_ID",  # Telegram chat ID
    tp_pct=1.5,                  # Take profit percentage
    sl_pct=0.75,                 # Stop loss percentage
    strategy_name="rsi_bollinger" # Strategy to use
)
```

## Usage

### Running the Bot
```python
from bot import CryptoBot

# Initialize the bot
bot = CryptoBot(
    symbol="BTC/USDT",
    timeframe="5m",
    telegram_token="your_telegram_token",
    telegram_chat_id="your_chat_id"
)

# Start trading
bot.run()
```

### Jupyter Notebook
The bot can also be run from the included Jupyter notebook (`bot.ipynb`):

1. Open the notebook
2. Configure your parameters in the second cell
3. Run all cells

## File Structure

```
crypto-bot/
├── bot.ipynb           # Jupyter notebook with bot code
├── README.md           # This file
├── requirements.txt    # Python dependencies
├── logs.txt           # Bot execution logs
└── data/              # Data storage directory
    ├── BTCUSDT/       # Symbol-specific data
    │   ├── 1m.csv     # Historical price data
    │   └── trade.json # Current trade state
    └── XRPUSDT/
        ├── 1m.csv
        └── 5m.csv
```

## Data Management

- **Historical Data**: OHLCV data is stored in CSV files for each symbol/timeframe
- **Trade State**: Current trade information is persisted in JSON format
- **Logs**: All bot activities are logged to `logs.txt`

## Risk Disclaimer

⚠️ **WARNING**: This is experimental software for educational purposes.

- **Use at your own risk**: Cryptocurrency trading involves substantial risk
- **Test thoroughly**: Always test with small amounts first
- **No guarantees**: Past performance does not guarantee future results
- **Monitor actively**: Keep track of your bot's performance
- **Start small**: Begin with minimal capital

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is provided as-is for educational purposes. Use responsibly.

## Support

For issues and questions:
1. Check the logs in `logs.txt`
2. Verify your Telegram configuration
3. Ensure TA-Lib is properly installed
4. Check exchange connectivity

## Changelog

### v1.0.0
- Initial release with RSI/Bollinger Bands strategy
- Telegram notifications
- Basic risk management
- Data persistence

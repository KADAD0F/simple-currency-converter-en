# Currency Converter en

## Description
A currency converter with offline support that allows converting amounts between various currencies using up-to-date exchange rates. The script automatically fetches data from APIs, saves it locally, and can operate without an internet connection by using cached data.

## Features
- **Offline mode**: Automatic use of locally saved data when internet is unavailable
- **Multi-layer data validation**: Integrity checks for API responses and local data
- **Error protection**: Maximum amount limit to prevent arithmetic errors
- **Visual interface**: Progress bar for data loading process
- **20+ currency support**: With full names in English
- **Update date display**: Shows date of last rates update
- **Data freshness check**: Automatic warning when using outdated rates (older than 7 days)

## Requirements
- Python 3.6 or higher
- Dependencies:
  - `requests` (for HTTP requests)
  - `locale` (for localization)

## Installation
1. Install dependencies:
```bash
pip install requests
```
2. Save the script as `offline_currency_converter_en.py`

## Configuration
You can modify configuration parameters at the beginning of the script:

```python
# Path to local database file
DB_FILE = "currency_rates.json"

# List of API sources for data retrieval
API_URLS = [
    "https://api.exchangerate-api.com/v4/latest/USD",
    "https://api.exchangerate-api.com/v4/latest/EUR"
]

# Maximum conversion amount
MAX_AMOUNT = 1_000_000_000

# Dictionary with currency names
CURRENCY_NAMES = {
    "USD": "US Dollar",
    "EUR": "Euro",
    # ... other currencies
}
```

## Usage
Run the script:
```bash
python offline_currency_converter_en.py
```

After launch:
1. The script checks internet connectivity and updates data if available
2. Displays data status (current/outdated/unavailable)
3. Shows available currencies with numbers
4. Asks for source currency, amount, and target currency
5. Performs conversion and displays the result

## Code Structure

### Main Functions
- `check_internet()`: Checks internet availability through multiple reliable sources
- `fetch_rates()`: Fetches current exchange rates from API
- `load_db()`: Loads data from local database
- `save_db(data)`: Saves data to local database
- `is_data_fresh(data)`: Checks data freshness
- `get_available_currencies(rates_data)`: Gets list of available currencies
- `get_user_amount()`: Validates user input amount
- `perform_conversion()`: Performs conversion with validation
- `main()`: Main application logic

### Error Handling
- **Network errors**: Multi-source verification and fallback to backup sources
- **Data errors**: JSON structure validation and currency rate verification
- **Input errors**: Amount validation and currency selection validation
- **Critical errors**: Exception handling with user-friendly messages

## Example of Operation
```
Checking database..
Updating data.. [██████████████████████████████]

✓ Data successfully updated, exchange rates as of 07/08/2025.

Welcome to the currency converter!
This application uses internet to update the database, but it's not required as we'll use previously downloaded data if needed. To convert currency, select source currency:

Available currencies (remember the numbers, they'll be needed for selecting both currencies):
1. US Dollar (USD)
2. Euro (EUR)
3. Russian Ruble (RUB)
...

-> Select source currency (number from the list above): 1

Got it, currency "US Dollar", what amount?
-> 100

-> Select target currency (number from the list above): 3

==================================================
Conversion result:
100.00 US Dollar (USD)
→ 8,520.00 Russian Ruble (RUB)
Rates as of 07/08/2025
==================================================

Great! The conversion is complete.

Would you like to perform another conversion? (yes/no): 
```

## Critical Situation Handling
- **No internet**: Automatic fallback to local data
- **Outdated data**: Warning when using data older than 7 days
- **Missing required currencies**: Checks for USD, EUR and RUB
- **Same currency conversion**: Prevents meaningless operations
- **Zero/negative amount**: Input validation

## Data Information
- **Data sources**: ExchangeRate-API.com (multiple reliable sources)
- **Data type**: Indicative midpoint rates
- **Update frequency**: Data updates daily
- **Storage duration**: Local data stored for up to 7 days, after which it's marked as outdated

## Testing
- **Automated tests**: 100% coverage of main scenarios
- **Platforms**:
  - Windows 10 21H2
  - Kali Linux (2025.2)
  - Termux (Android 12+)
- **Verified scenarios**:
  - Working with different currencies
  - Network error handling
  - Boundary value conversion
  - Special character display

## Version and License
- **Version**: 1.0
- **Release date**: 08/25/2025
- **License**: No

## Note
This script uses data from ExchangeRate-API.com, which are indicative and not intended for financial transactions requiring high precision. For commercial use, please review the API provider's terms of service.

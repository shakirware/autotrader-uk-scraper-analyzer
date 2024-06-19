autotrader-uk-scraper-analyzer is a Python-based web scraping tool designed to collect and analyze car details from AutoTrader UK. It downloads car images, detects number plates, retrieves MOT history, and calculates a total score for each car based on various parameters. The data is saved into an Excel spreadsheet for further review and analysis.

## Features

- Download car images and detect number plates.
- Retrieve car details such as name, type, price, mileage, registration year, seller, and location.
- Extract MOT history and calculate MOT scores.
- Calculate and normalize scores for price, mileage, registration year, and MOT.
- Save all data to an Excel spreadsheet for easy review and analysis.

## Prerequisites

- Python 3.7 or higher
- Google Cloud Vision API credentials (JSON file)
- Chrome WebDriver

## Installation

1. **Clone the repository:**

    ```sh
    git clone https://github.com/yourusername/AutoTraderScraper.git
    cd AutoTraderScraper
    ```

2. **Install required Python packages:**

    ```sh
    pip install -r requirements.txt
    ```

3. **Set up Google Cloud Vision API:**

    - Create a Google Cloud Project.
    - Enable the Vision API.
    - Create a service account and download the JSON key file.
    - Save the JSON key file in the project directory.

4. **Download Chrome WebDriver:**

    - Download the Chrome WebDriver corresponding to your Chrome browser version from [here](https://sites.google.com/chromium.org/driver/).
    - Place the WebDriver executable in the project directory or specify the path in the script.

## Usage

1. **Prepare a text file with AutoTrader links:**

    - Create a text file named `links.txt` in the project directory.
    - Add one AutoTrader UK car detail link per line in the text file.

2. **Run the scraper:**

    ```sh
    python autotrader_scraper.py
    ```

    - The script will read the links from `links.txt`, scrape the car details, and save the data to `autotrader_uk_details.xlsx`.
    - Review the spreadsheet for any missing or incorrect data.

3. **Update car scores:**

    - After reviewing the initial data, press Enter to continue with updating car scores.
    - The script will fetch MOT details, calculate scores, and update the spreadsheet `updated_autotrader_uk_details.xlsx`.

## Detailed Functionality

### Initialization

```python
scraper = AutoTraderScraper(service_account_file='service-account-file.json', chrome_driver_path=r".\chromedriver.exe")
```
  - service_account_file: Path to your Google Cloud Vision API JSON credentials.
  - chrome_driver_path: Path to your Chrome WebDriver executable.

### Screenshot
Here's an example of the final spreadsheet output:

![Final Spreadsheet](https://imgur.com/x74pBMZ.png)

### Scoring System

The scoring system evaluates each car based on the following parameters:

- **Price Score:** Calculated by normalizing the car's price against the range of prices in the dataset.
- **Mileage Score:** Calculated by normalizing the car's mileage against the range of mileages in the dataset.
- **Year Score:** Calculated by normalizing the car's registration year against the range of years in the dataset.
- **MOT Score:** Calculated based on the MOT history, including factors such as advisories and failures.

Each parameter is weighted to compute the total score for each car. The weights are defined as follows:

- **Price:** 30%
- **Mileage:** 20%
- **Registration Year:** 20%
- **MOT:** 30%

# Data Visualization Project: COVID-19 & Population Demographics

A Python-based data visualization project that analyzes COVID-19 statistics and population demographics across multiple countries to identify correlations between age distribution and pandemic outcomes.

## Overview

This project combines real-time COVID-19 data with demographic information to create visualizations comparing:
- Population age distribution (under 35 and over 65 years old)
- COVID-19 case rates and death rates
- Correlations between age demographics and pandemic impact

## Features

- **Data Collection**: Fetches current COVID-19 data from the disease.sh API and population demographics from the U.S. Census Bureau API
- **Database Management**: Stores normalized data in SQLite for efficient querying and analysis
- **Data Visualization**: Generates horizontal bar charts comparing statistics across six countries: Canada, Japan, Australia, Chile, Kenya, and France
- **Data Analysis**: Calculates and exports key statistical comparisons to JSON format

## Project Structure

```
├── covid.py                 # Fetches COVID-19 data from public API
├── population.py            # Retrieves population demographic data
├── database.py              # Creates and populates SQLite database
├── visualization.py         # Generates charts and visualizations
├── database.db              # SQLite database with normalized data
├── population_data.csv      # Population demographic data
├── calculations.txt         # Exported calculation results (JSON format)
└── README.md               # Project documentation
```

## Module Descriptions

### `covid.py`
Retrieves current COVID-19 statistics from the [disease.sh API](https://disease.sh/v3/covid-19/countries).
- **Function**: `get_covid_data()`
- **Returns**: List of dictionaries containing country name, cases, deaths, and active cases
- **Output**: Sorted alphabetically by country name

### `population.py`
Fetches population demographic data from the U.S. Census Bureau API for 2021.
- **Function**: `get_population_data()`
- **Metrics Extracted**:
  - Total population
  - Population under 35 years old
  - Population over 65 years old
- **Output**: CSV file and sorted list of dictionaries by country name

### `database.py`
Manages SQLite database creation and data insertion.
- **Key Functions**:
  - `set_up_database()`: Initializes database connection
  - `create_country_code_table()`: Creates normalized country reference table
  - `add_country_code()`: Populates country codes
  - `add_covid_country()`: Inserts COVID-19 statistics
  - `add_population()`: Inserts population demographics
  - `make_master_list()`: Ensures data consistency across datasets
- **Database Schema**:
  - `codes`: Country name and ID mappings
  - `covid`: Country ID with cases, deaths, and active cases
  - `population`: Country ID with age demographic breakdowns

### `visualization.py`
Generates comparative bar charts and calculates statistics.
- **Key Functions**:
  - `join_tables()`: Combines data from all database tables
  - `over_65()`: Creates visualizations for population over 65 and COVID-19 death rates
  - `under_35()`: Creates visualizations for population under 35 and COVID-19 case rates
  - `write_calc()`: Exports calculations to JSON file
- **Output**: Multiple matplotlib charts and calculations.txt JSON file

## Installation & Requirements

### Dependencies
```
requests
sqlite3
matplotlib
csv
json
```

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/leenahk/206-final-project.git
   cd 206-final-project
   ```

2. Install required packages:
   ```bash
   pip install requests matplotlib
   ```

3. Run the pipeline:
   ```bash
   # Step 1: Set up database and populate data
   python database.py
   
   # Step 2: Generate visualizations
   python visualization.py
   ```

## Usage

### Run Individual Modules
- **Get COVID-19 data**: `python covid.py`
- **Get population data**: `python population.py`
- **Setup database**: `python database.py`
- **Generate visualizations**: `python visualization.py`

### Output
- **Charts**: Interactive matplotlib visualizations comparing demographics and COVID statistics
- **Data Export**: `calculations.txt` containing JSON-formatted calculations for further analysis

## Countries Analyzed
- Canada
- Japan
- Australia
- Chile
- Kenya
- France

## Data Sources
- **COVID-19 Data**: [disease.sh COVID-19 API](https://disease.sh/v3/covid-19/countries)
- **Population Demographics**: [U.S. Census Bureau International Database](https://api.census.gov/data/timeseries/idb/5year)

## Key Insights
The project enables analysis of:
- How age demographics correlate with COVID-19 case and death rates
- Whether countries with older populations experienced higher mortality rates
- Regional pandemic impact variations based on population structure

## License
This project is provided as-is for educational purposes.

## Notes
- Data is fetched from public APIs at runtime; internet connection required
- Database updates with the latest COVID-19 statistics each time `database.py` is run
- Visualizations display data for six selected countries; can be modified in `visualization.py`

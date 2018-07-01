# Bubble Tea in California

The purpose of this project was to collect data regarding bubble tea shops in California and do some exploration around that data.
I acquired bubble tea business information using the YelpAPI and piped the data into a PostgreSQL database. Once the data was ingested,
I exported the data into two datasets (bubble_tea.csv and hours.csv within the csvs directory). These two datasets were used for some
data exploration in a Jupyter notebook (exploration.ipynb). Some plots and maps generated by the data exploration are stored in the html
and png directory. I also hosted the combined html output on  GitHub pages, and that can be found here: https://cabubbletea.github.io/
![alt text](./png/bubble_tea_ca_map.png)

## Getting Started

It's possible to set up your environment to insert bubble tea business information into a PostgreSQL database as well.

### Prerequisites

PostgreSQL, Python3, and a Yelp API key are required to run the code.

To download PostgreSQL, see https://www.postgresql.org/download/

To download Python, see https://www.python.org/getit/

For information regarding obtaining a Yelp API key, see https://www.yelp.com/developers/faq

### Installing

To install the required packages, run

```
pipenv install
```

To setup your PostgreSQL database (assuming localhost) with the required tables, functions, triggers, and views, run

```
psql -U <username> -f seed.sql
```

It's also possible to pass in a flag for host (_-h_) and port (_-p_) if running _seed.sql_ on a different machine.

## Setup

Either export your Yelp API key to an environment variable named _YELP_API_KEY_ or
change the value of the `YELP_API_KEY_` variable in _settings.py_

Within _settings.py_, update the `DATABASE` variable to reflect your database credentials
(if running localhost, most likely only need to update the database _password_)

Right now, in _settings.py_, the `STATE` variable is set to `CA` for California.
However, it's possible to import bubble tea locations from other states by
setting the value of this variable to another state abbreviation.

It's also possible to import bubble tea business hour information into the database (stored in the hours table)
if the `IMPORT_HOURS` variable in _settings.py_ is set to `True`.

## Importing Data

To begin importing data into your database, run

```
python bubble_tea.py
```

Please note that the Yelp API is limited to 25,000 API calls a day, so any attempted API calls after
will not return any data.

## Exporting Data

Running the following command will export the results of the _bubble_tea_w_fips_ view to ./csv/bubble_tea.csv
and the _bubble_tea_w_hours_ view to ./csv/hours.csv

```
psql -U <username> -f export.sql
```

However, it's possible to modify export.sql to export any dataset to any location by changing the SELECT statement and output path respectively.

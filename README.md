# seloger-google-sheets

Tired of searching with your mouse ? Let's automate the process.

I'm currently only supporting seloger and google sheets as third parties. For other integrations, feel free to write an issue.

## Genereting credentials

### Google sheets

To learn how to create credentials for a desktop application, go to [Create credentials](https://developers.google.com/workspace/guides/create-credentials).

Once you create the credentials, make sure the downloaded JSON file is saved as credentials.json. Then move the file to your working directory and fill the path when instanciating the service.

### SeLoger

An account on *RapidAPI* is needed to retieve the API key.

[https://rapidapi.com/apidojo/api/seloger/](https://rapidapi.com/apidojo/api/seloger/)

## Usage

### Install

```sh
pip install seloger-google-sheets
```

### Write your script

```py
from typing import List
from seloger_google_sheets import RealEstate
from seloger_google_sheets.google import GoogleSpreadsheetsService
from seloger_google_sheets.seloger import (SelogerService, SelogerSearchQuery, RealEstateFilter, 
RealEstateType, TransactionType)


seloger = SelogerService(api_key='my_seloger_api_key')
google_sheets = GoogleSpreadsheetsService(credentials_file_path='./credentials.json')

query = SelogerSearchQuery(
    maximumPrice="800",
    bedrooms="1",
    zipCodes="76300,76800,76000",
    includeNewConstructions="false",
    transactionType=TransactionType.RENT,
    realtyTypes=RealEstateType.APPARTMENT,
    sortBy=RealEstateFilter.NEWEST
)

results: List[RealEstate] = seloger.search(query)
google_sheets.use("my_sheet_id").clear().insert(results)
```

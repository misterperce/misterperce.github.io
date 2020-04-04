---
layout: post
title: Importing Robinhood Portfolio Data into Python Pandas
---
# Import Robinhood
Instructions:
* Login, go to Account, go to History, right click and go to Inspect, open Network console, refresh the webpage, scroll to the bottom, get the response from the last "orders/" line
* Save response to .json file

```
robinhood_response = pd.read_json('robinhood_response.json') # read json
robinhood_response = json_normalize(robinhood_response['results']) #normalize json ... effectively zooms into one column
robinhood_response = robinhood_response[['last_transaction_at', 'side','instrument','average_price','quantity']] # select columns

# pull unique instruments for translation to symbol
instrument_urls = robinhood_response[['instrument']]
instrument_urls = instrument_urls.drop_duplicates()

# translate instrument URLs to symbol
instrument_translation = []

for i in range(0,instrument_urls.size):
    loop_url =instrument_urls.iat[i,0]
    loop_request = requests.get(loop_url)
    loop_read = loop_request.text
    loop_df = pd.read_json(loop_read,typ='series')
    loop_symbol = loop_df['symbol']
    instrument_translation.append([loop_url,loop_symbol])

instrument_translation_df = pd.DataFrame(instrument_translation, columns=['url','symbol'])
robinhood_response = robinhood_response.rename(index=str, columns={'instrument': 'url'})
robinhood_response = pd.merge(robinhood_response, instrument_translation_df, how='left', on='url')
robinhood_response = robinhood_response[['last_transaction_at','side','symbol','quantity','average_price']]
robinhood_response.columns = morgan.columns
robinhood_response['date']=pd.to_datetime(robinhood_response['date']).dt.date
robinhood_response[['units','price']] = robinhood_response[['units','price']].apply(pd.to_numeric, errors='coerce', axis=1)
```

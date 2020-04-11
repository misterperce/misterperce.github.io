---
layout: post
title: Importing Robinhood Portfolio Data into Python Pandas
---
## Introduction

As a Python Pandas enthusiast who owns some stock in a Robinhood account, it seemed natural to me to try to play around with my own financial data in a Jupyter Notebook. It's very doable, but Robinhood doesn't make it too user-friendly.

The two main hurdles that I had to spend some time navigating were:
1. Getting a data download of my portfolio positions, which involves rendering and downloading a .json response file (something I hadn't done before)

2. Robinhood's .json file doesn't explicitly have the stock symbols in the data, but rather has API urls per stock symbol. I had to write a loop to read the urls, extract the stock symbol, and then join the symbol name back to the original DataFrame.


## Getting the .json Response

Credit goes to this [Medium post](https://medium.com/@bartclaeys/how-to-export-your-robinhood-stocks-fc8245b3d118), where I learned how to do this.

Instructions:
Log on to Robinhood via web browser and navigate to your account portfolio. This is found under Account → History.

Next, open the console viewer (for Chrome: right click the background of the page → Inspect) and go to the Network view (highlighted in the image).

![img](/assets/post-imgs/robinhood-network-view.PNG)

Now, you'll need to refresh the webpage (so that the Network console can pick up the full page load). Find an `orders/` file, right click it, and select "Copy Response". This will put the json resonse in your computer's clipboard.

From here, open a text editor, paste the response, and save it as a .json file locally. I called my file `robinhood_response.`



## Importing into Python Pandas

I use pandas's included packages `read_json` and `json_normalize` and extracted the datapoints that I wanted into my DataFrame, `robinhood_response`:

```python
# read json
robinhood_response = pd.read_json('robinhood_response.json')
robinhood_response = json_normalize(robinhood_response['results'])

# reset to only columns of interest
robinhood_response = robinhood_response[['last_transaction_at', 'side','instrument','average_price','quantity']]
```
## Translating Instrument URLs

In order to translate the intrument urls into the standardized stock symbols, I first pull the unique list of instruments to look up:

```python
# pull unique instruments for translation to symbol
instrument_urls = robinhood_response[['instrument']]
instrument_urls = instrument_urls.drop_duplicates()
```

Next, I loop through the list of urls, open each one, find the symbol in the json from the URL, and append it to a list. I then take the list of translations and left join (or 'vlookup', if you're more familiar with Excel) it back to the original DataFrame, `robinhood_response`.

```python
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
```

Lastly, I convert the date into a datetime data type and the units and prices into numeric data types.
```python
robinhood_response['date']=pd.to_datetime(robinhood_response['date']).dt.date
robinhood_response[['units','price']] = robinhood_response[['units','price']].apply(pd.to_numeric, errors='coerce', axis=1)
```

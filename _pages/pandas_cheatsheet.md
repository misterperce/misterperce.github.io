---
title: Pandas Cheatsheet
layout: page
---

- [Input, Output](#input--output)
  * [Read Excel / CSV](#read-excel---csv)
  * [Export as CSV with date in filename](#export-as-csv-with-date-in-filename)
- [Database Functions](#database-functions)
  * [Merge DataFrames](#merge-dataframes)
  * [Create column with values based on conditional](#create-column-with-values-based-on-conditional)
  * [Time Delta](#time-delta)
- [Data Cleanup](#data-cleanup)
  * [Conditional drop rows](#conditional-drop-rows)
  * [Drop duplicates](#drop-duplicates)
  * [Replace value](#replace-value)
  * [Replace string part in column](#replace-string-part-in-column)
  * [Fill NA](#fill-na)
- [Data Formatting](#data-formatting)
  * [Rename columns](#rename-columns)
  * [Coerce datetime format](#coerce-datetime-format)
  * [Datetime to string with custom formatting](#datetime-to-string-with-custom-formatting)
  * [Sort rows by column values](#sort-rows-by-column-values)
  * [Round data](#round-data)
  * [Column arrangement](#column-arrangement)
  * [Convert string to uppercase](#convert-string-to-uppercase)
- [Code Snippets](#code-snippets)
  * [Pick List Generator](#pick-list-generator)
  * [Map Dictionary](#map-dictionary)

(TOC generator credit: [https://ecotrust-canada.github.io/markdown-toc/](https://ecotrust-canada.github.io/markdown-toc/))

---

## Input, Output

### Read Excel / CSV

```python
df = pd.read_excel('file.xlsx', sheet_name=0, header=0)

df = pd.read_csv('file.csv', sep=',')
```

### Export as CSV with date in filename

```python
import datetime as dt
from datetime import date, timedelta

today = date.today()
datestr = today.strftime('%m-%d-%Y')

df.to_csv('pick_list_output_'+datestr+'.csv',index=False)
```

## Database Functions

### Merge DataFrames

```python
output_df = pd.merge(output_df, asin_attr, how='left', on=['asin'])
```

### Create column with values based on conditional

```python
pog_map['vendor_type'] = np.where((pog_map['pog_name']=='GSF Transfer') | (pog_map['pog_name']=='NACF'), 'TRANSSHIP', 'SUBMIT_PO')
```

### Time Delta

```python
# https://pymotw.com/2/datetime/

import datetime

today = datetime.date.today()
print 'Today    :', today

one_day = datetime.timedelta(days=1)
print 'One day  :', one_day

yesterday = today - one_day
print 'Yesterday:', yesterday

tomorrow = today + one_day
print 'Tomorrow :', tomorrow

print 'tomorrow - yesterday:', tomorrow - yesterday
print 'yesterday - tomorrow:', yesterday - tomorrow

----
Output:
Today    : 2013-02-21
One day  : 1 day, 0:00:00
Yesterday: 2013-02-20
Tomorrow : 2013-02-22
tomorrow - yesterday: 2 days, 0:00:00
yesterday - tomorrow: -2 days, 0:00:00
```

## Data Cleanup

### Conditional drop rows

```python
remove.drop(remove[remove.qty == 0].index, inplace=True)
```

### Drop duplicates

```python
asin_attr = asin_attr.drop_duplicates(subset ='asin')
```

### Replace value

```python
pog_map2['case_pack'] = pog_map2['case_pack'].replace(0,1)
```

### Replace string part in column

```python
output_df['past_donated'] = output_df['past_donated'].replace('N','')
```

### Fill NA

```python
pog_map.category = pog_map.category.fillna('AMBIENT')
pog_map.case_pack = pog_map.case_pack.fillna(0)
```

## Data Formatting

### Rename columns

```jsx
df.rename({1: 2, 2: 4}, axis='index')
```

### Coerce datetime format

```python
df_exp['expiration_date'] = pd.to_datetime(df_exp['expiration_date'], errors='coerce')
```

### Datetime to string with custom formatting

```python
inv['snapshot_date'] = sdate.strftime('\'%Y/%m/%d\'')
```

### Sort rows by column values

```python
df_exp1 = df_exp.sort_values(['expiration_date','qty'],ascending = (True, False)).reset_index(drop=True)
```

### Round data

```python
remove.qty = remove.qty.round(0)
```

### Column arrangement

```python
cols = fcst_df_output.columns
cols = list(fcst_df_output.columns.values)
cols = cols[1:2] + cols[:1] + cols[-1:] + cols[2:33]
fcst_df_output = fcst_df_output[cols]
```

### Convert string to uppercase

```python
pog_map.category = pog_map.category.str.upper()
```

## Code Snippets

### Pick List Generator

```python
output = []

for i, row in remove.iterrows():
    temp_mini_asin_loc = df_exp1.drop(df_exp1[df_exp1.asin != row['ASIN']].index).reset_index(drop=True)
    row_counter = 0
    qty_to_remove_counter = row['qty']
    while qty_to_remove_counter > 0 and row_counter < temp_mini_asin_loc.shape[0]:
        if temp_mini_asin_loc.qty.iloc[row_counter] <= qty_to_remove_counter:
            to_remove_from_bin = temp_mini_asin_loc.qty.iloc[row_counter]
        else:
            to_remove_from_bin = qty_to_remove_counter
        output.append([temp_mini_asin_loc.asin.iloc[row_counter], temp_mini_asin_loc.location_id.iloc[row_counter], to_remove_from_bin, temp_mini_asin_loc.expiration_date.iloc[row_counter]])
        qty_to_remove_counter = qty_to_remove_counter - temp_mini_asin_loc.qty.iloc[row_counter]
        row_counter = row_counter + 1
```

### Map Dictionary

```python
mydict = {'Bin:A.' : 'AMBIENT',
          'Bin:DC.' : 'AMBIENT',
          'Bin:S.' : 'AMBIENT',
          'Bin:G.' : 'AMBIENT',
          'Bin:M.' : 'CHILLED',
          'Bin:RT.' : 'CHILLED',
          'Bin:P.' : 'CHILLED',
          'Bin:F.' : 'FROZEN',
          'Bin:D' : 'CHILLED'}

pat = '|'.join(r"\b{}\b".format(x) for x in mydict.keys())
bins1['temp_zone'] = bins1['location_id'].str.extract('('+ pat + ')', expand=False).map(mydict)
output_df = pd.merge(output_df, bins1, how='left', on=['location_id'])
output_df = output_df.dropna(subset=['capacity_subgroup'])
```

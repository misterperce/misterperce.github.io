---
title: R Cheatsheet
layout: page
---

### Call column in dataframe

```
dataframe$column
```

### Transpose shape of dataframe
```
df2 <- spread(returns, stock, return)
```

### Find correlation of columns in dataframe  
```
cor(df2, y=NULL, use="everything")
```
### Find percentile given quantity, mean, and sd  
```
pnorm(1,3.23,8.47)
```


### Create new dataframe with just col_a and col_b  
```
select(df, col_a, col_b)
```
### Probability of succeeding 8 or more times out of 12 trials with success rate = 0.587  
```
1 - pbinom(7,12,0.587)
```

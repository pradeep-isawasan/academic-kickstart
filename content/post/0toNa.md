---
title: Data Cleaning using Python
summary: Replacing 0 with NaN
date: "2020-05-19"
draft: false
share: false
commentable: false
editable: false

# Optional header image (relative to `static/img/` folder).
header:
  caption: ""
  image: ""
---

Real-world data often has missing values. Data can have missing values for a number of reasons such as observations that were not recorded and data corruption.

## Libraries
```{python}
from pandas import read_csv
from pandas import nan
```

## Summary
We can use summary statistics to help identify missing or corrupt data.

```{python}
# summarize the dataset
data.describe()
```
{{< figure library="true" src="datadescribe.JPG" title="O" lightbox="true" >}}

## Dataset
```{python}
#load the dataset
data = read_csv('diamonds.csv')
```
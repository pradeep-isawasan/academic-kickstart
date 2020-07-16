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
  caption: "datadescribe.PNG"
  image: ""
---

Real-world data often has "unusual values". Data can have this so called "unusual" values for a number of reasons such as observations that were not recorded, data corruption.

## Libraries
```{python}
from pandas import read_csv
from pandas import nan
```

## Dataset (Bling Bling $$)
For this tutorial we will be using diamonds dataset. It is a classic dataset and suitable for beginner for their data analysis.

You can dowload the dataset from <https://www.kaggle.com/shivam2503/diamonds>

```{python}
#load the dataset
data = read_csv('diamonds.csv')
#view the dataset
data
```
{{< figure library="true" src="viewdata.PNG" title="O" lightbox="true" >}}

## Summary Statistics
We can use summary statistics to help identify missing or corrupt data.

```{python}
# summarize the dataset
data.describe()
```
{{< figure library="true" src="datadescribe.PNG" title="O" lightbox="true" >}}

Note the red arrow. It indicate the minimum value in the column x, y, z. Having 0 kind of unusual 
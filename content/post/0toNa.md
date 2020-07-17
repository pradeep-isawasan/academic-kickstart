---
title: Data Cleaning using Python
subtitle: Handling Unusual Values
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

### Libraries
```{python}
from pandas import read_csv
from pandas import nan
```

### Dataset (Bling Bling $$)
For this tutorial we will be using diamonds dataset. It is a classic dataset and suitable for beginner for their data analysis.

You can dowload the dataset from <https://www.kaggle.com/shivam2503/diamonds>

```{python}
#load the dataset
data = read_csv('diamonds.csv')
#view the dataset
data
```
{{< figure library="true" src="viewdata.PNG" lightbox="true" >}}

## Summary Statistics
We can use summary statistics to help identify missing or corrupt data.

```{python}
# summarize the dataset
data.describe()
```
{{< figure library="true" src="datadescribe.PNG" lightbox="true" >}}

The red arrow indicate the minimum value in each column. Note that column x, y, z, the dimensions of these diamonds, in mm have minimum value 0. 

We know that diamonds can’t have a width of 0 mm, so these values kind of unusual and must be incorrect.


## Whats wrong with having 0 ?

If 0 is the real value, for example 0 mark in an exam, we can keep it.

Now, imagine 0 is a data error, like the diamods dataset, it will really effect the data distribution.


## Handling the Unusual Value
We first locate and count this 0's.

```{python}
# Finding 0
(data.loc[:, 'carat':'z'] == 0).sum()
```
{{< figure library="true" src="finding0.PNG" lightbox="true" >}}




## Replace with NaN
In Python, specically Pandas, NumPy and Scikit-Learn, we mark missing values as NaN.
Values with a NaN value are ignored from operations like sum, count, etc.
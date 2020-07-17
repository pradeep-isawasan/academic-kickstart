---
title: Data Cleaning using Python
subtitle: Handling "Unusual" Values
summary: Real-world data often has "unusual values". Data can have this so called "unusual" values for a number of reasons such as human errors or problem in measuring devices.
date: "2020-07-17"
draft: false
share: false
commentable: false
editable: false

# Optional header image (relative to `static/img/` folder).
header:
  caption: "datadescribe.PNG"
  image: ""
---

Real-world data often has "unusual values". Data can have this so called "unusual" values for a number of reasons such as human errors or problem in measuring devices.

### Libraries
```{python}
from pandas import read_csv
from pandas import nan
```

### Dataset (Bling Bling $$)
For this tutorial we will be using diamonds dataset. It is a classic dataset and suitable for beginner to explore data analysis.

You can dowload the dataset from -> <https://www.kaggle.com/shivam2503/diamonds>

```{python}
#load the dataset, please make sure on your working directory
data = read_csv('diamonds.csv')
#view the dataset
data
```
{{< figure library="true" src="viewdata.PNG" lightbox="true" >}}

### Summary Statistics
We can use summary statistics to help identify this unusual data.

```{python}
# summarize the dataset
data.describe()
```
{{< figure library="true" src="datadescribe.PNG" lightbox="true" >}}

The red arrow indicate the minimum value in each column. Note that column x, y, z, the dimensions of these diamonds, in mm have minimum value 0. 

We know that diamonds can’t have a width of 0 mm, so these values kind of unusual and must be incorrect.


### Whats wrong with having 0 ?

If 0 is the real value, for example 0 mark in an exam, we can keep it.

Now, imagine 0 is a data error, like the diamods dataset, it will really effect the data distribution.


### Handling the Unusual Value
We first locate and count this 0's.

```{python}
# Finding and counting 0
(data.loc[:, 'carat':'z'] == 0).sum()
```
{{< figure library="true" src="finding0.PNG" lightbox="true" >}}

Note that column x, y, z have 8, 7, 20 values with 0 respectively. Now lets view the rows when the column x = 0.
```{python}
# Filtering rows with column condition, x = 0
data.loc[data.x == 0, :]
```
{{< figure library="true" src="viewx0.PNG" lightbox="true" >}}

### Marking with NaN
In Pandas or NumPy, we can replace them with NaN (missing values) or some refer this step as marking with NaN. Values with a NaN value are ignored from operations like sum or count.

Note that we only need to focus on column x, y, z because this are the columns where the 0's are located.

```{python}
# Replace 0 with NaN
data[['x','y','z']] = data[['x','y','z']].replace(0, nan)
```

After we have replaced 0 with NaN, we can use the isnull() function to mark the NaN values as True and count the number of missing values for each column.

```{python}
# Counting NaN
data.isnull().sum()
```
Running this will produce a similiar output as counting 0's. Note that columns x, y, z have the same number of NaN as zero values identified above. Now you can have a peace of mind!

Now lets view again the rows when the column x = 0, whether they had been replaced with NaN.
```{python}
# Filtering rows with column condition, x = NaN
data.loc[data.x.isnull(), :]
```
{{< figure library="true" src="NaN.PNG" lightbox="true" >}}

Yes, finally we had successfully replaced the 0's with NaN's. 

For some machine learning algorithms having missing values can cause trouble. In my next post I will discuss on this.
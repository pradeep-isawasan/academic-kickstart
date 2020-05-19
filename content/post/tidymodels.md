---
title: Introduction to Machone Learning using tidymodels.
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

## Dataset
```{r}
iris
```

## Libraries
These two packages will be mainly used.
```{r}
library(tidyverse)
library(tidymodels)
```

## Data Sampling
Split your dataset into training and testing.

```{r}
# initial_split from rsample package which is part of tidymodels
iris_split <- initial_split(iris, prop = 0.7)

# extract training and testing sets
iris_train <- training(iris_split)
iris_test <- testing(iris_split)
```

## Recipe
Prepare your recipe

1. recipe(): specify the formula
2. step_xyz(): specify the pre-processing steps

```{r}
iris_recipe <-
  #define your formula
  recipe(Species ~., data = iris_full) %>%
  # if you are planning to normalize your numerical values
  step_normalize(all_numeric()) %>%
  # if you are planning to knn-ly fill the missing values for categorical type
  step_knnimpute(Species)
```

If you want to extract the pre-processed dataset itself, you can first prep() the recipe for a specific dataset and juice() the prepped recipe to extract the pre-processed data

```{r}
iris_train_preprocessed <- iris_recipe %>%
  # apply the recipe to the training data
  prep(iris_train) %>%
  # extract the pre-processed training dataset
  juice()
```

## Model Training
Decide on what model you are planning to use.

```{r}
knn_model <-
  # specify that the model is a k-Nearest Neigbhour (kNN)
  nearest_neighbor() %>%
  # select the package that the model coming from
  set_engine("kknn") %>%
  # choose mode
  set_mode("classification")
```

## Workflow
Now you can put the model and recipes together into a workflow

```{r}
library(workflows)
# set the workflow
knn_workflow <- workflow() %>%
  # add the recipe
  add_recipe(iris_recipe) %>%
  # add the model
  add_model(knn_model)
```

You can now fit your model to the dataset.

```{r}
knn_fit <- knn_workflow %>%
  # fit the final best model to the training set and evaluate the test set
  last_fit(iris_split)
```
## Model Evaluation
Model evaluation is very important part in machine learning.

### Performance
Here you can check on how good is your model performing

```{r}
# Obtain and format results produced by tuning functions
knn_predictions <- knn_fit %>%
  collect_predictions()

knn_performance <- knn_fit %>%
  collect_metrics()
```

To generate the confusion matrix:
```{r}
knn_predictions %>%
  conf_mat(truth = Species, estimate = .pred_class)
```

## Use your final model
If you want to use your model to predict new data, you need to use the fit() function on your workflow and the dataset that you want to fit the final model. Remember: training dataset + testing dataset.
```{r}
final_knnmodel <- fit(knn_workflow, iris)
```

For example lets create a new data:
```{r}
new_iris <- tribble(~Sepal.Length, ~Sepal.Width, ~Petal.Length, ~Petal.Width, 5.1, 3, 2.7, 4)
```

If you wanted to predict the species of iris for new_iris, use predict() function.
```{r}
predict(final_knnmodel, new_data = new_iris)
```

## Video Tutorial
The full tutorial available in my YouTube channel. Enjoy and don't forget to subscribe!
{{< youtube 04sncGOrLR0 >}}

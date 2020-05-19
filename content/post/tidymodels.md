---
title: Jom Bersihkan Data!
date: "2018-06-28T00:00:00+01:00"
draft: false
share: false
commentable: false
editable: false

# Optional header image (relative to `static/img/` folder).
header:
  caption: ""
  image: ""
---

# Model Training

We will parsnip package
1. model type: what kind of model you want to fit
2. engine: set_engine(), the package the model coming from
3. mode: set_mode(), the type of prediction

```{r}
knn_model <-
  # specify that the model is a k-Nearest Neigbhour (kNN)
  nearest_neighbor() %>%
  # select the package that the model coming from
  set_engine("kknn") %>%
  # choose mode
  set_mode("classification")
```

The full tutorial available in my YouTube channel
{{< youtube 04sncGOrLR0 >}}

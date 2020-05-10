---
title: Jom Bersihkan Data!
date: "2018-06-28T00:00:00+01:00"
draft: true
share: true
commentable: false
editable: false

# Optional header image (relative to `static/img/` folder).
header:
  caption: ""
  image: ""
---

```r
library(tidyverse)
iris <- iris %>%
  select(Petal.Length)
```

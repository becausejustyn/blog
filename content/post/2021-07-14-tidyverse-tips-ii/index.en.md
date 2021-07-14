---
title: "Tidyverse Tips II"
author: "R package build"
date: '2021-07-14'
slug: tidyverse-tips-ii
categories: R
tags:
- tidyverse
- R
subtitle: ''
summary: ''
authors: []
lastmod: '2021-07-14T20:03:47+10:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

```{r}
library(tidyverse)
library(ggplot2)
```

```{r}
midwest <- tibble::as_tibble(midwest)
```

#### Selecting Columns

```{r}
midwest %>%
  select(county, starts_with("A")) %>%
  head()
```

#### Selecting Columns (Regex)

`matches()` here results all columns that have the letter p followed by more than one letter that also contain the letter n.

```{r}
midwest %>%
  select(matches("p.+n")) %>%
  head()
```

#### Reformatting All Column Names

```{r}
midwest %>%
  select_all(toupper) #could also use tolower()
```

### Cleaning Column Names

```{r}
#making an unclean database:
midwest2 <- midwest %>%
  select(poptotal, popother, county, percbelowpoverty, category)

colnames(midwest2) <- c("pop total", "pop other", "county", "perc below poverty", "category")


midwest2 %>%
  select_all(~str_replace(., " ", "_"))
```

### Filtering

You can use `near()` with the tolerance argument to find values close to a certain number.

```{r}
midwest %>%
  select(county, poptotal) %>%
  filter(near(
    poptotal, 96000, tol = 15000
    ))
```

If you want to filter your rows on multiple values, you can use the `%in%` operator.

```{r}
midwest %>%
  select(poptotal, popother, county, percbelowpoverty, category) %>%
  filter(county %in% c("IOWA", "JERSEY", "PARKE", "FULTON"))
```

To return all rows where only one condition is met you can use `xor()` from base.

```{r}
midwest %>%
  filter(xor(popother < 80, percbelowpoverty > 15))
```

Return all rows where `popother` is less than $80$, but `percbelowpoverty` does not exceed $15%$.

```{r}
midwest %>%
  filter(popother < 80, !percbelowpoverty > 15)
```

### Counting

The `count()` function has a sort argument.

```{r}
midwest %>%
  count(category, sort = TRUE)
```

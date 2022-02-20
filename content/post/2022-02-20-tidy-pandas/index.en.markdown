---
title: Tidy Pandas
author: R package build
date: '2022-02-20'
slug: tidy-pandas
categories:
  - R
tags:
  - python
  - tidyverse
  - R
  - pandas
subtitle: ''
summary: ''
authors: []
lastmod: '2022-02-20T17:51:21+11:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
output: 
  html_document: 
    toc: yes
    self_contained: no
---


Uni starts back up soon so I thought it would be a good idea to brush up on my `python`. I have avoided using `python` since `R` is much more user friendly between `dplyr` and `ggplot2`. Now that RStudio has `python` computability via `reticulate` there is not really a good reason to completely avoid `python`. I think it is always good practice to get more comfortable with different languages, because sometimes you will need to do a task that is only available using a specific tool. Similarly, there are times when a group project works best when everybody is able to use a similar language.

As tempting as it might be to do all my data wrangling via `tidyverse`, I have been practising using pandas. This post was entirely written in RStudio, however, the `python` code will run in a notebook alternative such as Jupyter or VS Code. 

### Installing Packages {.tabset .tabset-fade .tabset-pills}

#### R


```r
install.packages("ggplot2")
install.packages("dplyr")
install.packages("purrr")

#or simply
install.packages("tidyverse")
```

#### Python


```python
!pip3 install seaborn
!pip3 install numpy
!pip3 install pandas

#You can also install these packages in the terminal 
pip3 install seaborn
pip3 install numpy
pip3 install pandas
```

Learning `python` was overwhelming because you use the terminal much more often than you need to when using `R`. Over time, I have began to appreciate using a virtual environment because you can easily run multiple versions of `python`, which makes it more practical when you are using a package that requires an older version. 

### Importing Data, Loading Libraries {.tabset .tabset-fade .tabset-pills}

I have hidden the output of the code, however, you can view it by clicking the dropdown menu. I did this primarily for myself so it was easier to scroll down, but I think it is also more practical since the output is not necessarily the focus of this post.

#### R


```r
library(dplyr)
library(ggplot2)

df <- diamonds

df %>% head()
```

```
## # A tibble: 6 × 10
##   carat cut       color clarity depth table price     x     y     z
##   <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
## 1  0.23 Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
## 2  0.21 Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
## 3  0.23 Good      E     VS1      56.9    65   327  4.05  4.07  2.31
## 4  0.29 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
## 5  0.31 Good      J     SI2      63.3    58   335  4.34  4.35  2.75
## 6  0.24 Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
```

#### Python


```python
import seaborn as sns
import numpy as np
import pandas as pd
sns.set_style('white')

df = sns.load_dataset('diamonds')

df.head()
```

```
##    carat      cut color clarity  depth  table  price     x     y     z
## 0   0.23    Ideal     E     SI2   61.5   55.0    326  3.95  3.98  2.43
## 1   0.21  Premium     E     SI1   59.8   61.0    326  3.89  3.84  2.31
## 2   0.23     Good     E     VS1   56.9   65.0    327  4.05  4.07  2.31
## 3   0.29  Premium     I     VS2   62.4   58.0    334  4.20  4.23  2.63
## 4   0.31     Good     J     SI2   63.3   58.0    335  4.34  4.35  2.75
```

### Example of Functions {.tabset .tabset-fade .tabset-pills}

#### Verbs

|                            dplyr |                           pandas |
|---------------------------------:|---------------------------------:|
|         `filter()` and `slice()` |  `query()` and `loc[]`, `iloc[]` |
|                      `arrange()` | `sort_values` and `sort_index()` |
|        `select()` and `rename()` |     `__getitem__` and `rename()` |
|                       `select()` |                       `filter()` |
|                     `distinct()` |              `drop_duplicates()` |
|                       `mutate()` |                         `assign` |
|                    `summarise()` |                            `agg` |
|                     `group_by()` |                      `groupby()` |
| `sample_n()` and `sample_frac()` |                         `sample` |
|                            `%>%` |                       `pipe[^1]` |

#### Example

|                                           dplyr |                                       pandas |
|------------------------------------------------:|---------------------------------------------:|
|                 `filter(df, col == 'val')`      |                   `df.query('col == "val"')` |
|                         `arrange(df, col)`      |                      `df.sort_values('val')` |
|           `rename(df, new_name = old_name)`     | `df.rename(columns = {old_name = new_name})` |
|                           `select(df, col)`     |                              `df.loc['val']` |
|           `distinct(df, col, .keep_all = TRUE)` |              `df[['val']].drop_duplicates()` |
|                  `mutate(new_var = col - col2)` |      `df.assign(new_var = df.col - df.col2)` |
| `summarise(mean = mean(col2), n = count(col1))` |  `df.agg({"col1": "count", "col2", "mean"})` |
|                             `group_by(df, col)` |                          `df.groupby('col')` |
|                                           `%>%` |                                   `pipe[^1]` |

[^1]: To the best of my knowledge, you can still pipe without using the function, however, I have not explored it that much.

One of the confusing things are first is that there are many similar functions under different names. I personally find it easier to remember them by the way I write my code. For example, by only using `<-` as an assignment operator in `R`, I find it easier to treat the two languages differently. 

## `select()` 

### selecting columns {.tabset .tabset-fade .tabset-pills}

#### R


```r
select(df, color, cut)

#or

df %>%
  select(color, cut)
```

<details>
<summary>View Output</summary>


```r
select(df, color, cut)
```

```
## # A tibble: 53,940 × 2
##    color cut      
##    <ord> <ord>    
##  1 E     Ideal    
##  2 E     Premium  
##  3 E     Good     
##  4 I     Premium  
##  5 J     Good     
##  6 J     Very Good
##  7 I     Very Good
##  8 H     Very Good
##  9 E     Fair     
## 10 H     Very Good
## # … with 53,930 more rows
```

</details>

#### Python


```python
df.filter(['color', 'cut'])

#or

df[['x', 'y', 'z']]
```

<details>
<summary>View Output</summary>


```python
df.filter(['color', 'cut'])
```

```
##       color        cut
## 0         E      Ideal
## 1         E    Premium
## 2         E       Good
## 3         I    Premium
## 4         J       Good
## ...     ...        ...
## 53935     D      Ideal
## 53936     D       Good
## 53937     D  Very Good
## 53938     H    Premium
## 53939     D      Ideal
## 
## [53940 rows x 2 columns]
```

</details>

### If we want to select a range of columns {.tabset .tabset-fade .tabset-pills}

#### R


```r
select(df, x:z)

#or

df %>% select(x:z)
```

<details>
<summary>View Output</summary>


```r
select(df, x:z)
```

```
## # A tibble: 53,940 × 3
##        x     y     z
##    <dbl> <dbl> <dbl>
##  1  3.95  3.98  2.43
##  2  3.89  3.84  2.31
##  3  4.05  4.07  2.31
##  4  4.2   4.23  2.63
##  5  4.34  4.35  2.75
##  6  3.94  3.96  2.48
##  7  3.95  3.98  2.47
##  8  4.07  4.11  2.53
##  9  3.87  3.78  2.49
## 10  4     4.05  2.39
## # … with 53,930 more rows
```

</details>

#### Python


```python
df.loc[:, 'x':'z']
```

<details>
<summary>View Output</summary>


```python
df.loc[:, 'x':'z']
```

```
##           x     y     z
## 0      3.95  3.98  2.43
## 1      3.89  3.84  2.31
## 2      4.05  4.07  2.31
## 3      4.20  4.23  2.63
## 4      4.34  4.35  2.75
## ...     ...   ...   ...
## 53935  5.75  5.76  3.50
## 53936  5.69  5.75  3.61
## 53937  5.66  5.68  3.56
## 53938  6.15  6.12  3.74
## 53939  5.83  5.87  3.64
## 
## [53940 rows x 3 columns]
```

</details>

### If we want to pipe it {.tabset .tabset-fade .tabset-pills}

#### R


```r
df %>% 
  select(color, cut)
```

<details>
<summary>View Output</summary>


```r
df %>% 
  select(color, cut)
```

```
## # A tibble: 53,940 × 2
##    color cut      
##    <ord> <ord>    
##  1 E     Ideal    
##  2 E     Premium  
##  3 E     Good     
##  4 I     Premium  
##  5 J     Good     
##  6 J     Very Good
##  7 I     Very Good
##  8 H     Very Good
##  9 E     Fair     
## 10 H     Very Good
## # … with 53,930 more rows
```

</details>

#### Python


```python
(df
.filter(['color', 'cut'])
)
```

<details>
<summary>View Output</summary>


```python
(df
.filter(['color', 'cut'])
)
```

```
##       color        cut
## 0         E      Ideal
## 1         E    Premium
## 2         E       Good
## 3         I    Premium
## 4         J       Good
## ...     ...        ...
## 53935     D      Ideal
## 53936     D       Good
## 53937     D  Very Good
## 53938     H    Premium
## 53939     D      Ideal
## 
## [53940 rows x 2 columns]
```

</details>

### If we want to drop a certain column {.tabset .tabset-fade .tabset-pills}

#### R


```r
select(df, -(x:z))

#or

df %>%
  select(-(x:z))
```

<details>
<summary>View Output</summary>


```r
select(df, -(x:z))
```

```
## # A tibble: 53,940 × 7
##    carat cut       color clarity depth table price
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int>
##  1  0.23 Ideal     E     SI2      61.5    55   326
##  2  0.21 Premium   E     SI1      59.8    61   326
##  3  0.23 Good      E     VS1      56.9    65   327
##  4  0.29 Premium   I     VS2      62.4    58   334
##  5  0.31 Good      J     SI2      63.3    58   335
##  6  0.24 Very Good J     VVS2     62.8    57   336
##  7  0.24 Very Good I     VVS1     62.3    57   336
##  8  0.26 Very Good H     SI1      61.9    55   337
##  9  0.22 Fair      E     VS2      65.1    61   337
## 10  0.23 Very Good H     VS1      59.4    61   338
## # … with 53,930 more rows
```

</details>


#### Python


```python
(df
.drop(['x', 'y', 'z'], axis = 1)
)
```

<details>
<summary>View Output</summary>


```python
(df
.drop(['x', 'y', 'z'], axis = 1)
)
```

```
##        carat        cut color clarity  depth  table  price
## 0       0.23      Ideal     E     SI2   61.5   55.0    326
## 1       0.21    Premium     E     SI1   59.8   61.0    326
## 2       0.23       Good     E     VS1   56.9   65.0    327
## 3       0.29    Premium     I     VS2   62.4   58.0    334
## 4       0.31       Good     J     SI2   63.3   58.0    335
## ...      ...        ...   ...     ...    ...    ...    ...
## 53935   0.72      Ideal     D     SI1   60.8   57.0   2757
## 53936   0.72       Good     D     SI1   63.1   55.0   2757
## 53937   0.70  Very Good     D     SI1   62.8   60.0   2757
## 53938   0.86    Premium     H     SI2   61.0   58.0   2757
## 53939   0.75      Ideal     D     SI2   62.2   55.0   2757
## 
## [53940 rows x 7 columns]
```

</details>


## `filter()`

### filtering on one condition {.tabset .tabset-fade .tabset-pills}

#### R


```r
filter(df, color == 'E')
```

<details>
<summary>View Output</summary>


```r
filter(df, color == 'E')
```

```
## # A tibble: 9,797 × 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  0.23 Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
##  2  0.21 Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
##  3  0.23 Good      E     VS1      56.9    65   327  4.05  4.07  2.31
##  4  0.22 Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
##  5  0.2  Premium   E     SI2      60.2    62   345  3.79  3.75  2.27
##  6  0.32 Premium   E     I1       60.9    58   345  4.38  4.42  2.68
##  7  0.23 Very Good E     VS2      63.8    55   352  3.85  3.92  2.48
##  8  0.23 Very Good E     VS1      60.7    59   402  3.97  4.01  2.42
##  9  0.23 Very Good E     VS1      59.5    58   402  4.01  4.06  2.4 
## 10  0.23 Good      E     VS1      64.1    59   402  3.83  3.85  2.46
## # … with 9,787 more rows
```

</details>


#### Python


```python
(df
.query("color == 'E'")
)
```

<details>
<summary>View Output</summary>


```python
(df
.query("color == 'E'")
)
```

```
##        carat        cut color clarity  depth  table  price     x     y     z
## 0       0.23      Ideal     E     SI2   61.5   55.0    326  3.95  3.98  2.43
## 1       0.21    Premium     E     SI1   59.8   61.0    326  3.89  3.84  2.31
## 2       0.23       Good     E     VS1   56.9   65.0    327  4.05  4.07  2.31
## 8       0.22       Fair     E     VS2   65.1   61.0    337  3.87  3.78  2.49
## 14      0.20    Premium     E     SI2   60.2   62.0    345  3.79  3.75  2.27
## ...      ...        ...   ...     ...    ...    ...    ...   ...   ...   ...
## 53926   0.71      Ideal     E     SI1   61.9   56.0   2756  5.71  5.73  3.54
## 53928   0.79    Premium     E     SI2   61.4   58.0   2756  6.03  5.96  3.68
## 53930   0.71    Premium     E     SI1   60.5   55.0   2756  5.79  5.74  3.49
## 53932   0.70  Very Good     E     VS2   60.5   59.0   2757  5.71  5.76  3.47
## 53933   0.70  Very Good     E     VS2   61.2   59.0   2757  5.69  5.72  3.49
## 
## [9797 rows x 10 columns]
```

</details>

### If we want multiple conditions {.tabset .tabset-fade .tabset-pills}

#### R


```r
filter(df, color == 'E', cut == 'Good')

#or

filter(df, color == 'E' & cut == 'Good')
```

<details>
<summary>View Output</summary>


```r
filter(df, color == 'E', cut == 'Good')
```

```
## # A tibble: 933 × 10
##    carat cut   color clarity depth table price     x     y     z
##    <dbl> <ord> <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  0.23 Good  E     VS1      56.9    65   327  4.05  4.07  2.31
##  2  0.23 Good  E     VS1      64.1    59   402  3.83  3.85  2.46
##  3  0.26 Good  E     VVS1     57.9    60   554  4.22  4.25  2.45
##  4  0.7  Good  E     VS2      57.5    58  2759  5.85  5.9   3.38
##  5  0.71 Good  E     VS2      59.2    61  2772  5.8   5.88  3.46
##  6  0.7  Good  E     VS2      64.1    59  2777  5.64  5.59  3.6 
##  7  0.7  Good  E     VS1      57.2    62  2782  5.81  5.77  3.31
##  8  0.76 Good  E     SI1      63.7    54  2789  5.76  5.85  3.7 
##  9  0.7  Good  E     VS2      64.1    55  2793  5.6   5.66  3.61
## 10  0.73 Good  E     SI1      63.2    58  2796  5.7   5.76  3.62
## # … with 923 more rows
```

</details>

#### Python


```python
(df
.query('color == "E" & cut == "Good"')
)
```

<details>
<summary>View Output</summary>


```python
(df
.query('color == "E" & cut == "Good"')
)
```

```
##        carat   cut color clarity  depth  table  price     x     y     z
## 2       0.23  Good     E     VS1   56.9   65.0    327  4.05  4.07  2.31
## 36      0.23  Good     E     VS1   64.1   59.0    402  3.83  3.85  2.46
## 84      0.26  Good     E    VVS1   57.9   60.0    554  4.22  4.25  2.45
## 95      0.70  Good     E     VS2   57.5   58.0   2759  5.85  5.90  3.38
## 169     0.71  Good     E     VS2   59.2   61.0   2772  5.80  5.88  3.46
## ...      ...   ...   ...     ...    ...    ...    ...   ...   ...   ...
## 53695   0.75  Good     E     VS2   59.7   65.0   2717  5.85  5.80  3.48
## 53739   0.73  Good     E     VS2   63.3   60.0   2723  5.67  5.73  3.61
## 53741   0.78  Good     E     SI1   57.9   62.0   2723  6.06  6.03  3.50
## 53785   0.89  Good     E     SI2   64.3   65.0   2728  6.00  5.95  3.84
## 53890   0.73  Good     E     SI1   57.9   55.0   2749  6.00  5.96  3.46
## 
## [933 rows x 10 columns]
```

</details>

### If we want multiple conditions in one column {.tabset .tabset-fade .tabset-pills}

#### R


```r
df %>% 
    filter(color %in% c('E', 'J'))
```

<details>
<summary>View Output</summary>


```r
df %>% 
    filter(color %in% c('E', 'J'))
```

```
## # A tibble: 12,605 × 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
##  1  0.23 Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
##  2  0.21 Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
##  3  0.23 Good      E     VS1      56.9    65   327  4.05  4.07  2.31
##  4  0.31 Good      J     SI2      63.3    58   335  4.34  4.35  2.75
##  5  0.24 Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
##  6  0.22 Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
##  7  0.3  Good      J     SI1      64      55   339  4.25  4.28  2.73
##  8  0.23 Ideal     J     VS1      62.8    56   340  3.93  3.9   2.46
##  9  0.31 Ideal     J     SI2      62.2    54   344  4.35  4.37  2.71
## 10  0.2  Premium   E     SI2      60.2    62   345  3.79  3.75  2.27
## # … with 12,595 more rows
```

</details>

#### Python


```python
(df
.query('color in ["E", "J"]')
)
```

<details>
<summary>View Output</summary>


```python
(df
.query('color in ["E", "J"]')
)
```

```
##        carat        cut color clarity  depth  table  price     x     y     z
## 0       0.23      Ideal     E     SI2   61.5   55.0    326  3.95  3.98  2.43
## 1       0.21    Premium     E     SI1   59.8   61.0    326  3.89  3.84  2.31
## 2       0.23       Good     E     VS1   56.9   65.0    327  4.05  4.07  2.31
## 4       0.31       Good     J     SI2   63.3   58.0    335  4.34  4.35  2.75
## 5       0.24  Very Good     J    VVS2   62.8   57.0    336  3.94  3.96  2.48
## ...      ...        ...   ...     ...    ...    ...    ...   ...   ...   ...
## 53926   0.71      Ideal     E     SI1   61.9   56.0   2756  5.71  5.73  3.54
## 53928   0.79    Premium     E     SI2   61.4   58.0   2756  6.03  5.96  3.68
## 53930   0.71    Premium     E     SI1   60.5   55.0   2756  5.79  5.74  3.49
## 53932   0.70  Very Good     E     VS2   60.5   59.0   2757  5.71  5.76  3.47
## 53933   0.70  Very Good     E     VS2   61.2   59.0   2757  5.69  5.72  3.49
## 
## [12605 rows x 10 columns]
```

</details>

### Count Missing Values {.tabset .tabset-fade .tabset-pills}

#### R


```r
# sum of missing values in each column
df %>% 
  summarise(across(everything(), ~sum(is.na(.))))

purrr::map_df(df, ~sum(is.na(.)))
```

<details>
<summary>View Output</summary>


```r
purrr::map_df(df, ~sum(is.na(.)))
```

```
## # A tibble: 1 × 10
##   carat   cut color clarity depth table price     x     y     z
##   <int> <int> <int>   <int> <int> <int> <int> <int> <int> <int>
## 1     0     0     0       0     0     0     0     0     0     0
```

</details>

#### Python


```python
df.isna().sum()
```

<details>
<summary>View Output</summary>


```python
df.isna().sum()
```

```
## carat      0
## cut        0
## color      0
## clarity    0
## depth      0
## table      0
## price      0
## x          0
## y          0
## z          0
## dtype: int64
```

</details>

### Count Unique Values in Each Column {.tabset .tabset-fade .tabset-pills}

#### R


```r
# getting the count of unique values in each column 
df %>% 
  summarise(across(everything(), n_distinct))

#can also map across for the same result
purrr::map_df(df, ~sum(n_distinct(.)))

# if you just want numerical columns
df %>% 
  summarise(across(where(is.numeric), n_distinct))
```

<details>
<summary>View Output</summary>


```r
purrr::map_df(df, ~sum(n_distinct(.)))
```

```
## # A tibble: 1 × 10
##   carat   cut color clarity depth table price     x     y     z
##   <int> <int> <int>   <int> <int> <int> <int> <int> <int> <int>
## 1   273     5     7       8   184   127 11602   554   552   375
```

</details>

#### Python



```python
df.nunique()

# If you want unique values in numeric columns
df.select_dtypes(include = np.number).nunique()
#or
df.select_dtypes('number').nunique()

# If you just want the column names of numeric type
df.select_dtypes('number').columns
# If you want them as a list
df.select_dtypes(include = np.number).columns.tolist()

# count and unique values
df.agg(['count', 'size', 'nunique'])

#for the proportions
df.select_dtypes(include = np.number).value_counts(normalize = True)
#or
df.select_dtypes('number').value_counts(normalize = True)
```

<details>
<summary>View Output</summary>


```python
(df
.select_dtypes(include = np.number)
.nunique()
)
```

```
## carat      273
## depth      184
## table      127
## price    11602
## x          554
## y          552
## z          375
## dtype: int64
```

</details>

### Complex Pipings {.tabset .tabset-fade .tabset-pills}

#### R


```r
df %>%
  select(starts_with('c')) %>%
  filter(cut %in% c('Ideal', 'Premium')) %>%
  group_by(cut, color, clarity) %>%
  summarise(
    avgcarat = mean(carat, na.rm=TRUE),
    n = n()
    ) %>%
  arrange(-avgcarat) %>% #desc(avgcarat) also works
  head()
```

<details>
<summary>View Output</summary>


```r
df %>%
  select(starts_with('c')) %>%
  filter(cut %in% c('Ideal', 'Premium')) %>%
  group_by(cut, color, clarity) %>%
  summarise(
    avgcarat = mean(carat, na.rm=TRUE),
    n = n()
    ) %>%
  arrange(-avgcarat) %>% #desc(avgcarat) also works
  head()
```

```
## `summarise()` has grouped output by 'cut', 'color'. You can override using the
## `.groups` argument.
```

```
## # A tibble: 6 × 5
## # Groups:   cut, color [4]
##   cut     color clarity avgcarat     n
##   <ord>   <ord> <ord>      <dbl> <int>
## 1 Ideal   J     I1          1.99     2
## 2 Premium I     I1          1.61    24
## 3 Premium J     I1          1.58    13
## 4 Premium J     SI2         1.55   161
## 5 Ideal   H     I1          1.48    38
## 6 Premium I     SI2         1.42   312
```

</details>


#### Python


```python
(df
 .filter(regex = '^c')
 .query('cut in ["Ideal", "Premium"]')
 .groupby(['cut', 'color', 'clarity'])
 .agg(['mean', 'size'])
 .sort_values(by = ('carat', 'mean'), ascending = False)
 .head())
```

<details>
<summary>View Output</summary>


```python
(df
 .filter(regex = '^c')
 .query('cut in ["Ideal", "Premium"]')
 .groupby(['cut', 'color', 'clarity'])
 .agg(['mean', 'size'])
 .sort_values(by = ('carat', 'mean'), ascending = False)
 .head())
```

```
##                           carat     
##                            mean size
## cut     color clarity               
## Ideal   J     I1       1.990000    2
## Premium I     I1       1.605833   24
##         J     I1       1.578462   13
##               SI2      1.554534  161
## Ideal   H     I1       1.475526   38
```

</details>

### More Examples {.tabset .tabset-fade .tabset-pills}

#### Transforming

| R                                | pandas                                                |
|----------------------------------|-------------------------------------------------------|
| `select(df, col_one = col1)`     | `df.rename(columns = {'col1': 'col_one'})['col_one']` |
| `rename(df, col_one = col1)[^2]` | `df.rename(columns = {'col1': 'col_one'})`            |
| `mutate(df, c = a - b)`          | `df.assign(c = df['a'] - df['b'])`                    |

[^2]: You can achieve the same result with `select()`. However, `rename()` can be helpful if you do not want to drop or add, or relocate columns.

#### Sorting

| R                                | pandas                                      |
|----------------------------------|---------------------------------------------|
| `arrange(df, col1, col2)`        | `df.sort_values(['col1', 'col2'])`          |
| `arrange(df, desc(col1))[^3]`    | `df.sort_values('col1', ascending = False)` |

[^3]: I personally prefer using `arrange(df, -col1)`

#### Grouping and Summarising

| R                                                                  | pandas                                      |
|--------------------------------------------------------------------|---------------------------------------------|
| `summary(df)`                                                      | `df.describe()`                             |
| `group_by(df, col1)`                                               | `df.groupby('col1')`                        |
| `group_by(df, col1) %>% summarise(avg = mean(col1, na.rm = TRUE))` | `df.groupby('col1').agg({'col1' : 'mean'})` |
| `group_by(df, col1) %>% summarise(total = sum(col1))`              | `df.groupby('col1').sum()`                  |



---
title: "Combinations-vs-Permutation"
author: "Justyn Rodrigues"
date: '2021-12-26'
slug: combinations-vs-permutation
categories:
- R
- Maths
tags:
- R
- tidyverse
subtitle: ''
summary: ''
authors: []
lastmod: '2021-12-26T14:06:37+11:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

## Possible Variations

-   When the order doesn't matter, it is a **combination**;
-   When the order does matter it is a **permutation**.

## Repetition

-   Repetition could be **allowed** in a situation where you wanted to know the character in a password (you can have multiple letters or numbers);
-   **No repetition** is when there is no replacement in the values such as lotto numbers or selecting a seat (you cannot sit where somebody is already sitting).

## Example

I had a gift card where two of the numbers were scratched off as I peeled back the scratchy thing. I did not want to contact the store if I could avoid that.

For example,

`A3E# - 3JH# - 45HL`

where the hashtags are the two values I can not see clearly. There are `36` possible values for each (`26` letters and `10` numbers), so figuring this out via bruteforce will take a long time. But how many possible numbers could it be?

Where

$$
\text{ Characters to choose from} = n
$$

$$
n = 36
$$

$$
\text{ Characters selected} = k
$$

$$
k = 2
$$

## Combinations

Pretending that order does not matter for our code or password, we could calculate the combinations by

$$
C_{k}^{\prime}(n) = \binom{n + k  - 1}{k}
$$

$$
C_{2}^{\prime}(36) = C_{2}(36 +2 - 1)
$$

$$
C_{2}(37) = \binom{37}{2} = \frac{37!}{2!(37 - 2)!} = \frac{37 \cdot 36}{2 \cdot 1} = 666
$$

If order did not matter and we could not have repetition then we would have

$$
C_{k}(n) = \binom{n}{k} = \frac{n!}{k!(n - k)!}
$$

$$
C_{2}(36) = \binom{36}{2} = \frac{36!}{2!(36 - 2)!} = \frac{36 \cdot 35}{2 \cdot 1} = 630
$$

## Permutation

This problem will be a permutation problem since the order is important since `A` and `5` is not the same as `5` and `A` due to both values being independent from each other. For example,

`A3EA - 3JH5 - 45HL` $!=$ `A3E5 - 3JHA - 45HL`

This is a simple solution since **repetition is allowed**. For example, both values could be the same. As such

$$
\text{Permutation} = P
$$

$$
P_{k}^{\prime} = n^{k}
$$

$$
P_{2}^{\prime} = 36^{2} = 1296
$$

However, lets just say in this situation **repetition is not allowed**. This would mean if the first character is `A` then the second character cannot be `A`. While this may seem like an obscure example in this example, imagine if the code was not entirely scratched off and you were certain that the two values were different from each other.

$$
P_{k}(n) = \frac{n!}{(n - k)}!
$$

$$
P_{2}(36) = \frac{36!}{(36-2)} = \frac{36!}{34!} = 36 \cdot 35 = 1260
$$

This should be fairly intuitive since `1296 - 1260 = 36`.

## Passwords

To finish here are the amount of unique combinations for a password of `6 characters`

| Characters Used                        | Possible Characters | Unique Permutations |
|----------------------------------------|---------------------|---------------------|
| `a - z`                                | 26                  | 308,915,776         |
| `a - z & 0 - 9`                        | 36                  | 2,176,782,336       |
| `a - z & A - Z`                        | 52                  | 19,770,609,664      |
| `a - z & A - Z & 0 - 9`                | 62                  | 56,800,235,584      |
| `a - z & A - Z & 0 - 9 & !@#$%^&*()+-` | 74                  | 164,206,490,176     |

and `8 characters`

| Characters Used                        | Possible Characters | Unique Permutations |
|----------------------------------------|---------------------|---------------------|
| `a - z`                                | 26                  | 208,827,064,576     |
| `a - z & 0 - 9`                        | 36                  | 2,821,109,907,456   |
| `a - z & A - Z`                        | 52                  | 53,459,728,531,456  |
| `a - z & A - Z & 0 - 9`                | 62                  | 218,340,105,584,896 |
| `a - z & A - Z & 0 - 9 & !@#$%^&*()+-` | 74                  | 899,194,740,203,776 |

If you want to calculate these values in `R` you can simply do it via

``` r
library(tidyverse)

crossing(
  # total characters 
  character_n = c(26, 36, 52, 62, 74),
  # password length
  length = c(6, 7, 8, 10, 12), 
  possible_values = character_n ^ length
)
```

---
title: "APA Styling in RMarkdown HTML"
author: "R package build"
date: '2021-06-16'
slug: apa-styling-in-rmarkdown
categories: []
tags:
- RMarkdown
- Markdown
- APA
subtitle: ''
summary: ''
authors: []
lastmod: '2021-06-16T14:39:46+10:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
bibliography: referen_bib.bib
link-citations: yes
csl: apa.csl
---

**Note:** this page is currently being updated.  
**Note 2:** it appears that pandoc makes it challenging for hanging references to appear with blogdown. I am currently finding a workout. The approach list below works for regular HTML, just not for blogdown.

Once I learnt how to format my reference list in APA format I switched over to RMarkdown for all my word processing because it was convenient to have the code and LaTeX available all in the same place. The process for formatting in APA is different for HTML and PDF so I will show how to do it in PDF another time.

<details>
Hello!
</details>

To reference in APA format you need two things

-   bibliography

-   style guide

#### Bibliography

The bibliography needs to be a BibTex file, which you can create with a referencing tool. I prefer to make it manually[^1] through `File > New File > Text file`

Screenshot

#### Style Guide

The default referencing style in RMarkdown is Chicago. Since we want to use APA, we have to specify the CSL (Citation Style Language) file in the metadata.

``` r
---
title: "APA Styling in RMarkdown"
author: "Justyn Rodrigues"
csl: apa.csl
bibliography: references.bib
link-citations: yes
---
```

To find the format, the [Zotero Style Repository](https://www.zotero.org/styles "referencing style formats") allows you to search and download regardless of the style you are looking for. Further, if you want to have a custom style, you can head over to <https://editor.citationstyles.org> to customise the style you want.

For the reference list[^2] to population you need to reference a citation from your bibliography by using square brackets `[ ]` with the `@` sign followed by the word input value inside the curly bracket for the specific reference.

For example, the best language is ([R Core Team, 2021](#ref-R-base)).

`For example, the best language is [@R-base].`

To get the BibTex citation for a package, you can use

``` r
toBibtex(citation("blogdown"))
```

    ## @Manual{,
    ##   title = {blogdown: Create Blogs and Websites with R Markdown},
    ##   author = {Yihui Xie and Christophe Dervieux and Alison Presmanes Hill},
    ##   year = {2021},
    ##   note = {R package version 1.3},
    ##   url = {https://github.com/rstudio/blogdown},
    ## }
    ## 
    ## @Book{,
    ##   title = {blogdown: Creating Websites with {R} Markdown},
    ##   author = {Yihui Xie and Alison Presmanes Hill and Amber Thomas},
    ##   publisher = {Chapman and Hall/CRC},
    ##   address = {Boca Raton, Florida},
    ##   year = {2017},
    ##   note = {ISBN 978-0815363729},
    ##   url = {https://bookdown.org/yihui/blogdown/},
    ## }

You can also write multiple package citations straight to the bibliography if you want.

``` r
knitr::write_bib(c("bookdown", "knitr", "rmarkdown", "tidyverse"), width = 60)
```

Knitr ([Xie, 2015](#ref-knitr2015)).  
RMarkdown ([Xie et al., 2020](#ref-rmarkdown2020)).

Further, if you want to cite multiple sources in the same citation, you simply add a semi colon between the two references `[@bookdown2016; @R-bookdown]`.

Bookdown ([Xie, 2016](#ref-bookdown2016), [2021](#ref-R-bookdown)).

For an in-text citation you simply do not use the square brackets `@tidyverse2019`.

Tidyverse [Wickham et al.](#ref-tidyverse2019) ([2019](#ref-tidyverse2019)).

# References

<div id="refs" class="references csl-bib-body hanging-indent" custom-style="Bibliography" line-spacing="2">

<div id="ref-R-base" class="csl-entry">

R Core Team. (2021). *R: A language and environment for statistical computing*. R Foundation for Statistical Computing. <https://www.R-project.org/>

</div>

<div id="ref-tidyverse2019" class="csl-entry">

Wickham, H., Averick, M., Bryan, J., Chang, W., McGowan, L. D., François, R., Grolemund, G., Hayes, A., Henry, L., Hester, J., Kuhn, M., Pedersen, T. L., Miller, E., Bache, S. M., Müller, K., Ooms, J., Robinson, D., Seidel, D. P., Spinu, V., … Yutani, H. (2019). Welcome to the <span class="nocase">tidyverse</span>. *Journal of Open Source Software*, *4*(43), 1686. <https://doi.org/10.21105/joss.01686>

</div>

<div id="ref-knitr2015" class="csl-entry">

Xie, Y. (2015). *Dynamic documents with R and knitr* (2nd ed.). Chapman; Hall/CRC. <https://yihui.org/knitr/>

</div>

<div id="ref-bookdown2016" class="csl-entry">

Xie, Y. (2016). *Bookdown: Authoring books and technical documents with R markdown*. Chapman; Hall/CRC. <https://bookdown.org/yihui/bookdown>

</div>

<div id="ref-R-bookdown" class="csl-entry">

Xie, Y. (2021). *Bookdown: Authoring books and technical documents with r markdown*. <https://CRAN.R-project.org/package=bookdown>

</div>

<div id="ref-rmarkdown2020" class="csl-entry">

Xie, Y., Dervieux, C., & Riederer, E. (2020). *R markdown cookbook*. Chapman; Hall/CRC. <https://bookdown.org/yihui/rmarkdown-cookbook>

</div>

</div>

[^1]: If you make the .bib file manually, make sure to save it in the same folder as your Rmarkdown file, and explicitly specific .bib as the extension.

[^2]: The reference list does not having hanging indents.

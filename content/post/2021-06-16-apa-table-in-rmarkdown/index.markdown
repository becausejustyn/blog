---
title: APA Table in Rmarkdown
author: R package build
date: '2021-06-16'
slug: apa-table-in-rmarkdown
categories: []
tags:
  - RMarkdown
  - Markdown
  - APA
subtitle: ''
summary: ''
authors: []
lastmod: '2021-06-16T16:43:30+10:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
output: 
  html_document:
    css: table_style.css
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

APA Table


```r
library(knitr)
library(kableExtra)
library(tidyverse)
```


```r
# Create table data
tab_01 = data.frame(
  scale = c("BAS-T", "SR", "BDI", "ASRM", "M-SRM"),
  high = c("46.17 (2.87)", "17.94 (1.88)", "7.11 (6.50)", 
           "6.46 (4.01)", "11.05 (3.36)"),
  moderate = c("37.99 (1.32)", "11.52 (1.84)", "6.18 (6.09)", 
               "5.63 (3.69)", "11.76 (2.75)"),
  p = c("<.001", "<.001", ".254", ".109", ".078")
)
```


```r
kable(
  tab_01,
  format = "html",
  col.names = c("Scale", "High BAS group", "Moderate BAS group", "*p*"),
  align = c("l", "c", "c", "c"),
  caption = "Means and Standard Deviations of Scores on Baseline Measures"
  )
```

<table>
<caption>Table 1: Means and Standard Deviations of Scores on Baseline Measures</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Scale </th>
   <th style="text-align:center;"> High BAS group </th>
   <th style="text-align:center;"> Moderate BAS group </th>
   <th style="text-align:center;"> *p* </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> BAS-T </td>
   <td style="text-align:center;"> 46.17 (2.87) </td>
   <td style="text-align:center;"> 37.99 (1.32) </td>
   <td style="text-align:center;"> &lt;.001 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> SR </td>
   <td style="text-align:center;"> 17.94 (1.88) </td>
   <td style="text-align:center;"> 11.52 (1.84) </td>
   <td style="text-align:center;"> &lt;.001 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> BDI </td>
   <td style="text-align:center;"> 7.11 (6.50) </td>
   <td style="text-align:center;"> 6.18 (6.09) </td>
   <td style="text-align:center;"> .254 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ASRM </td>
   <td style="text-align:center;"> 6.46 (4.01) </td>
   <td style="text-align:center;"> 5.63 (3.69) </td>
   <td style="text-align:center;"> .109 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> M-SRM </td>
   <td style="text-align:center;"> 11.05 (3.36) </td>
   <td style="text-align:center;"> 11.76 (2.75) </td>
   <td style="text-align:center;"> .078 </td>
  </tr>
</tbody>
</table>

**Table 1**

```r
kable(
  tab_01,
  format = "html",
  col.names = c("Scale", "High BAS group", "Moderate BAS group", "p"),
  align = c("l", "c", "c", "c"),
  caption = "Means and Standard Deviations of Scores on Baseline Measures"
  ) %>%
  kable_styling(full_width = TRUE) %>%
  row_spec(row = 0, align = "c") %>%
   footnote(
    general_title = "Note.",
    general = "Standard deviations are presented in parentheses. BAS = Behavioral Activation System; BAS-T = Behavioral Activation System-Total sores from the Behavioral Inhibition System/Behavioral Activation System Scales; SR = Sensitivity to Reward scores from the Sensitivity to Punishment and Sensitivity to Reward Questionnaire; BDI = Beck Depression Inventory scores; ASRM = Altman Self-Rating Mania Scale scores; M-SRM = Modified Social Rhythm Metric Regularity scores.",
   footnote_as_chunk = TRUE
    )
```

<table class="table" style="margin-left: auto; margin-right: auto;border-bottom: 0;">
<caption>Table 2: Means and Standard Deviations of Scores on Baseline Measures</caption>
 <thead>
  <tr>
   <th style="text-align:left;text-align: center;"> Scale </th>
   <th style="text-align:center;text-align: center;"> High BAS group </th>
   <th style="text-align:center;text-align: center;"> Moderate BAS group </th>
   <th style="text-align:center;text-align: center;"> p </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> BAS-T </td>
   <td style="text-align:center;"> 46.17 (2.87) </td>
   <td style="text-align:center;"> 37.99 (1.32) </td>
   <td style="text-align:center;"> &lt;.001 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> SR </td>
   <td style="text-align:center;"> 17.94 (1.88) </td>
   <td style="text-align:center;"> 11.52 (1.84) </td>
   <td style="text-align:center;"> &lt;.001 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> BDI </td>
   <td style="text-align:center;"> 7.11 (6.50) </td>
   <td style="text-align:center;"> 6.18 (6.09) </td>
   <td style="text-align:center;"> .254 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ASRM </td>
   <td style="text-align:center;"> 6.46 (4.01) </td>
   <td style="text-align:center;"> 5.63 (3.69) </td>
   <td style="text-align:center;"> .109 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> M-SRM </td>
   <td style="text-align:center;"> 11.05 (3.36) </td>
   <td style="text-align:center;"> 11.76 (2.75) </td>
   <td style="text-align:center;"> .078 </td>
  </tr>
</tbody>
<tfoot><tr><td style="padding: 0; " colspan="100%">
<span style="font-style: italic;">Note.</span> <sup></sup> Standard deviations are presented in parentheses. BAS = Behavioral Activation System; BAS-T = Behavioral Activation System-Total sores from the Behavioral Inhibition System/Behavioral Activation System Scales; SR = Sensitivity to Reward scores from the Sensitivity to Punishment and Sensitivity to Reward Questionnaire; BDI = Beck Depression Inventory scores; ASRM = Altman Self-Rating Mania Scale scores; M-SRM = Modified Social Rhythm Metric Regularity scores.</td></tr></tfoot>
</table>

Styling the Table Using CSS

Under the RStudio File menu, select New File > Text File

Save this file as table_style.css in the exact same folder as your RMD file. The file extension css indicate that this is a CSS file.

Next, we need to tell your RMarkdown file to look at this file for its styling rules. We do this in the YAML of your RMD document. Change your YAML as follows:


```r
---
title: "Untitled"
author: "Andrew Zieffler"
date: "1/12/2020"
output: 
  html_document:
    css: table_style.css
---
```

Now we can our styling rules to the CSS file. You can add the following syntax to table-style.css.


```css
/** Change border color to black **/
.table>thead>tr>th {
  border-color: black;
}


/** Remove borders within the table body **/
.table>tbody>tr>td {
  border: none;
}


/** Add a top border to the table header row **/
.table thead tr:first-child { 
  border-top: 2px solid black;
}


/** Add a bottom border to the table body **/
.table tbody tr:last-child {
  border-bottom: 2px solid black;
}


/** Make the table header row a normal weight; not bold **/
.table th{
  font-weight: normal;
}


/** Make the caption italic and black **/
.table caption{
  font-style: italic;
  color: black;
}
```






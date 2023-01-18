---
title: 'QALL401: Data Analysis for Researchers'
output:
  ioslides_presentation: 
    df_print: paged
    smaller: yes
    keep_md: yes
  html_document:
    df_print: paged
    number_sections: yes
    toc: yes
    toc_float: yes
  beamer_presentation: default
  pdf_document:
    number_sections: yes
  html_notebook:
    number_sections: yes
    toc: yes
    toc_float: yes
---

## Course Contents {-}

1. 2022.12.07: Introduction: About the course [lead by TK]
    - An introduction to open and public data, and data science
2. 2022-12-14: Exploratory Data Analysis (EDA) 1 [lead by hs]  
    - R Basics with RStudio and/or RStudio.cloud; Toy Data
3. 2022-12-21: Exploratory Data Analysis (EDA) 2 [lead by hs]   
    - R Markdown, `tidyverse` I: `dplyr`; `gapminder`
4. 2023-01-11: Exploratory Data Analysis (EDA) 3 [lead by hs]  
    - `tidyverse`II: `readr`, `ggplot2`; Public Data, WDI, WIR, etc
5. **2023-01-18: Exploratory Data Analysis (EDA) 4 [lead by hs]**  
    - `tidyverse` III: `tidyr`, etc.; WDI, WIR, etc
6. 2023-01-25: Exploratory Data Analysis (EDA) 5 [lead by hs]  
    - `tidyverse` IV; WDI, WIR, etc
7. 2023-02-01: Introduction to PPDAC         
    - Problem-Plan-Data-Analysis-Conclusion Cycle: [lead by TK]
8. 2023-02-08: Model building I [lead by TK]    
    - Collecting and visualizing data and Introduction to WDI  
         (World Development Indicators by World Bank)
9. 2023-02-15: Model building II [lead by TK]    
    - Analyzing data and communications
10. 2023-02-22: Project Presentation


# Exploratory Data Analysis (EDA) I

# Exploratory Data Analysis II

# Exploratory Data Analysis III  



# Exploratory Data Analysis (EDA) IV  

## Tidy Data

### Reviews and Previews

### Example: World Inequility Report - WIR2022

* World Inequality Report: https://wir2022.wid.world/
* Executive Summary: https://wir2022.wid.world/executive-summary/
* Methodology: https://wir2022.wid.world/methodology/
* Data URL: https://wir2022.wid.world/www-site/uploads/2022/03/WIR2022TablesFigures-Summary.xlsx


```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(readxl)
```


```r
url_summary <- "https://wir2022.wid.world/www-site/uploads/2022/03/WIR2022TablesFigures-Summary.xlsx"
download.file(url = url_summary, destfile = "data/WIR2022s.xlsx") 
```


```r
excel_sheets("data/WIR2022s.xlsx")
```

```
##  [1] "Index"     "F1"        "F2"        "F3"        "F4"        "F5."      
##  [7] "F6"        "F7"        "F8"        "F9"        "F10"       "F11"      
## [13] "F12"       "F13"       "F14"       "F15"       "T1"        "data-F1"  
## [19] "data-F2"   "data-F3"   "data-F4"   "data-F5"   "data-F6"   "data-F7"  
## [25] "data-F8"   "data-F9"   "data-F10"  "data-F11"  "data-F12"  "data-F13."
## [31] "data-F14." "data-F15"
```

---

### F1: Global income and wealth inequality, 2021


```r
df_f1 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F1")
df_f1
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["...1"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Bottom 50%"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["Middle 40%"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Top 10%"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["Top 1%"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"Income","2":"0.0840","3":"0.3942","4":"0.5217","5":"0.1925"},{"1":"Wealth","2":"0.0199","3":"0.2245","4":"0.7556","5":"0.3779"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>



<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["cat"],"name":[1],"type":["chr"],"align":["left"]},{"label":["group"],"name":[2],"type":["chr"],"align":["left"]},{"label":["value"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Income","2":"Bottom 50%","3":"0.0840"},{"1":"Income","2":"Middle 40%","3":"0.3942"},{"1":"Income","2":"Top 10%","3":"0.5217"},{"1":"Wealth","2":"Bottom 50%","3":"0.0199"},{"1":"Wealth","2":"Middle 40%","3":"0.2245"},{"1":"Wealth","2":"Top 10%","3":"0.7556"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f1_rev %>%
  ggplot(aes(x = cat, y = value, fill = group)) +
  geom_col(position = "dodge")
```

![](eda4_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

---

### References of `tidyr`

* Textbook: [R for Data Science,Tidy Data](https://r4ds.had.co.nz/tidy-data.html#tidy-data)

#### RStudio Primers: See References in Moodle at the bottom

**Tidy Your Data**

  - Reshape Data
  - Separate and Unite Columns
  - Join Data Sets
  
---

### Variables, values, and observations: Definitions

* A **variable** is a quantity, quality, or property that you can measure.
* A **value** is the state of a variable when you measure it. The value of a variable may change from measurement to measurement.
* An **observation** or **case** is a set of measurements made under similar conditions (you usually make all of the measurements in an observation at the same time and on the same object). An observation will contain several values, each associated with a different variable. I’ll sometimes refer to an observation as a case or data point.
* **Tabular data** is a table of values, each associated with a variable and an observation. Tabular data is tidy if each value is placed in its own cell, each variable in its own column, and each observation in its own row.
* So far, all of the data that you’ve seen has been tidy. In real-life, most data isn’t tidy, so we’ll come back to these ideas again in Data Wrangling.

---

### Tidy Data

> “Data comes in many formats, but R prefers just one: tidy data.” — Garrett Grolemund

Data can come in a variety of formats, but one format is easier to use in R than the others. This format is known as tidy data. A data set is tidy if:

1. Each variable is in its own column
2. Each observation is in its own row
3. Each value is in its own cell (this follows from #1 and #2)

> “Tidy data sets are all alike; but every messy data set is messy in its own way.” — Hadley Wickham

> “all happy families are all alike; each unhappy family is unhappy in its own way” - Tolstoy's Anna Karenina

---

### `tidyr` Basics

<img src="data/tidy-1.png" width="100%" />

1. Each variable is in its own column
2. Each observation is in its own row

---

### Pivot data from wide to long: [`pivot_longer()`](https://tidyr.tidyverse.org/reference/pivot_longer.html)

```
pivot_longer(data, cols = <columns to pivot into longer format>,
  names_to = <name of the new character column>, # e.g. "group", "category", "class"
  values_to = <name of the column the values of cells go to>) # e.g. "value", "n"
```


```r
df_f1
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["...1"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Bottom 50%"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["Middle 40%"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Top 10%"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["Top 1%"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"Income","2":"0.0840","3":"0.3942","4":"0.5217","5":"0.1925"},{"1":"Wealth","2":"0.0199","3":"0.2245","4":"0.7556","5":"0.3779"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>


```r
(df_f1_rev <- df_f1 %>% pivot_longer(-1, names_to = "group", values_to = "value"))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["...1"],"name":[1],"type":["chr"],"align":["left"]},{"label":["group"],"name":[2],"type":["chr"],"align":["left"]},{"label":["value"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"Income","2":"Bottom 50%","3":"0.0840"},{"1":"Income","2":"Middle 40%","3":"0.3942"},{"1":"Income","2":"Top 10%","3":"0.5217"},{"1":"Income","2":"Top 1%","3":"0.1925"},{"1":"Wealth","2":"Bottom 50%","3":"0.0199"},{"1":"Wealth","2":"Middle 40%","3":"0.2245"},{"1":"Wealth","2":"Top 10%","3":"0.7556"},{"1":"Wealth","2":"Top 1%","3":"0.3779"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f1_rev %>% 
  ggplot(aes(x = ...1, y = value, fill = group)) +
  geom_col(position = "dodge")
```

![](eda4_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

---


```r
df_f1_rev %>% filter(group != "Top 1%") %>%
  ggplot() +
  geom_col(aes(x = ...1, y = value, fill = group), position = "dodge") +
  geom_text(aes(x = ...1, y = value, group = group, 
            label = scales::label_percent(accuracy=1)(value)), 
            position = position_dodge(width = 0.9)) + 
  scale_y_continuous(labels = scales::percent_format(accuracy = 1)) +
  labs(title = "Figure 1. Global income and wealth inequality, 2021",
       x = "", y = "Share of total income or wealth", fill = "")
```

---

![](eda4_files/figure-html/unnamed-chunk-10-1.png)<!-- -->
**Interpretation**: The global bottom 50% captures 8.5% of total income measured at Purchasing Power Parity (PPP). The global bottom 50% owns 2% of wealth (at Purchasing Power Parity). The global top 10% owns 76% of total Household wealth and captures 52% of total income in 2021. Note that top wealth holders are not necessarily top income holders. Incomes are measured after the operation of pension and unemployment systems and before taxes and transfers.  
**Sources and series**: wir2022.wid.world/methodology.

---

### F2: The poorest half lags behind: Bottom 50%, middle 40% and top 10% income shares across the world in 2021


```r
df_f2 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F2")
df_f2
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["iso"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Bottom 50%"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Middle 40%"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["Top 10%"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"2021","2":"Europe","3":"0.1891","4":"0.4531","5":"0.3578"},{"1":"2021","2":"East Asia","3":"0.1391","4":"0.4268","5":"0.4341"},{"1":"2021","2":"North America","3":"0.1322","4":"0.4105","5":"0.4573"},{"1":"2021","2":"Russia & Central Asia","3":"0.1466","4":"0.3863","5":"0.4671"},{"1":"2021","2":"South & South East Asia","3":"0.1233","4":"0.3283","5":"0.5484"},{"1":"2021","2":"Latin America","3":"0.1016","4":"0.3445","5":"0.5539"},{"1":"2021","2":"Sub-Saharan Africa","3":"0.0892","4":"0.3537","5":"0.5571"},{"1":"2021","2":"MENA","3":"0.0900","4":"0.3288","5":"0.5812"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f2 %>% pivot_longer(cols = 3:5, names_to = "group", values_to = "value")
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["iso"],"name":[2],"type":["chr"],"align":["left"]},{"label":["group"],"name":[3],"type":["chr"],"align":["left"]},{"label":["value"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"2021","2":"Europe","3":"Bottom 50%","4":"0.1891"},{"1":"2021","2":"Europe","3":"Middle 40%","4":"0.4531"},{"1":"2021","2":"Europe","3":"Top 10%","4":"0.3578"},{"1":"2021","2":"East Asia","3":"Bottom 50%","4":"0.1391"},{"1":"2021","2":"East Asia","3":"Middle 40%","4":"0.4268"},{"1":"2021","2":"East Asia","3":"Top 10%","4":"0.4341"},{"1":"2021","2":"North America","3":"Bottom 50%","4":"0.1322"},{"1":"2021","2":"North America","3":"Middle 40%","4":"0.4105"},{"1":"2021","2":"North America","3":"Top 10%","4":"0.4573"},{"1":"2021","2":"Russia & Central Asia","3":"Bottom 50%","4":"0.1466"},{"1":"2021","2":"Russia & Central Asia","3":"Middle 40%","4":"0.3863"},{"1":"2021","2":"Russia & Central Asia","3":"Top 10%","4":"0.4671"},{"1":"2021","2":"South & South East Asia","3":"Bottom 50%","4":"0.1233"},{"1":"2021","2":"South & South East Asia","3":"Middle 40%","4":"0.3283"},{"1":"2021","2":"South & South East Asia","3":"Top 10%","4":"0.5484"},{"1":"2021","2":"Latin America","3":"Bottom 50%","4":"0.1016"},{"1":"2021","2":"Latin America","3":"Middle 40%","4":"0.3445"},{"1":"2021","2":"Latin America","3":"Top 10%","4":"0.5539"},{"1":"2021","2":"Sub-Saharan Africa","3":"Bottom 50%","4":"0.0892"},{"1":"2021","2":"Sub-Saharan Africa","3":"Middle 40%","4":"0.3537"},{"1":"2021","2":"Sub-Saharan Africa","3":"Top 10%","4":"0.5571"},{"1":"2021","2":"MENA","3":"Bottom 50%","4":"0.0900"},{"1":"2021","2":"MENA","3":"Middle 40%","4":"0.3288"},{"1":"2021","2":"MENA","3":"Top 10%","4":"0.5812"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f2 %>% pivot_longer(cols = 3:5, names_to = "group", values_to = "value") %>%
  ggplot(aes(x = iso, y = value, fill = group)) +
  geom_col(position = "dodge")
```

![](eda4_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

---

### Pivot data from long to wide: 
[`pivot_wider()`](https://tidyr.tidyverse.org/reference/pivot_wider.html)
In Console: vignette("pivot") 

```
pivot_wider(data, 
  names_from = <name of the column (or columns) to get the name of the output column>,
  values_from = <name of the column to get the value of the output>) 
```


---

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["iso"],"name":[2],"type":["chr"],"align":["left"]},{"label":["group"],"name":[3],"type":["chr"],"align":["left"]},{"label":["value"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"2021","2":"Europe","3":"Bottom 50%","4":"0.1891"},{"1":"2021","2":"Europe","3":"Middle 40%","4":"0.4531"},{"1":"2021","2":"Europe","3":"Top 10%","4":"0.3578"},{"1":"2021","2":"East Asia","3":"Bottom 50%","4":"0.1391"},{"1":"2021","2":"East Asia","3":"Middle 40%","4":"0.4268"},{"1":"2021","2":"East Asia","3":"Top 10%","4":"0.4341"},{"1":"2021","2":"North America","3":"Bottom 50%","4":"0.1322"},{"1":"2021","2":"North America","3":"Middle 40%","4":"0.4105"},{"1":"2021","2":"North America","3":"Top 10%","4":"0.4573"},{"1":"2021","2":"Russia & Central Asia","3":"Bottom 50%","4":"0.1466"},{"1":"2021","2":"Russia & Central Asia","3":"Middle 40%","4":"0.3863"},{"1":"2021","2":"Russia & Central Asia","3":"Top 10%","4":"0.4671"},{"1":"2021","2":"South & South East Asia","3":"Bottom 50%","4":"0.1233"},{"1":"2021","2":"South & South East Asia","3":"Middle 40%","4":"0.3283"},{"1":"2021","2":"South & South East Asia","3":"Top 10%","4":"0.5484"},{"1":"2021","2":"Latin America","3":"Bottom 50%","4":"0.1016"},{"1":"2021","2":"Latin America","3":"Middle 40%","4":"0.3445"},{"1":"2021","2":"Latin America","3":"Top 10%","4":"0.5539"},{"1":"2021","2":"Sub-Saharan Africa","3":"Bottom 50%","4":"0.0892"},{"1":"2021","2":"Sub-Saharan Africa","3":"Middle 40%","4":"0.3537"},{"1":"2021","2":"Sub-Saharan Africa","3":"Top 10%","4":"0.5571"},{"1":"2021","2":"MENA","3":"Bottom 50%","4":"0.0900"},{"1":"2021","2":"MENA","3":"Middle 40%","4":"0.3288"},{"1":"2021","2":"MENA","3":"Top 10%","4":"0.5812"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

```
pivot_wider(data, names_from = group, values_from = value) 
```

---

### Practice: F4 and F13

F4 and F13 are similar. Please use `pivot_longer` to tidy the data and create charts.

* **References**: https://ds-sl.github.io/data-analysis/wir2022.nb.html

#### Done Last Week

* F12: Female share in global labor incomes, 1990-2020
* F14: Global carbon inequality, 2019. Group contribution to world emissions (%)

---

### F3: Top 10/Bottom 50 income gaps across the world, 2021



```r
df_f3 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F3")
df_f3
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Country"],"name":[2],"type":["chr"],"align":["left"]},{"label":["T10B50"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"2021","2":"United Arab Emirates","3":"19.204010"},{"1":"2021","2":"Afghanistan","3":"11.669610"},{"1":"2021","2":"Albania","3":"8.989956"},{"1":"2021","2":"Armenia","3":"10.957560"},{"1":"2021","2":"Angola","3":"32.092700"},{"1":"2021","2":"Argentina","3":"13.180250"},{"1":"2021","2":"Austria","3":"7.679657"},{"1":"2021","2":"Australia","3":"10.393100"},{"1":"2021","2":"Azerbaijan","3":"9.630005"},{"1":"2021","2":"Bosnia and Herzegovina","3":"9.321850"},{"1":"2021","2":"Bangladesh","3":"12.561270"},{"1":"2021","2":"Belgium","3":"8.060792"},{"1":"2021","2":"Burkina Faso","3":"15.711230"},{"1":"2021","2":"Bulgaria","3":"13.200160"},{"1":"2021","2":"Bahrain","3":"28.280580"},{"1":"2021","2":"Burundi","3":"17.261540"},{"1":"2021","2":"Benin","3":"23.977820"},{"1":"2021","2":"Brunei Darussalam","3":"9.823530"},{"1":"2021","2":"Bolivia","3":"19.253270"},{"1":"2021","2":"Brazil","3":"29.074700"},{"1":"2021","2":"Bahamas","3":"19.253280"},{"1":"2021","2":"Bhutan","3":"14.184000"},{"1":"2021","2":"Botswana","3":"36.492850"},{"1":"2021","2":"Belarus","3":"7.417274"},{"1":"2021","2":"Belize","3":"19.253270"},{"1":"2021","2":"Canada","3":"13.057890"},{"1":"2021","2":"DR Congo","3":"19.317310"},{"1":"2021","2":"Central African Republic","3":"42.524850"},{"1":"2021","2":"Congo","3":"28.200510"},{"1":"2021","2":"Switzerland","3":"7.176620"},{"1":"2021","2":"Cote d'Ivoire","3":"23.599090"},{"1":"2021","2":"Chile","3":"28.942710"},{"1":"2021","2":"Cameroon","3":"24.472310"},{"1":"2021","2":"China","3":"14.505120"},{"1":"2021","2":"Colombia","3":"24.207660"},{"1":"2021","2":"Costa Rica","3":"23.365570"},{"1":"2020","2":"Cuba","3":"11.863260"},{"1":"2021","2":"Cabo Verde","3":"19.826510"},{"1":"2021","2":"Cyprus","3":"9.494887"},{"1":"2021","2":"Czech Republic","3":"5.607577"},{"1":"2021","2":"Germany","3":"9.760151"},{"1":"2021","2":"Djibouti","3":"18.932130"},{"1":"2021","2":"Denmark","3":"7.918193"},{"1":"2021","2":"Dominican Republic","3":"19.253270"},{"1":"2021","2":"Algeria","3":"10.012040"},{"1":"2021","2":"Ecuador","3":"11.562460"},{"1":"2021","2":"Estonia","3":"9.522069"},{"1":"2021","2":"Egypt","3":"16.815820"},{"1":"2021","2":"Eritrea","3":"14.358130"},{"1":"2021","2":"Spain","3":"8.161876"},{"1":"2021","2":"Ethiopia","3":"14.358130"},{"1":"2021","2":"Finland","3":"7.900719"},{"1":"2021","2":"France","3":"7.091090"},{"1":"2021","2":"Gabon","3":"15.022300"},{"1":"2021","2":"United Kingdom","3":"8.766573"},{"1":"2021","2":"Georgia","3":"17.632930"},{"1":"2021","2":"Ghana","3":"20.029220"},{"1":"2021","2":"Gambia","3":"15.270910"},{"1":"2021","2":"Guinea","3":"13.182330"},{"1":"2021","2":"Equatorial Guinea","3":"22.545290"},{"1":"2021","2":"Greece","3":"7.759043"},{"1":"2021","2":"Guatemala","3":"19.253280"},{"1":"2021","2":"Guinea-Bissau","3":"31.343620"},{"1":"2021","2":"Guyana","3":"19.253280"},{"1":"2021","2":"Hong Kong","3":"17.724050"},{"1":"2021","2":"Honduras","3":"19.253270"},{"1":"2021","2":"Croatia","3":"9.613139"},{"1":"2021","2":"Haiti","3":"19.253280"},{"1":"2021","2":"Hungary","3":"7.691266"},{"1":"2021","2":"Indonesia","3":"19.366180"},{"1":"2021","2":"Ireland","3":"8.603584"},{"1":"2021","2":"Israel","3":"18.668620"},{"1":"2021","2":"India","3":"21.757670"},{"1":"2021","2":"Iraq","3":"20.355850"},{"1":"2021","2":"Iran","3":"19.828190"},{"1":"2021","2":"Iceland","3":"5.820321"},{"1":"2021","2":"Italy","3":"7.778762"},{"1":"2021","2":"Jamaica","3":"19.253280"},{"1":"2021","2":"Jordan","3":"17.331080"},{"1":"2021","2":"Japan","3":"13.378050"},{"1":"2021","2":"Kenya","3":"18.716540"},{"1":"2021","2":"Kyrgyzstan","3":"13.124270"},{"1":"2021","2":"Cambodia","3":"16.773860"},{"1":"2021","2":"Comoros","3":"22.056120"},{"1":"2020","2":"North Korea","3":"14.112850"},{"1":"2021","2":"Korea","3":"14.481250"},{"1":"2020","2":"Kosovo","3":"8.973072"},{"1":"2021","2":"Kuwait","3":"22.994100"},{"1":"2021","2":"Kazakhstan","3":"12.997360"},{"1":"2021","2":"Lao PDR","3":"19.256650"},{"1":"2020","2":"Lebanon","3":"26.646230"},{"1":"2021","2":"Sri Lanka","3":"17.520910"},{"1":"2021","2":"Liberia","3":"14.011740"},{"1":"2021","2":"Lesotho","3":"21.941270"},{"1":"2021","2":"Lithuania","3":"10.126340"},{"1":"2021","2":"Luxembourg","3":"8.303045"},{"1":"2021","2":"Latvia","3":"9.637069"},{"1":"2021","2":"Libya","3":"13.529750"},{"1":"2021","2":"Morocco","3":"18.229160"},{"1":"2021","2":"Moldova","3":"9.451350"},{"1":"2021","2":"Montenegro","3":"10.890540"},{"1":"2021","2":"Madagascar","3":"20.333440"},{"1":"2021","2":"North Macedonia","3":"6.978232"},{"1":"2021","2":"Mali","3":"12.629370"},{"1":"2021","2":"Myanmar","3":"13.833160"},{"1":"2021","2":"Mongolia","3":"14.836730"},{"1":"2021","2":"Macao","3":"14.505120"},{"1":"2021","2":"Mauritania","3":"12.059080"},{"1":"2021","2":"Malta","3":"7.931879"},{"1":"2021","2":"Mauritius","3":"16.007260"},{"1":"2021","2":"Maldives","3":"11.063860"},{"1":"2021","2":"Malawi","3":"23.939230"},{"1":"2021","2":"Mexico","3":"31.262120"},{"1":"2021","2":"Malaysia","3":"11.641520"},{"1":"2021","2":"Mozambique","3":"38.944060"},{"1":"2021","2":"Namibia","3":"49.030030"},{"1":"2021","2":"Niger","3":"13.774560"},{"1":"2021","2":"Nigeria","3":"13.784810"},{"1":"2021","2":"Nicaragua","3":"19.253270"},{"1":"2021","2":"Netherlands","3":"6.539901"},{"1":"2021","2":"Norway","3":"5.956634"},{"1":"2021","2":"Nepal","3":"12.570650"},{"1":"2021","2":"New Zealand","3":"8.832035"},{"1":"2021","2":"Oman","3":"139.590900"},{"1":"2021","2":"Panama","3":"19.253280"},{"1":"2021","2":"Peru","3":"22.248380"},{"1":"2021","2":"Papua New Guinea","3":"18.281150"},{"1":"2021","2":"Philippines","3":"16.094840"},{"1":"2021","2":"Pakistan","3":"12.525410"},{"1":"2021","2":"Poland","3":"9.694258"},{"1":"2021","2":"Palestine","3":"21.060580"},{"1":"2021","2":"Portugal","3":"8.785279"},{"1":"2021","2":"Paraguay","3":"19.253280"},{"1":"2021","2":"Qatar","3":"30.238270"},{"1":"2021","2":"Romania","3":"13.672130"},{"1":"2021","2":"Serbia","3":"9.652961"},{"1":"2021","2":"Russian Federation","3":"13.670900"},{"1":"2021","2":"Rwanda","3":"22.775260"},{"1":"2021","2":"Saudi Arabia","3":"24.654720"},{"1":"2021","2":"Seychelles","3":"21.471810"},{"1":"2021","2":"Sudan","3":"14.281640"},{"1":"2021","2":"Sweden","3":"6.471685"},{"1":"2021","2":"Singapore","3":"13.900120"},{"1":"2021","2":"Slovenia","3":"6.411677"},{"1":"2021","2":"Slovakia","3":"5.393878"},{"1":"2021","2":"Sierra Leone","3":"15.675510"},{"1":"2021","2":"Senegal","3":"17.830500"},{"1":"2021","2":"Somalia","3":"14.744090"},{"1":"2021","2":"Suriname","3":"19.253280"},{"1":"2021","2":"South Sudan","3":"20.991060"},{"1":"2021","2":"Sao Tome and Principe","3":"11.253070"},{"1":"2021","2":"El Salvador","3":"17.586230"},{"1":"2020","2":"Syrian Arab Republic","3":"26.545660"},{"1":"2021","2":"Swaziland","3":"38.112220"},{"1":"2021","2":"Chad","3":"20.046880"},{"1":"2021","2":"Togo","3":"19.635430"},{"1":"2021","2":"Thailand","3":"17.565470"},{"1":"2021","2":"Tajikistan","3":"14.004820"},{"1":"2021","2":"Timor-Leste","3":"12.634010"},{"1":"2021","2":"Turkmenistan","3":"20.770220"},{"1":"2021","2":"Tunisia","3":"12.450550"},{"1":"2021","2":"Turkey","3":"22.779770"},{"1":"2021","2":"Trinidad and Tobago","3":"19.253270"},{"1":"2021","2":"Taiwan","3":"8.426919"},{"1":"2021","2":"Tanzania","3":"19.837950"},{"1":"2021","2":"Ukraine","3":"7.419922"},{"1":"2021","2":"Uganda","3":"21.469920"},{"1":"2021","2":"USA","3":"17.077610"},{"1":"2021","2":"Uruguay","3":"10.960740"},{"1":"2021","2":"Uzbekistan","3":"15.865990"},{"1":"2020","2":"Venezuela","3":"19.253270"},{"1":"2021","2":"Viet Nam","3":"15.394770"},{"1":"2021","2":"Yemen","3":"31.963060"},{"1":"2021","2":"South Africa","3":"63.098640"},{"1":"2021","2":"Zambia","3":"44.420860"},{"1":"2021","2":"Zimbabwe","3":"31.924770"},{"1":"2021","2":"Zanzibar","3":"19.837950"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

### F3: Top 10/Bottom 50 income gaps across the world, 2021 - Original

<img src="data/F3.png" width="100%" />

---

* To 10 / Bottom 50 ratio has 5 classes: 5-12, 12-13, 13-16, 16-19, 19-140


```r
df_f3$T10B50 %>% summary()
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   5.394  10.958  15.676  17.635  19.838 139.591
```

---


```r
df_f3 %>% ggplot() + geom_histogram(aes(T10B50))
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](eda4_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

---


```r
df_f3 %>% arrange(desc(T10B50))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Country"],"name":[2],"type":["chr"],"align":["left"]},{"label":["T10B50"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"2021","2":"Oman","3":"139.590900"},{"1":"2021","2":"South Africa","3":"63.098640"},{"1":"2021","2":"Namibia","3":"49.030030"},{"1":"2021","2":"Zambia","3":"44.420860"},{"1":"2021","2":"Central African Republic","3":"42.524850"},{"1":"2021","2":"Mozambique","3":"38.944060"},{"1":"2021","2":"Swaziland","3":"38.112220"},{"1":"2021","2":"Botswana","3":"36.492850"},{"1":"2021","2":"Angola","3":"32.092700"},{"1":"2021","2":"Yemen","3":"31.963060"},{"1":"2021","2":"Zimbabwe","3":"31.924770"},{"1":"2021","2":"Guinea-Bissau","3":"31.343620"},{"1":"2021","2":"Mexico","3":"31.262120"},{"1":"2021","2":"Qatar","3":"30.238270"},{"1":"2021","2":"Brazil","3":"29.074700"},{"1":"2021","2":"Chile","3":"28.942710"},{"1":"2021","2":"Bahrain","3":"28.280580"},{"1":"2021","2":"Congo","3":"28.200510"},{"1":"2020","2":"Lebanon","3":"26.646230"},{"1":"2020","2":"Syrian Arab Republic","3":"26.545660"},{"1":"2021","2":"Saudi Arabia","3":"24.654720"},{"1":"2021","2":"Cameroon","3":"24.472310"},{"1":"2021","2":"Colombia","3":"24.207660"},{"1":"2021","2":"Benin","3":"23.977820"},{"1":"2021","2":"Malawi","3":"23.939230"},{"1":"2021","2":"Cote d'Ivoire","3":"23.599090"},{"1":"2021","2":"Costa Rica","3":"23.365570"},{"1":"2021","2":"Kuwait","3":"22.994100"},{"1":"2021","2":"Turkey","3":"22.779770"},{"1":"2021","2":"Rwanda","3":"22.775260"},{"1":"2021","2":"Equatorial Guinea","3":"22.545290"},{"1":"2021","2":"Peru","3":"22.248380"},{"1":"2021","2":"Comoros","3":"22.056120"},{"1":"2021","2":"Lesotho","3":"21.941270"},{"1":"2021","2":"India","3":"21.757670"},{"1":"2021","2":"Seychelles","3":"21.471810"},{"1":"2021","2":"Uganda","3":"21.469920"},{"1":"2021","2":"Palestine","3":"21.060580"},{"1":"2021","2":"South Sudan","3":"20.991060"},{"1":"2021","2":"Turkmenistan","3":"20.770220"},{"1":"2021","2":"Iraq","3":"20.355850"},{"1":"2021","2":"Madagascar","3":"20.333440"},{"1":"2021","2":"Chad","3":"20.046880"},{"1":"2021","2":"Ghana","3":"20.029220"},{"1":"2021","2":"Tanzania","3":"19.837950"},{"1":"2021","2":"Zanzibar","3":"19.837950"},{"1":"2021","2":"Iran","3":"19.828190"},{"1":"2021","2":"Cabo Verde","3":"19.826510"},{"1":"2021","2":"Togo","3":"19.635430"},{"1":"2021","2":"Indonesia","3":"19.366180"},{"1":"2021","2":"DR Congo","3":"19.317310"},{"1":"2021","2":"Lao PDR","3":"19.256650"},{"1":"2021","2":"Bahamas","3":"19.253280"},{"1":"2021","2":"Guatemala","3":"19.253280"},{"1":"2021","2":"Guyana","3":"19.253280"},{"1":"2021","2":"Haiti","3":"19.253280"},{"1":"2021","2":"Jamaica","3":"19.253280"},{"1":"2021","2":"Panama","3":"19.253280"},{"1":"2021","2":"Paraguay","3":"19.253280"},{"1":"2021","2":"Suriname","3":"19.253280"},{"1":"2021","2":"Bolivia","3":"19.253270"},{"1":"2021","2":"Belize","3":"19.253270"},{"1":"2021","2":"Dominican Republic","3":"19.253270"},{"1":"2021","2":"Honduras","3":"19.253270"},{"1":"2021","2":"Nicaragua","3":"19.253270"},{"1":"2021","2":"Trinidad and Tobago","3":"19.253270"},{"1":"2020","2":"Venezuela","3":"19.253270"},{"1":"2021","2":"United Arab Emirates","3":"19.204010"},{"1":"2021","2":"Djibouti","3":"18.932130"},{"1":"2021","2":"Kenya","3":"18.716540"},{"1":"2021","2":"Israel","3":"18.668620"},{"1":"2021","2":"Papua New Guinea","3":"18.281150"},{"1":"2021","2":"Morocco","3":"18.229160"},{"1":"2021","2":"Senegal","3":"17.830500"},{"1":"2021","2":"Hong Kong","3":"17.724050"},{"1":"2021","2":"Georgia","3":"17.632930"},{"1":"2021","2":"El Salvador","3":"17.586230"},{"1":"2021","2":"Thailand","3":"17.565470"},{"1":"2021","2":"Sri Lanka","3":"17.520910"},{"1":"2021","2":"Jordan","3":"17.331080"},{"1":"2021","2":"Burundi","3":"17.261540"},{"1":"2021","2":"USA","3":"17.077610"},{"1":"2021","2":"Egypt","3":"16.815820"},{"1":"2021","2":"Cambodia","3":"16.773860"},{"1":"2021","2":"Philippines","3":"16.094840"},{"1":"2021","2":"Mauritius","3":"16.007260"},{"1":"2021","2":"Uzbekistan","3":"15.865990"},{"1":"2021","2":"Burkina Faso","3":"15.711230"},{"1":"2021","2":"Sierra Leone","3":"15.675510"},{"1":"2021","2":"Viet Nam","3":"15.394770"},{"1":"2021","2":"Gambia","3":"15.270910"},{"1":"2021","2":"Gabon","3":"15.022300"},{"1":"2021","2":"Mongolia","3":"14.836730"},{"1":"2021","2":"Somalia","3":"14.744090"},{"1":"2021","2":"China","3":"14.505120"},{"1":"2021","2":"Macao","3":"14.505120"},{"1":"2021","2":"Korea","3":"14.481250"},{"1":"2021","2":"Eritrea","3":"14.358130"},{"1":"2021","2":"Ethiopia","3":"14.358130"},{"1":"2021","2":"Sudan","3":"14.281640"},{"1":"2021","2":"Bhutan","3":"14.184000"},{"1":"2020","2":"North Korea","3":"14.112850"},{"1":"2021","2":"Liberia","3":"14.011740"},{"1":"2021","2":"Tajikistan","3":"14.004820"},{"1":"2021","2":"Singapore","3":"13.900120"},{"1":"2021","2":"Myanmar","3":"13.833160"},{"1":"2021","2":"Nigeria","3":"13.784810"},{"1":"2021","2":"Niger","3":"13.774560"},{"1":"2021","2":"Romania","3":"13.672130"},{"1":"2021","2":"Russian Federation","3":"13.670900"},{"1":"2021","2":"Libya","3":"13.529750"},{"1":"2021","2":"Japan","3":"13.378050"},{"1":"2021","2":"Bulgaria","3":"13.200160"},{"1":"2021","2":"Guinea","3":"13.182330"},{"1":"2021","2":"Argentina","3":"13.180250"},{"1":"2021","2":"Kyrgyzstan","3":"13.124270"},{"1":"2021","2":"Canada","3":"13.057890"},{"1":"2021","2":"Kazakhstan","3":"12.997360"},{"1":"2021","2":"Timor-Leste","3":"12.634010"},{"1":"2021","2":"Mali","3":"12.629370"},{"1":"2021","2":"Nepal","3":"12.570650"},{"1":"2021","2":"Bangladesh","3":"12.561270"},{"1":"2021","2":"Pakistan","3":"12.525410"},{"1":"2021","2":"Tunisia","3":"12.450550"},{"1":"2021","2":"Mauritania","3":"12.059080"},{"1":"2020","2":"Cuba","3":"11.863260"},{"1":"2021","2":"Afghanistan","3":"11.669610"},{"1":"2021","2":"Malaysia","3":"11.641520"},{"1":"2021","2":"Ecuador","3":"11.562460"},{"1":"2021","2":"Sao Tome and Principe","3":"11.253070"},{"1":"2021","2":"Maldives","3":"11.063860"},{"1":"2021","2":"Uruguay","3":"10.960740"},{"1":"2021","2":"Armenia","3":"10.957560"},{"1":"2021","2":"Montenegro","3":"10.890540"},{"1":"2021","2":"Australia","3":"10.393100"},{"1":"2021","2":"Lithuania","3":"10.126340"},{"1":"2021","2":"Algeria","3":"10.012040"},{"1":"2021","2":"Brunei Darussalam","3":"9.823530"},{"1":"2021","2":"Germany","3":"9.760151"},{"1":"2021","2":"Poland","3":"9.694258"},{"1":"2021","2":"Serbia","3":"9.652961"},{"1":"2021","2":"Latvia","3":"9.637069"},{"1":"2021","2":"Azerbaijan","3":"9.630005"},{"1":"2021","2":"Croatia","3":"9.613139"},{"1":"2021","2":"Estonia","3":"9.522069"},{"1":"2021","2":"Cyprus","3":"9.494887"},{"1":"2021","2":"Moldova","3":"9.451350"},{"1":"2021","2":"Bosnia and Herzegovina","3":"9.321850"},{"1":"2021","2":"Albania","3":"8.989956"},{"1":"2020","2":"Kosovo","3":"8.973072"},{"1":"2021","2":"New Zealand","3":"8.832035"},{"1":"2021","2":"Portugal","3":"8.785279"},{"1":"2021","2":"United Kingdom","3":"8.766573"},{"1":"2021","2":"Ireland","3":"8.603584"},{"1":"2021","2":"Taiwan","3":"8.426919"},{"1":"2021","2":"Luxembourg","3":"8.303045"},{"1":"2021","2":"Spain","3":"8.161876"},{"1":"2021","2":"Belgium","3":"8.060792"},{"1":"2021","2":"Malta","3":"7.931879"},{"1":"2021","2":"Denmark","3":"7.918193"},{"1":"2021","2":"Finland","3":"7.900719"},{"1":"2021","2":"Italy","3":"7.778762"},{"1":"2021","2":"Greece","3":"7.759043"},{"1":"2021","2":"Hungary","3":"7.691266"},{"1":"2021","2":"Austria","3":"7.679657"},{"1":"2021","2":"Ukraine","3":"7.419922"},{"1":"2021","2":"Belarus","3":"7.417274"},{"1":"2021","2":"Switzerland","3":"7.176620"},{"1":"2021","2":"France","3":"7.091090"},{"1":"2021","2":"North Macedonia","3":"6.978232"},{"1":"2021","2":"Netherlands","3":"6.539901"},{"1":"2021","2":"Sweden","3":"6.471685"},{"1":"2021","2":"Slovenia","3":"6.411677"},{"1":"2021","2":"Norway","3":"5.956634"},{"1":"2021","2":"Iceland","3":"5.820321"},{"1":"2021","2":"Czech Republic","3":"5.607577"},{"1":"2021","2":"Slovakia","3":"5.393878"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f3 %>% 
  mutate(`Top 10 Bottom 50 Ratio` = cut(T10B50,breaks = c(5, 12, 13, 16, 19,140), 
                                        include.lowest = FALSE)) 
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Country"],"name":[2],"type":["chr"],"align":["left"]},{"label":["T10B50"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Top 10 Bottom 50 Ratio"],"name":[4],"type":["fct"],"align":["left"]}],"data":[{"1":"2021","2":"United Arab Emirates","3":"19.204010","4":"(19,140]"},{"1":"2021","2":"Afghanistan","3":"11.669610","4":"(5,12]"},{"1":"2021","2":"Albania","3":"8.989956","4":"(5,12]"},{"1":"2021","2":"Armenia","3":"10.957560","4":"(5,12]"},{"1":"2021","2":"Angola","3":"32.092700","4":"(19,140]"},{"1":"2021","2":"Argentina","3":"13.180250","4":"(13,16]"},{"1":"2021","2":"Austria","3":"7.679657","4":"(5,12]"},{"1":"2021","2":"Australia","3":"10.393100","4":"(5,12]"},{"1":"2021","2":"Azerbaijan","3":"9.630005","4":"(5,12]"},{"1":"2021","2":"Bosnia and Herzegovina","3":"9.321850","4":"(5,12]"},{"1":"2021","2":"Bangladesh","3":"12.561270","4":"(12,13]"},{"1":"2021","2":"Belgium","3":"8.060792","4":"(5,12]"},{"1":"2021","2":"Burkina Faso","3":"15.711230","4":"(13,16]"},{"1":"2021","2":"Bulgaria","3":"13.200160","4":"(13,16]"},{"1":"2021","2":"Bahrain","3":"28.280580","4":"(19,140]"},{"1":"2021","2":"Burundi","3":"17.261540","4":"(16,19]"},{"1":"2021","2":"Benin","3":"23.977820","4":"(19,140]"},{"1":"2021","2":"Brunei Darussalam","3":"9.823530","4":"(5,12]"},{"1":"2021","2":"Bolivia","3":"19.253270","4":"(19,140]"},{"1":"2021","2":"Brazil","3":"29.074700","4":"(19,140]"},{"1":"2021","2":"Bahamas","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"Bhutan","3":"14.184000","4":"(13,16]"},{"1":"2021","2":"Botswana","3":"36.492850","4":"(19,140]"},{"1":"2021","2":"Belarus","3":"7.417274","4":"(5,12]"},{"1":"2021","2":"Belize","3":"19.253270","4":"(19,140]"},{"1":"2021","2":"Canada","3":"13.057890","4":"(13,16]"},{"1":"2021","2":"DR Congo","3":"19.317310","4":"(19,140]"},{"1":"2021","2":"Central African Republic","3":"42.524850","4":"(19,140]"},{"1":"2021","2":"Congo","3":"28.200510","4":"(19,140]"},{"1":"2021","2":"Switzerland","3":"7.176620","4":"(5,12]"},{"1":"2021","2":"Cote d'Ivoire","3":"23.599090","4":"(19,140]"},{"1":"2021","2":"Chile","3":"28.942710","4":"(19,140]"},{"1":"2021","2":"Cameroon","3":"24.472310","4":"(19,140]"},{"1":"2021","2":"China","3":"14.505120","4":"(13,16]"},{"1":"2021","2":"Colombia","3":"24.207660","4":"(19,140]"},{"1":"2021","2":"Costa Rica","3":"23.365570","4":"(19,140]"},{"1":"2020","2":"Cuba","3":"11.863260","4":"(5,12]"},{"1":"2021","2":"Cabo Verde","3":"19.826510","4":"(19,140]"},{"1":"2021","2":"Cyprus","3":"9.494887","4":"(5,12]"},{"1":"2021","2":"Czech Republic","3":"5.607577","4":"(5,12]"},{"1":"2021","2":"Germany","3":"9.760151","4":"(5,12]"},{"1":"2021","2":"Djibouti","3":"18.932130","4":"(16,19]"},{"1":"2021","2":"Denmark","3":"7.918193","4":"(5,12]"},{"1":"2021","2":"Dominican Republic","3":"19.253270","4":"(19,140]"},{"1":"2021","2":"Algeria","3":"10.012040","4":"(5,12]"},{"1":"2021","2":"Ecuador","3":"11.562460","4":"(5,12]"},{"1":"2021","2":"Estonia","3":"9.522069","4":"(5,12]"},{"1":"2021","2":"Egypt","3":"16.815820","4":"(16,19]"},{"1":"2021","2":"Eritrea","3":"14.358130","4":"(13,16]"},{"1":"2021","2":"Spain","3":"8.161876","4":"(5,12]"},{"1":"2021","2":"Ethiopia","3":"14.358130","4":"(13,16]"},{"1":"2021","2":"Finland","3":"7.900719","4":"(5,12]"},{"1":"2021","2":"France","3":"7.091090","4":"(5,12]"},{"1":"2021","2":"Gabon","3":"15.022300","4":"(13,16]"},{"1":"2021","2":"United Kingdom","3":"8.766573","4":"(5,12]"},{"1":"2021","2":"Georgia","3":"17.632930","4":"(16,19]"},{"1":"2021","2":"Ghana","3":"20.029220","4":"(19,140]"},{"1":"2021","2":"Gambia","3":"15.270910","4":"(13,16]"},{"1":"2021","2":"Guinea","3":"13.182330","4":"(13,16]"},{"1":"2021","2":"Equatorial Guinea","3":"22.545290","4":"(19,140]"},{"1":"2021","2":"Greece","3":"7.759043","4":"(5,12]"},{"1":"2021","2":"Guatemala","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"Guinea-Bissau","3":"31.343620","4":"(19,140]"},{"1":"2021","2":"Guyana","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"Hong Kong","3":"17.724050","4":"(16,19]"},{"1":"2021","2":"Honduras","3":"19.253270","4":"(19,140]"},{"1":"2021","2":"Croatia","3":"9.613139","4":"(5,12]"},{"1":"2021","2":"Haiti","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"Hungary","3":"7.691266","4":"(5,12]"},{"1":"2021","2":"Indonesia","3":"19.366180","4":"(19,140]"},{"1":"2021","2":"Ireland","3":"8.603584","4":"(5,12]"},{"1":"2021","2":"Israel","3":"18.668620","4":"(16,19]"},{"1":"2021","2":"India","3":"21.757670","4":"(19,140]"},{"1":"2021","2":"Iraq","3":"20.355850","4":"(19,140]"},{"1":"2021","2":"Iran","3":"19.828190","4":"(19,140]"},{"1":"2021","2":"Iceland","3":"5.820321","4":"(5,12]"},{"1":"2021","2":"Italy","3":"7.778762","4":"(5,12]"},{"1":"2021","2":"Jamaica","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"Jordan","3":"17.331080","4":"(16,19]"},{"1":"2021","2":"Japan","3":"13.378050","4":"(13,16]"},{"1":"2021","2":"Kenya","3":"18.716540","4":"(16,19]"},{"1":"2021","2":"Kyrgyzstan","3":"13.124270","4":"(13,16]"},{"1":"2021","2":"Cambodia","3":"16.773860","4":"(16,19]"},{"1":"2021","2":"Comoros","3":"22.056120","4":"(19,140]"},{"1":"2020","2":"North Korea","3":"14.112850","4":"(13,16]"},{"1":"2021","2":"Korea","3":"14.481250","4":"(13,16]"},{"1":"2020","2":"Kosovo","3":"8.973072","4":"(5,12]"},{"1":"2021","2":"Kuwait","3":"22.994100","4":"(19,140]"},{"1":"2021","2":"Kazakhstan","3":"12.997360","4":"(12,13]"},{"1":"2021","2":"Lao PDR","3":"19.256650","4":"(19,140]"},{"1":"2020","2":"Lebanon","3":"26.646230","4":"(19,140]"},{"1":"2021","2":"Sri Lanka","3":"17.520910","4":"(16,19]"},{"1":"2021","2":"Liberia","3":"14.011740","4":"(13,16]"},{"1":"2021","2":"Lesotho","3":"21.941270","4":"(19,140]"},{"1":"2021","2":"Lithuania","3":"10.126340","4":"(5,12]"},{"1":"2021","2":"Luxembourg","3":"8.303045","4":"(5,12]"},{"1":"2021","2":"Latvia","3":"9.637069","4":"(5,12]"},{"1":"2021","2":"Libya","3":"13.529750","4":"(13,16]"},{"1":"2021","2":"Morocco","3":"18.229160","4":"(16,19]"},{"1":"2021","2":"Moldova","3":"9.451350","4":"(5,12]"},{"1":"2021","2":"Montenegro","3":"10.890540","4":"(5,12]"},{"1":"2021","2":"Madagascar","3":"20.333440","4":"(19,140]"},{"1":"2021","2":"North Macedonia","3":"6.978232","4":"(5,12]"},{"1":"2021","2":"Mali","3":"12.629370","4":"(12,13]"},{"1":"2021","2":"Myanmar","3":"13.833160","4":"(13,16]"},{"1":"2021","2":"Mongolia","3":"14.836730","4":"(13,16]"},{"1":"2021","2":"Macao","3":"14.505120","4":"(13,16]"},{"1":"2021","2":"Mauritania","3":"12.059080","4":"(12,13]"},{"1":"2021","2":"Malta","3":"7.931879","4":"(5,12]"},{"1":"2021","2":"Mauritius","3":"16.007260","4":"(16,19]"},{"1":"2021","2":"Maldives","3":"11.063860","4":"(5,12]"},{"1":"2021","2":"Malawi","3":"23.939230","4":"(19,140]"},{"1":"2021","2":"Mexico","3":"31.262120","4":"(19,140]"},{"1":"2021","2":"Malaysia","3":"11.641520","4":"(5,12]"},{"1":"2021","2":"Mozambique","3":"38.944060","4":"(19,140]"},{"1":"2021","2":"Namibia","3":"49.030030","4":"(19,140]"},{"1":"2021","2":"Niger","3":"13.774560","4":"(13,16]"},{"1":"2021","2":"Nigeria","3":"13.784810","4":"(13,16]"},{"1":"2021","2":"Nicaragua","3":"19.253270","4":"(19,140]"},{"1":"2021","2":"Netherlands","3":"6.539901","4":"(5,12]"},{"1":"2021","2":"Norway","3":"5.956634","4":"(5,12]"},{"1":"2021","2":"Nepal","3":"12.570650","4":"(12,13]"},{"1":"2021","2":"New Zealand","3":"8.832035","4":"(5,12]"},{"1":"2021","2":"Oman","3":"139.590900","4":"(19,140]"},{"1":"2021","2":"Panama","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"Peru","3":"22.248380","4":"(19,140]"},{"1":"2021","2":"Papua New Guinea","3":"18.281150","4":"(16,19]"},{"1":"2021","2":"Philippines","3":"16.094840","4":"(16,19]"},{"1":"2021","2":"Pakistan","3":"12.525410","4":"(12,13]"},{"1":"2021","2":"Poland","3":"9.694258","4":"(5,12]"},{"1":"2021","2":"Palestine","3":"21.060580","4":"(19,140]"},{"1":"2021","2":"Portugal","3":"8.785279","4":"(5,12]"},{"1":"2021","2":"Paraguay","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"Qatar","3":"30.238270","4":"(19,140]"},{"1":"2021","2":"Romania","3":"13.672130","4":"(13,16]"},{"1":"2021","2":"Serbia","3":"9.652961","4":"(5,12]"},{"1":"2021","2":"Russian Federation","3":"13.670900","4":"(13,16]"},{"1":"2021","2":"Rwanda","3":"22.775260","4":"(19,140]"},{"1":"2021","2":"Saudi Arabia","3":"24.654720","4":"(19,140]"},{"1":"2021","2":"Seychelles","3":"21.471810","4":"(19,140]"},{"1":"2021","2":"Sudan","3":"14.281640","4":"(13,16]"},{"1":"2021","2":"Sweden","3":"6.471685","4":"(5,12]"},{"1":"2021","2":"Singapore","3":"13.900120","4":"(13,16]"},{"1":"2021","2":"Slovenia","3":"6.411677","4":"(5,12]"},{"1":"2021","2":"Slovakia","3":"5.393878","4":"(5,12]"},{"1":"2021","2":"Sierra Leone","3":"15.675510","4":"(13,16]"},{"1":"2021","2":"Senegal","3":"17.830500","4":"(16,19]"},{"1":"2021","2":"Somalia","3":"14.744090","4":"(13,16]"},{"1":"2021","2":"Suriname","3":"19.253280","4":"(19,140]"},{"1":"2021","2":"South Sudan","3":"20.991060","4":"(19,140]"},{"1":"2021","2":"Sao Tome and Principe","3":"11.253070","4":"(5,12]"},{"1":"2021","2":"El Salvador","3":"17.586230","4":"(16,19]"},{"1":"2020","2":"Syrian Arab Republic","3":"26.545660","4":"(19,140]"},{"1":"2021","2":"Swaziland","3":"38.112220","4":"(19,140]"},{"1":"2021","2":"Chad","3":"20.046880","4":"(19,140]"},{"1":"2021","2":"Togo","3":"19.635430","4":"(19,140]"},{"1":"2021","2":"Thailand","3":"17.565470","4":"(16,19]"},{"1":"2021","2":"Tajikistan","3":"14.004820","4":"(13,16]"},{"1":"2021","2":"Timor-Leste","3":"12.634010","4":"(12,13]"},{"1":"2021","2":"Turkmenistan","3":"20.770220","4":"(19,140]"},{"1":"2021","2":"Tunisia","3":"12.450550","4":"(12,13]"},{"1":"2021","2":"Turkey","3":"22.779770","4":"(19,140]"},{"1":"2021","2":"Trinidad and Tobago","3":"19.253270","4":"(19,140]"},{"1":"2021","2":"Taiwan","3":"8.426919","4":"(5,12]"},{"1":"2021","2":"Tanzania","3":"19.837950","4":"(19,140]"},{"1":"2021","2":"Ukraine","3":"7.419922","4":"(5,12]"},{"1":"2021","2":"Uganda","3":"21.469920","4":"(19,140]"},{"1":"2021","2":"USA","3":"17.077610","4":"(16,19]"},{"1":"2021","2":"Uruguay","3":"10.960740","4":"(5,12]"},{"1":"2021","2":"Uzbekistan","3":"15.865990","4":"(13,16]"},{"1":"2020","2":"Venezuela","3":"19.253270","4":"(19,140]"},{"1":"2021","2":"Viet Nam","3":"15.394770","4":"(13,16]"},{"1":"2021","2":"Yemen","3":"31.963060","4":"(19,140]"},{"1":"2021","2":"South Africa","3":"63.098640","4":"(19,140]"},{"1":"2021","2":"Zambia","3":"44.420860","4":"(19,140]"},{"1":"2021","2":"Zimbabwe","3":"31.924770","4":"(19,140]"},{"1":"2021","2":"Zanzibar","3":"19.837950","4":"(19,140]"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
world_map <- map_data("world")
df_f3 %>% mutate(`Top 10 Bottom 50 Ratio` = cut(T10B50,breaks = c(5, 12, 13, 16, 19,140), 
                                        include.lowest = FALSE)) %>%
  ggplot(aes(map_id = Country)) + 
  geom_map(aes(fill = `Top 10 Bottom 50 Ratio`), map = world_map) + 
  expand_limits(x = world_map$long, y = world_map$lat)
```

![](eda4_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

---


```r
world_map_wir <- world_map
world_map_wir$region[
  world_map_wir$region=="Democratic Republic of the Congo"]<-"DR Congo"
world_map_wir$region[world_map_wir$region=="Republic of Congo"]<-"Congo"
world_map_wir$region[world_map_wir$region=="Ivory Coast"]<-"Cote dIvoire"
world_map_wir$region[world_map_wir$region=="Vietnam"]<-"Viet Nam"
world_map_wir$region[world_map_wir$region=="Russia"]<-"Russian Federation"
world_map_wir$region[world_map_wir$region=="South Korea"]<-"Korea"
world_map_wir$region[world_map_wir$region=="UK"]<-"United Kingdom"
world_map_wir$region[world_map_wir$region=="Brunei"]<-"Brunei Darussalam"
world_map_wir$region[world_map_wir$region=="Laos"]<-"Lao PDR"
world_map_wir$region[world_map_wir$region=="Cote dIvoire"]<-"Cote d'Ivoire"
world_map_wir$region[world_map_wir$region=="Cape Verde"]<- "Cabo Verde"
world_map_wir$region[world_map_wir$region=="Syria"]<- "Syrian Arab Republic"
world_map_wir$region[world_map_wir$region=="Trinidad"]<- "Trinidad and Tobago"
world_map_wir$region[world_map_wir$region=="Tobago"]<- "Trinidad and Tobago"
```
  
---


```r
df_f3 %>% mutate(`Top 10 Bottom 50 Ratio` = 
    cut(T10B50, breaks = c(5, 12, 13, 16, 19,140), include.lowest = FALSE)) %>%
  ggplot(aes(map_id = Country)) + 
  geom_map(aes(fill = `Top 10 Bottom 50 Ratio`), 
    map = world_map_wir) + 
    expand_limits(x = world_map_wir$long, y = world_map_wir$lat)
```

![](eda4_files/figure-html/unnamed-chunk-23-1.png)<!-- -->



---


```r
df_f3 %>% mutate(`Top 10 Bottom 50 Ratio` = 
    cut(T10B50,breaks = c(5, 12, 13, 16, 19,140), include.lowest = FALSE)) %>%
  ggplot(aes(map_id = Country)) + geom_map(aes(fill = `Top 10 Bottom 50 Ratio`), 
    map = world_map_wir) + expand_limits(x = world_map_wir$long, y = world_map_wir$lat) + 
  coord_map("orthographic", orientation = c(25, 60, 0))
```

![](eda4_files/figure-html/unnamed-chunk-24-1.png)<!-- -->

---


```r
df_f3 %>% mutate(`Top 10 Bottom 50 Ratio` = 
  cut(T10B50,breaks = c(5, 12, 13, 16, 19,140), include.lowest = FALSE)) %>%
  ggplot(aes(map_id = Country)) + geom_map(aes(fill = `Top 10 Bottom 50 Ratio`), 
    map = world_map_wir) + expand_limits(x = world_map_wir$long, y = world_map_wir$lat) + 
  coord_map("orthographic", orientation = c(15, -80, 0))
```

![](eda4_files/figure-html/unnamed-chunk-25-1.png)<!-- -->

---



```r
df_f3 %>% mutate(`Top 10 Bottom 50 Ratio` = 
  cut(T10B50,breaks = c(5, 12, 13, 16, 19,140), include.lowest = FALSE)) %>%
  ggplot(aes(map_id = Country)) + geom_map(aes(fill = `Top 10 Bottom 50 Ratio`), 
    map = world_map_wir) + 
  expand_limits(x = world_map_wir$long, y = world_map_wir$lat)
```

![](eda4_files/figure-html/unnamed-chunk-26-1.png)<!-- -->

---


```r
df_f3 %>% 
  mutate(`Top 10 Bottom 50 Ratio` = 
        cut(T10B50,breaks = c(5, 12, 13, 16, 19,140), include.lowest = FALSE)) %>%
  ggplot(aes(map_id = Country)) + 
  geom_map(aes(fill = `Top 10 Bottom 50 Ratio`), map = world_map_wir) + 
  expand_limits(x = world_map_wir$long, y = world_map_wir$lat)  + 
  labs(title = "Figure 3. Top 10/Bottom 50 income gaps across the world, 2021",
       x = "", y = "", fill = "Top 10/Bottom 50 ratio") +
  theme(legend.position="bottom", 
        axis.text.x=element_blank(), axis.ticks.x=element_blank(),
        axis.text.y=element_blank(), axis.ticks.y=element_blank()) + 
  scale_fill_brewer(palette='YlOrRd')
```

---

![](eda4_files/figure-html/unnamed-chunk-28-1.png)<!-- -->

---


```r
df_f3 %>% anti_join(world_map_wir, by = c("Country" = "region"))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Country"],"name":[2],"type":["chr"],"align":["left"]},{"label":["T10B50"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"2021","2":"Hong Kong","3":"17.72405"},{"1":"2021","2":"Macao","3":"14.50512"},{"1":"2021","2":"Zanzibar","3":"19.83795"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

**Filtering joins**

* `anti_join(x,y, ...)`: return all rows from x without a match in y.
* `semi_join(x,y, ...)`: return all rows from x with a match in y.

Check `dplyr` cheat sheet, and Posit Primers Tidy Data.

---

### Remaining Charts

* F5: Global income inequality: T10/B50 ratio, 1820-2020 - fit curve
* F9: Average annual wealth growth rate, 1995-2021 - fit curve + alpha
* F7: Global income inequality, 1820-2020 - pivot + fit curve
* F10: The share of wealth owned by the global 0.1% and billionaires, 2021 - pivot + fit curve


* F6: Global income inequality: Between vs. Within country inequality (Theil index), 1820-2020 - pivot + area

* F11: Top 1% vs bottom 50% wealth shares in Western Europe and the US, 1910-2020 - pivot name_sep + fit curve
* F8: The rise of private versus the decline of public wealth in rich countries, 1970-2020 - rename + pivot + pivot + fit curve

* F15: Per capita emissions acriss the world, 2019 - add row names + dodge


---

### F5: Global income inequality: T10/B50 ratio, 1820-2020


```r
(df_f5 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F5"))
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["y"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["t10b50"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"1820","2":"18.53675"},{"1":"1850","2":"22.48805"},{"1":"1880","2":"32.67190"},{"1":"1900","2":"41.11015"},{"1":"1910","2":"41.23964"},{"1":"1920","2":"39.54550"},{"1":"1930","2":"39.04569"},{"1":"1940","2":"44.37845"},{"1":"1950","2":"40.31005"},{"1":"1960","2":"38.40167"},{"1":"1970","2":"45.88190"},{"1":"1980","2":"53.31809"},{"1":"1985","2":"48.95933"},{"1":"1990","2":"50.61138"},{"1":"1995","2":"49.94222"},{"1":"1997","2":"49.00875"},{"1":"2000","2":"50.42301"},{"1":"2002","2":"49.83546"},{"1":"2005","2":"49.28372"},{"1":"2007","2":"47.41053"},{"1":"2010","2":"43.23287"},{"1":"2015","2":"40.26652"},{"1":"2017","2":"38.81437"},{"1":"2020","2":"38.44040"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f5 %>% ggplot(aes(x = y, y = t10b50)) + geom_line() + geom_smooth(span=0.25, se=FALSE)
```

```
## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'
```

![](eda4_files/figure-html/unnamed-chunk-30-1.png)<!-- -->

---

### F9: Average annual wealth growth rate, 1995-2021 - fit curve + alpha


```r
df_f9 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F9"); df_f9
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["p"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Wealth growth 1995-2021"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"0.000","2":"0.03102311"},{"1":"1.000","2":"0.03102311"},{"1":"2.000","2":"0.03102311"},{"1":"3.000","2":"0.03102311"},{"1":"4.000","2":"0.03102311"},{"1":"5.000","2":"0.03102311"},{"1":"6.000","2":"0.03118334"},{"1":"7.000","2":"0.03165223"},{"1":"8.000","2":"0.03223753"},{"1":"9.000","2":"0.03281050"},{"1":"10.000","2":"0.03331926"},{"1":"11.000","2":"0.03380264"},{"1":"12.000","2":"0.03425127"},{"1":"13.000","2":"0.03465587"},{"1":"14.000","2":"0.03505633"},{"1":"15.000","2":"0.03533275"},{"1":"16.000","2":"0.03531424"},{"1":"17.000","2":"0.03519475"},{"1":"18.000","2":"0.03511410"},{"1":"19.000","2":"0.03511760"},{"1":"20.000","2":"0.03515608"},{"1":"21.000","2":"0.03524348"},{"1":"22.000","2":"0.03538625"},{"1":"23.000","2":"0.03554292"},{"1":"24.000","2":"0.03566767"},{"1":"25.000","2":"0.03577601"},{"1":"26.000","2":"0.03587980"},{"1":"27.000","2":"0.03597065"},{"1":"28.000","2":"0.03606234"},{"1":"29.000","2":"0.03616425"},{"1":"30.000","2":"0.03628138"},{"1":"31.000","2":"0.03641255"},{"1":"32.000","2":"0.03653315"},{"1":"33.000","2":"0.03663325"},{"1":"34.000","2":"0.03672126"},{"1":"35.000","2":"0.03678927"},{"1":"36.000","2":"0.03683394"},{"1":"37.000","2":"0.03687065"},{"1":"38.000","2":"0.03692934"},{"1":"39.000","2":"0.03700165"},{"1":"40.000","2":"0.03708560"},{"1":"41.000","2":"0.03720308"},{"1":"42.000","2":"0.03737086"},{"1":"43.000","2":"0.03757202"},{"1":"44.000","2":"0.03779476"},{"1":"45.000","2":"0.03802628"},{"1":"46.000","2":"0.03824022"},{"1":"47.000","2":"0.03839709"},{"1":"48.000","2":"0.03851535"},{"1":"49.000","2":"0.03863759"},{"1":"50.000","2":"0.03881265"},{"1":"51.000","2":"0.03904984"},{"1":"52.000","2":"0.03936489"},{"1":"53.000","2":"0.03974150"},{"1":"54.000","2":"0.04014270"},{"1":"55.000","2":"0.04052881"},{"1":"56.000","2":"0.04091159"},{"1":"57.000","2":"0.04128646"},{"1":"58.000","2":"0.04163751"},{"1":"59.000","2":"0.04192803"},{"1":"60.000","2":"0.04215331"},{"1":"61.000","2":"0.04230473"},{"1":"62.000","2":"0.04239625"},{"1":"63.000","2":"0.04246272"},{"1":"64.000","2":"0.04255537"},{"1":"65.000","2":"0.04268008"},{"1":"66.000","2":"0.04281863"},{"1":"67.000","2":"0.04294864"},{"1":"68.000","2":"0.04304929"},{"1":"69.000","2":"0.04311060"},{"1":"70.000","2":"0.04313104"},{"1":"71.000","2":"0.04312409"},{"1":"72.000","2":"0.04308372"},{"1":"73.000","2":"0.04300554"},{"1":"74.000","2":"0.04286919"},{"1":"75.000","2":"0.04267076"},{"1":"76.000","2":"0.04239105"},{"1":"77.000","2":"0.04203834"},{"1":"78.000","2":"0.04160896"},{"1":"79.000","2":"0.04108399"},{"1":"80.000","2":"0.04043937"},{"1":"81.000","2":"0.03968068"},{"1":"82.000","2":"0.03879190"},{"1":"83.000","2":"0.03777532"},{"1":"84.000","2":"0.03667277"},{"1":"85.000","2":"0.03552421"},{"1":"86.000","2":"0.03435350"},{"1":"87.000","2":"0.03320156"},{"1":"88.000","2":"0.03213683"},{"1":"89.000","2":"0.03117302"},{"1":"90.000","2":"0.03033051"},{"1":"91.000","2":"0.02968016"},{"1":"92.000","2":"0.02921267"},{"1":"93.000","2":"0.02886223"},{"1":"94.000","2":"0.02858335"},{"1":"95.000","2":"0.02836451"},{"1":"96.000","2":"0.02812004"},{"1":"97.000","2":"0.02782299"},{"1":"98.000","2":"0.02747279"},{"1":"99.000","2":"0.02713943"},{"1":"99.900","2":"0.02674679"},{"1":"99.900","2":"0.02636675"},{"1":"99.900","2":"0.02604863"},{"1":"99.900","2":"0.02584039"},{"1":"99.900","2":"0.02571661"},{"1":"99.900","2":"0.02577340"},{"1":"99.900","2":"0.02592032"},{"1":"99.900","2":"0.02617832"},{"1":"99.900","2":"0.02653326"},{"1":"99.990","2":"0.02701378"},{"1":"99.990","2":"0.02756237"},{"1":"99.990","2":"0.02824531"},{"1":"99.990","2":"0.02908172"},{"1":"99.990","2":"0.03004243"},{"1":"99.990","2":"0.03103916"},{"1":"99.990","2":"0.03210992"},{"1":"99.990","2":"0.03332751"},{"1":"99.990","2":"0.03457246"},{"1":"99.999","2":"0.03581344"},{"1":"99.999","2":"0.03711118"},{"1":"99.999","2":"0.03837790"},{"1":"99.999","2":"0.03943777"},{"1":"99.999","2":"0.04034064"},{"1":"99.999","2":"0.04408112"},{"1":"99.999","2":"0.05028756"},{"1":"99.999","2":"0.05175231"},{"1":"99.999","2":"0.09287249"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f9 %>% 
  ggplot(aes(x = p, y = `Wealth growth 1995-2021`)) + geom_smooth(span = 0.30, se = FALSE)
```

```
## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'
```

![](eda4_files/figure-html/unnamed-chunk-31-1.png)<!-- -->

---

### F7: Global income inequality, 1820-2020 - pivot + fit curve


```r
df_f7 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F7"); df_f7
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["y"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Bottom 50%"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["Middle 40%"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Top 10%"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"1820","2":"0.13564739","3":"0.3614602","4":"0.5028924"},{"1":"1850","2":"0.11820287","3":"0.3501668","4":"0.5316303"},{"1":"1880","2":"0.08696501","3":"0.3447726","4":"0.5682624"},{"1":"1900","2":"0.07241563","3":"0.3321809","4":"0.5954035"},{"1":"1910","2":"0.07285886","3":"0.3262064","4":"0.6009347"},{"1":"1920","2":"0.07546183","3":"0.3277030","4":"0.5968352"},{"1":"1930","2":"0.07139124","3":"0.3711047","4":"0.5575041"},{"1":"1940","2":"0.06286313","3":"0.3791833","4":"0.5579536"},{"1":"1950","2":"0.06873786","3":"0.3770968","4":"0.5541653"},{"1":"1960","2":"0.07008597","3":"0.3916303","4":"0.5382837"},{"1":"1970","2":"0.05856160","3":"0.4040549","4":"0.5373835"},{"1":"1980","2":"0.05282140","3":"0.3839114","4":"0.5632672"},{"1":"1985","2":"0.05795137","3":"0.3745966","4":"0.5674520"},{"1":"1990","2":"0.05760923","3":"0.3592542","4":"0.5831366"},{"1":"1995","2":"0.06004609","3":"0.3401870","4":"0.5997670"},{"1":"1997","2":"0.06139626","3":"0.3368129","4":"0.6017908"},{"1":"2000","2":"0.06041728","3":"0.3302984","4":"0.6092843"},{"1":"2002","2":"0.06050558","3":"0.3364298","4":"0.6030647"},{"1":"2005","2":"0.06057866","3":"0.3423130","4":"0.5971084"},{"1":"2007","2":"0.06196488","3":"0.3504775","4":"0.5875576"},{"1":"2010","2":"0.06564309","3":"0.3667691","4":"0.5675879"},{"1":"2015","2":"0.06888296","3":"0.3763816","4":"0.5547354"},{"1":"2017","2":"0.07074528","3":"0.3800681","4":"0.5491866"},{"1":"2020","2":"0.07133102","3":"0.3802704","4":"0.5483986"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f7 %>% 
  pivot_longer(cols = 2:4, names_to = "type", values_to = "value") %>%
  ggplot(aes(x = y, y = value, color = type)) +
  stat_smooth(formula = y~x, method = "loess", span = 0.25, se = FALSE)
```

![](eda4_files/figure-html/unnamed-chunk-32-1.png)<!-- -->

---

### F10: The share of wealth owned by the global 0.1% and billionaires, 2021 - pivot + fit curve


```r
df_f10 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F10"); df_f10
```

```
## New names:
## • `` -> `...4`
## • `` -> `...5`
## • `` -> `...6`
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["bn_hhweal"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["top0.1_hhweal"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["...4"],"name":[4],"type":["lgl"],"align":["right"]},{"label":["...5"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["...6"],"name":[6],"type":["dbl"],"align":["right"]}],"data":[{"1":"1995","2":"0.010817260","3":"0.0729","4":"NA","5":"NA","6":"NA"},{"1":"1996","2":"0.011425801","3":"0.0744","4":"NA","5":"NA","6":"NA"},{"1":"1997","2":"0.010075037","3":"0.0768","4":"NA","5":"NA","6":"NA"},{"1":"1998","2":"0.009947428","3":"0.0815","4":"NA","5":"NA","6":"NA"},{"1":"1999","2":"0.011193804","3":"0.0855","4":"NA","5":"NA","6":"NA"},{"1":"2000","2":"0.011535854","3":"0.0862","4":"NA","5":"NA","6":"NA"},{"1":"2001","2":"0.013913389","3":"0.0846","4":"NA","5":"NA","6":"NA"},{"1":"2002","2":"0.011883716","3":"0.0800","4":"NA","5":"NA","6":"NA"},{"1":"2003","2":"0.010289773","3":"0.0800","4":"NA","5":"NA","6":"NA"},{"1":"2004","2":"0.012676390","3":"0.0828","4":"NA","5":"NA","6":"NA"},{"1":"2005","2":"0.013148768","3":"0.0835","4":"NA","5":"NA","6":"NA"},{"1":"2006","2":"0.013991648","3":"0.0873","4":"NA","5":"NA","6":"NA"},{"1":"2007","2":"0.016698431","3":"0.0991","4":"NA","5":"NA","6":"NA"},{"1":"2008","2":"0.021107348","3":"0.1004","4":"NA","5":"NA","6":"NA"},{"1":"2009","2":"0.011754374","3":"0.0795","4":"NA","5":"NA","6":"NA"},{"1":"2010","2":"0.016418075","3":"0.0884","4":"NA","5":"NA","6":"NA"},{"1":"2011","2":"0.019611511","3":"0.0969","4":"NA","5":"NA","6":"NA"},{"1":"2012","2":"0.018814459","3":"0.0950","4":"NA","5":"NA","6":"NA"},{"1":"2013","2":"0.020675618","3":"0.0971","4":"NA","5":"NA","6":"NA"},{"1":"2014","2":"0.022932300","3":"0.1012","4":"NA","5":"NA","6":"NA"},{"1":"2015","2":"0.023889290","3":"0.1067","4":"NA","5":"NA","6":"NA"},{"1":"2016","2":"0.021082999","3":"0.1036","4":"NA","5":"NA","6":"NA"},{"1":"2017","2":"0.023488445","3":"0.1033","4":"NA","5":"NA","6":"NA"},{"1":"2018","2":"0.026223848","3":"0.1053","4":"NA","5":"NA","6":"NA"},{"1":"2019","2":"0.023779836","3":"0.1032","4":"NA","5":"NA","6":"NA"},{"1":"2020","2":"0.022011383","3":"0.1026","4":"NA","5":"NA","6":"NA"},{"1":"2021","2":"0.033361219","3":"0.1111","4":"NA","5":"3.084073","6":"2.284499"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f10 %>% 
  select(year, "Global Billionaire Wealth" = bn_hhweal, "Top 0.01%" = top0.1_hhweal) %>%
  pivot_longer(!year, names_to = "group",".value", values_to = "value")
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["group"],"name":[2],"type":["chr"],"align":["left"]},{"label":["value"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"1995","2":"Global Billionaire Wealth","3":"0.010817260"},{"1":"1995","2":"Top 0.01%","3":"0.072900000"},{"1":"1996","2":"Global Billionaire Wealth","3":"0.011425801"},{"1":"1996","2":"Top 0.01%","3":"0.074400000"},{"1":"1997","2":"Global Billionaire Wealth","3":"0.010075037"},{"1":"1997","2":"Top 0.01%","3":"0.076800000"},{"1":"1998","2":"Global Billionaire Wealth","3":"0.009947428"},{"1":"1998","2":"Top 0.01%","3":"0.081500000"},{"1":"1999","2":"Global Billionaire Wealth","3":"0.011193804"},{"1":"1999","2":"Top 0.01%","3":"0.085500000"},{"1":"2000","2":"Global Billionaire Wealth","3":"0.011535854"},{"1":"2000","2":"Top 0.01%","3":"0.086200000"},{"1":"2001","2":"Global Billionaire Wealth","3":"0.013913389"},{"1":"2001","2":"Top 0.01%","3":"0.084600000"},{"1":"2002","2":"Global Billionaire Wealth","3":"0.011883716"},{"1":"2002","2":"Top 0.01%","3":"0.080000000"},{"1":"2003","2":"Global Billionaire Wealth","3":"0.010289773"},{"1":"2003","2":"Top 0.01%","3":"0.080000000"},{"1":"2004","2":"Global Billionaire Wealth","3":"0.012676390"},{"1":"2004","2":"Top 0.01%","3":"0.082800000"},{"1":"2005","2":"Global Billionaire Wealth","3":"0.013148768"},{"1":"2005","2":"Top 0.01%","3":"0.083500000"},{"1":"2006","2":"Global Billionaire Wealth","3":"0.013991648"},{"1":"2006","2":"Top 0.01%","3":"0.087300000"},{"1":"2007","2":"Global Billionaire Wealth","3":"0.016698431"},{"1":"2007","2":"Top 0.01%","3":"0.099100000"},{"1":"2008","2":"Global Billionaire Wealth","3":"0.021107348"},{"1":"2008","2":"Top 0.01%","3":"0.100400000"},{"1":"2009","2":"Global Billionaire Wealth","3":"0.011754374"},{"1":"2009","2":"Top 0.01%","3":"0.079500000"},{"1":"2010","2":"Global Billionaire Wealth","3":"0.016418075"},{"1":"2010","2":"Top 0.01%","3":"0.088400000"},{"1":"2011","2":"Global Billionaire Wealth","3":"0.019611511"},{"1":"2011","2":"Top 0.01%","3":"0.096900000"},{"1":"2012","2":"Global Billionaire Wealth","3":"0.018814459"},{"1":"2012","2":"Top 0.01%","3":"0.095000000"},{"1":"2013","2":"Global Billionaire Wealth","3":"0.020675618"},{"1":"2013","2":"Top 0.01%","3":"0.097100000"},{"1":"2014","2":"Global Billionaire Wealth","3":"0.022932300"},{"1":"2014","2":"Top 0.01%","3":"0.101200000"},{"1":"2015","2":"Global Billionaire Wealth","3":"0.023889290"},{"1":"2015","2":"Top 0.01%","3":"0.106700000"},{"1":"2016","2":"Global Billionaire Wealth","3":"0.021082999"},{"1":"2016","2":"Top 0.01%","3":"0.103600000"},{"1":"2017","2":"Global Billionaire Wealth","3":"0.023488445"},{"1":"2017","2":"Top 0.01%","3":"0.103300000"},{"1":"2018","2":"Global Billionaire Wealth","3":"0.026223848"},{"1":"2018","2":"Top 0.01%","3":"0.105300000"},{"1":"2019","2":"Global Billionaire Wealth","3":"0.023779836"},{"1":"2019","2":"Top 0.01%","3":"0.103200000"},{"1":"2020","2":"Global Billionaire Wealth","3":"0.022011383"},{"1":"2020","2":"Top 0.01%","3":"0.102600000"},{"1":"2021","2":"Global Billionaire Wealth","3":"0.033361219"},{"1":"2021","2":"Top 0.01%","3":"0.111100000"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f10 %>% 
  select(year, "Global Billionaire Wealth" = bn_hhweal, "Top 0.01%" = top0.1_hhweal) %>%
  pivot_longer(!year, names_to = "group",".value", values_to = "value") %>%
  ggplot() +
  stat_smooth(aes(x = year, y = value, color = group), formula = y~x, method = "loess", span = 0.25, se = FALSE)
```

![](eda4_files/figure-html/unnamed-chunk-34-1.png)<!-- -->

---

### F6: Global income inequality: Between vs. Within country inequality (Theil index), 1820-2020 - pivot + area


```r
df_f6 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F6"); df_f6
```

```
## New names:
## • `` -> `...1`
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["...1"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Between-country inequality"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["Within-country inequality"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"1820","2":"0.1202971","3":"0.8797029"},{"1":"1850","2":"0.1664352","3":"0.8335648"},{"1":"1880","2":"0.2410592","3":"0.7589408"},{"1":"1900","2":"0.2565747","3":"0.7434253"},{"1":"1920","2":"0.3203289","3":"0.6796711"},{"1":"1950","2":"0.4391636","3":"0.5608364"},{"1":"1980","2":"0.5686893","3":"0.4313107"},{"1":"2000","2":"0.4734622","3":"0.5265378"},{"1":"2020","2":"0.3200879","3":"0.6799121"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f6 %>% select(year = "...1", 2:3) %>%
  pivot_longer(cols = 2:3, names_to = "type", values_to = "value") %>%
  mutate(types = factor(type, 
      levels = c("Within-country inequality", "Between-country inequality"))) %>%
  ggplot(aes(x = year, y = value, fill = types)) +
  geom_area() +
  scale_y_continuous(labels = scales::percent_format(accuracy = 1)) +
  scale_x_continuous(breaks = round(seq(1820, 2020, by = 20),1)) + 
  scale_fill_manual(values=rev(scales::hue_pal()(2)), 
      labels = function(x) str_wrap(x, width = 15)) +
  labs(title = "Figure 6. Global income inequality: 
       \nBetween vs. within country inequality (Theil index), 1820-2020",
       x = "", y = "Share of global inequality (% of total Theil index)", fill = "") + 
  annotate("text", x = 1850, y = 0.28, 
      label = stringr::str_wrap("1820: Between country inequality represents 11% 
                                of global inequality", width = 20), size = 3) + 
  annotate("text", x = 1980, y = 0.70, 
      label = stringr::str_wrap("1980: Between country inequality represents 57% 
                                of global inequality", width = 20), size = 3) +
  annotate("text", x = 1990, y = 0.30, 
      label = stringr::str_wrap("2020: Between country inequality represents 32% 
                                of global inequality", width = 20), size = 3)
```

---


![](eda4_files/figure-html/unnamed-chunk-36-1.png)<!-- -->


---

### F11: Top 1% vs bottom 50% wealth shares in Western Europe and the US, 1910-2020 - pivot name_sep + fit curve


```r
df_f11 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F11"); df_f11
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["USbot50"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["UStop1"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["EUbot50"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["EUtop1"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"1910","2":"0.007000000","3":"0.4254405","4":"0.01279333","5":"0.5543653"},{"1":"1920","2":"0.010233268","3":"0.4095210","4":"0.01393704","5":"0.4960562"},{"1":"1930","2":"0.007371547","3":"0.4091269","4":"0.01746296","5":"0.4636822"},{"1":"1940","2":"0.011213015","3":"0.3185391","4":"0.02824333","5":"0.4116194"},{"1":"1950","2":"0.027012533","3":"0.2760278","4":"0.02716333","5":"0.3388022"},{"1":"1960","2":"0.023194874","3":"0.2787299","4":"0.05026667","5":"0.3044353"},{"1":"1970","2":"0.022070000","3":"0.2408800","4":"0.06493667","5":"0.2349556"},{"1":"1980","2":"0.026040001","3":"0.2512800","4":"0.06583333","5":"0.2004263"},{"1":"1990","2":"0.021070000","3":"0.2939800","4":"0.05354417","5":"0.1996896"},{"1":"2000","2":"0.016200000","3":"0.3228200","4":"0.05428167","5":"0.2144617"},{"1":"2010","2":"0.011130000","3":"0.3574800","4":"0.04997167","5":"0.2190700"},{"1":"2020","2":"0.014900000","3":"0.3537500","4":"0.05762500","5":"0.2193208"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f11 %>% 
  rename(!year, US_bot50 = USbot50, US_top1 = UStop1, 
         EU_bot50 = EUbot50, EU_top1 = EUtop1) %>%
  pivot_longer(!year, names_to = c("group",".value"), names_sep = "_") %>%
  pivot_longer(3:4, names_to = "type", values_to = "value") %>%
  ggplot() +
  stat_smooth(aes(x = year, y = value, color = group, linetype = type), 
              span = 0.25, se = FALSE) +
  scale_x_continuous(breaks = round(seq(1910, 2020, by = 10),1)) +
  scale_y_continuous(labels = scales::percent_format(accuracy = 1)) +
  labs(title = "Figure 11. Top 1% vs bottom 50% wealth shares 
       \n in Western Europe and the US, 1910-2020", 
       x = "", y = "Share of total personal wealth (%)", color = "", linetype = "") +
  scale_linetype_manual(values = c("dotted","solid")) +
  annotate("text", x = 2000, y = 0.50, 
      label = stringr::str_wrap("Wealth inequality has been rising at 
        different speeds after a historical decline. The bottom 50% has always been 
                                extremely low.", width = 30), size = 3)
```


---

#### Step 1.


```r
df_f11 %>% rename(!year, US_bot50 = USbot50, US_top1 = UStop1, 
                  EU_bot50 = EUbot50, EU_top1 = EUtop1) 
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["US_bot50"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["US_top1"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["EU_bot50"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["EU_top1"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"1910","2":"0.007000000","3":"0.4254405","4":"0.01279333","5":"0.5543653"},{"1":"1920","2":"0.010233268","3":"0.4095210","4":"0.01393704","5":"0.4960562"},{"1":"1930","2":"0.007371547","3":"0.4091269","4":"0.01746296","5":"0.4636822"},{"1":"1940","2":"0.011213015","3":"0.3185391","4":"0.02824333","5":"0.4116194"},{"1":"1950","2":"0.027012533","3":"0.2760278","4":"0.02716333","5":"0.3388022"},{"1":"1960","2":"0.023194874","3":"0.2787299","4":"0.05026667","5":"0.3044353"},{"1":"1970","2":"0.022070000","3":"0.2408800","4":"0.06493667","5":"0.2349556"},{"1":"1980","2":"0.026040001","3":"0.2512800","4":"0.06583333","5":"0.2004263"},{"1":"1990","2":"0.021070000","3":"0.2939800","4":"0.05354417","5":"0.1996896"},{"1":"2000","2":"0.016200000","3":"0.3228200","4":"0.05428167","5":"0.2144617"},{"1":"2010","2":"0.011130000","3":"0.3574800","4":"0.04997167","5":"0.2190700"},{"1":"2020","2":"0.014900000","3":"0.3537500","4":"0.05762500","5":"0.2193208"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

#### Step 2. 


```r
df_f11 %>% 
  rename(!year, US_bot50 = USbot50, US_top1 = UStop1, 
         EU_bot50 = EUbot50, EU_top1 = EUtop1) %>%
  pivot_longer(!year, names_to = c("group",".value"), names_sep = "_")
```

---

#### Step 2. 

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["group"],"name":[2],"type":["chr"],"align":["left"]},{"label":["bot50"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["top1"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"1910","2":"US","3":"0.007000000","4":"0.4254405"},{"1":"1910","2":"EU","3":"0.012793333","4":"0.5543653"},{"1":"1920","2":"US","3":"0.010233268","4":"0.4095210"},{"1":"1920","2":"EU","3":"0.013937037","4":"0.4960562"},{"1":"1930","2":"US","3":"0.007371547","4":"0.4091269"},{"1":"1930","2":"EU","3":"0.017462963","4":"0.4636822"},{"1":"1940","2":"US","3":"0.011213015","4":"0.3185391"},{"1":"1940","2":"EU","3":"0.028243333","4":"0.4116194"},{"1":"1950","2":"US","3":"0.027012533","4":"0.2760278"},{"1":"1950","2":"EU","3":"0.027163332","4":"0.3388022"},{"1":"1960","2":"US","3":"0.023194874","4":"0.2787299"},{"1":"1960","2":"EU","3":"0.050266668","4":"0.3044353"},{"1":"1970","2":"US","3":"0.022070000","4":"0.2408800"},{"1":"1970","2":"EU","3":"0.064936668","4":"0.2349556"},{"1":"1980","2":"US","3":"0.026040001","4":"0.2512800"},{"1":"1980","2":"EU","3":"0.065833330","4":"0.2004263"},{"1":"1990","2":"US","3":"0.021070000","4":"0.2939800"},{"1":"1990","2":"EU","3":"0.053544167","4":"0.1996896"},{"1":"2000","2":"US","3":"0.016200000","4":"0.3228200"},{"1":"2000","2":"EU","3":"0.054281667","4":"0.2144617"},{"1":"2010","2":"US","3":"0.011130000","4":"0.3574800"},{"1":"2010","2":"EU","3":"0.049971666","4":"0.2190700"},{"1":"2020","2":"US","3":"0.014900000","4":"0.3537500"},{"1":"2020","2":"EU","3":"0.057624999","4":"0.2193208"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

#### Step 3.


```r
df_f11 %>% 
  rename(!year, US_bot50 = USbot50, US_top1 = UStop1, 
         EU_bot50 = EUbot50, EU_top1 = EUtop1) %>%
  pivot_longer(!year, names_to = c("group",".value"), 
               names_sep = "_") %>%
  pivot_longer(3:4, names_to = "type", values_to = "value") 
```

---

#### Step 3.

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["group"],"name":[2],"type":["chr"],"align":["left"]},{"label":["type"],"name":[3],"type":["chr"],"align":["left"]},{"label":["value"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"1910","2":"US","3":"bot50","4":"0.007000000"},{"1":"1910","2":"US","3":"top1","4":"0.425440520"},{"1":"1910","2":"EU","3":"bot50","4":"0.012793333"},{"1":"1910","2":"EU","3":"top1","4":"0.554365277"},{"1":"1920","2":"US","3":"bot50","4":"0.010233268"},{"1":"1920","2":"US","3":"top1","4":"0.409521013"},{"1":"1920","2":"EU","3":"bot50","4":"0.013937037"},{"1":"1920","2":"EU","3":"top1","4":"0.496056229"},{"1":"1930","2":"US","3":"bot50","4":"0.007371547"},{"1":"1930","2":"US","3":"top1","4":"0.409126878"},{"1":"1930","2":"EU","3":"bot50","4":"0.017462963"},{"1":"1930","2":"EU","3":"top1","4":"0.463682175"},{"1":"1940","2":"US","3":"bot50","4":"0.011213015"},{"1":"1940","2":"US","3":"top1","4":"0.318539083"},{"1":"1940","2":"EU","3":"bot50","4":"0.028243333"},{"1":"1940","2":"EU","3":"top1","4":"0.411619425"},{"1":"1950","2":"US","3":"bot50","4":"0.027012533"},{"1":"1950","2":"US","3":"top1","4":"0.276027769"},{"1":"1950","2":"EU","3":"bot50","4":"0.027163332"},{"1":"1950","2":"EU","3":"top1","4":"0.338802159"},{"1":"1960","2":"US","3":"bot50","4":"0.023194874"},{"1":"1960","2":"US","3":"top1","4":"0.278729945"},{"1":"1960","2":"EU","3":"bot50","4":"0.050266668"},{"1":"1960","2":"EU","3":"top1","4":"0.304435313"},{"1":"1970","2":"US","3":"bot50","4":"0.022070000"},{"1":"1970","2":"US","3":"top1","4":"0.240879998"},{"1":"1970","2":"EU","3":"bot50","4":"0.064936668"},{"1":"1970","2":"EU","3":"top1","4":"0.234955609"},{"1":"1980","2":"US","3":"bot50","4":"0.026040001"},{"1":"1980","2":"US","3":"top1","4":"0.251280010"},{"1":"1980","2":"EU","3":"bot50","4":"0.065833330"},{"1":"1980","2":"EU","3":"top1","4":"0.200426340"},{"1":"1990","2":"US","3":"bot50","4":"0.021070000"},{"1":"1990","2":"US","3":"top1","4":"0.293980002"},{"1":"1990","2":"EU","3":"bot50","4":"0.053544167"},{"1":"1990","2":"EU","3":"top1","4":"0.199689597"},{"1":"2000","2":"US","3":"bot50","4":"0.016200000"},{"1":"2000","2":"US","3":"top1","4":"0.322820008"},{"1":"2000","2":"EU","3":"bot50","4":"0.054281667"},{"1":"2000","2":"EU","3":"top1","4":"0.214461669"},{"1":"2010","2":"US","3":"bot50","4":"0.011130000"},{"1":"2010","2":"US","3":"top1","4":"0.357479990"},{"1":"2010","2":"EU","3":"bot50","4":"0.049971666"},{"1":"2010","2":"EU","3":"top1","4":"0.219070002"},{"1":"2020","2":"US","3":"bot50","4":"0.014900000"},{"1":"2020","2":"US","3":"top1","4":"0.353749990"},{"1":"2020","2":"EU","3":"bot50","4":"0.057624999"},{"1":"2020","2":"EU","3":"top1","4":"0.219320834"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

![](eda4_files/figure-html/unnamed-chunk-43-1.png)<!-- -->

---

### F8: The rise of private versus the decline of public wealth in rich countries, 1970-2020 - rename + pivot + pivot + fit curve


```r
df_f8 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F8"); df_f8
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Germany"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["Germany (private)"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Spain"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["Spain (private)"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["France"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["France (private)"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["UK"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["UK (private)"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["Japan"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["Japan (private)"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["Norway"],"name":[12],"type":["dbl"],"align":["right"]},{"label":["Norway (private)"],"name":[13],"type":["dbl"],"align":["right"]},{"label":["USA"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["USA (private)"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["gwealAVGRICH"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["pwealAVGRICH"],"name":[17],"type":["dbl"],"align":["right"]}],"data":[{"1":"1970","2":"1.1116530","3":"2.298287","4":"0.6038899","5":"4.061005","6":"0.4216273","7":"3.120332","8":"0.60128810","9":"2.849942","10":"0.71940960","11":"3.092434","12":"NA","13":"NA","14":"0.36390920","15":"3.264223","16":"0.6369629","17":"3.114371"},{"1":"1971","2":"1.1170860","3":"2.248584","4":"0.6569503","5":"4.531124","6":"0.4426854","7":"3.057913","8":"0.68890840","9":"2.856148","10":"0.78210390","11":"3.356449","12":"NA","13":"NA","14":"0.38012850","15":"3.261986","16":"0.6779771","17":"3.218701"},{"1":"1972","2":"1.1143400","3":"2.267685","4":"0.6244062","5":"4.356174","6":"0.4668727","7":"3.082564","8":"0.78986150","9":"2.944858","10":"0.84188520","11":"3.847256","12":"NA","13":"NA","14":"0.37432040","15":"3.340595","16":"0.7019477","17":"3.306522"},{"1":"1973","2":"1.1066390","3":"2.233598","4":"0.5957342","5":"4.460879","6":"0.4781224","7":"3.062226","8":"0.92906140","9":"2.916999","10":"0.89474570","11":"4.158962","12":"NA","13":"NA","14":"0.40660970","15":"3.247478","16":"0.7351521","17":"3.346690"},{"1":"1974","2":"1.1332370","3":"2.252788","4":"0.5860708","5":"4.641235","6":"0.4979704","7":"3.034183","8":"1.08790600","9":"2.942605","10":"0.93590400","11":"3.983348","12":"NA","13":"NA","14":"0.50054130","15":"3.072135","16":"0.7902716","17":"3.321049"},{"1":"1975","2":"1.1155300","3":"2.350618","4":"0.6017208","5":"4.826020","6":"0.5450546","7":"3.119721","8":"1.00039000","9":"2.651910","10":"0.94407140","11":"3.832413","12":"NA","13":"NA","14":"0.52876290","15":"3.057138","16":"0.7892550","17":"3.306303"},{"1":"1976","2":"1.0339160","3":"2.341541","4":"0.5807208","5":"4.460111","6":"0.5613294","7":"3.077914","8":"0.91778720","9":"2.536953","10":"0.90228480","11":"3.754025","12":"NA","13":"NA","14":"0.48457710","15":"3.111119","16":"0.7467692","17":"3.213610"},{"1":"1977","2":"1.0051520","3":"2.421246","4":"0.5855834","5":"4.097454","6":"0.5674292","7":"3.098735","8":"0.86698500","9":"2.467270","10":"0.87971750","11":"3.736542","12":"NA","13":"NA","14":"0.47339750","15":"3.096011","16":"0.7297108","17":"3.152876"},{"1":"1978","2":"0.9895794","3":"2.517136","4":"0.6040155","5":"4.099272","6":"0.5800219","7":"3.198225","8":"0.88060180","9":"2.514017","10":"0.85960620","11":"3.801498","12":"NA","13":"NA","14":"0.47283040","15":"3.052021","16":"0.7311092","17":"3.197028"},{"1":"1979","2":"0.9889561","3":"2.547218","4":"0.6211699","5":"4.203296","6":"0.6241281","7":"3.297995","8":"0.95529160","9":"2.618359","10":"0.88377380","11":"4.094389","12":"NA","13":"NA","14":"0.51814040","15":"3.152546","16":"0.7652433","17":"3.318967"},{"1":"1980","2":"1.0082360","3":"2.619206","4":"0.5345857","5":"3.998411","6":"0.6858925","7":"3.330940","8":"1.02314000","9":"2.644479","10":"0.93260660","11":"4.397739","12":"NA","13":"NA","14":"0.61595070","15":"3.372149","16":"0.8000686","17":"3.393821"},{"1":"1981","2":"1.0177520","3":"2.761267","4":"0.5024298","5":"4.137168","6":"0.7139040","7":"3.331905","8":"1.06498500","9":"2.701759","10":"0.95314710","11":"4.630446","12":"NA","13":"NA","14":"0.63743420","15":"3.348484","16":"0.8149420","17":"3.485171"},{"1":"1982","2":"0.9902356","3":"2.916600","4":"0.4789951","5":"3.940957","6":"0.6943125","7":"3.247173","8":"1.00022900","9":"2.716308","10":"0.93725780","11":"4.801749","12":"NA","13":"NA","14":"0.63080690","15":"3.460664","16":"0.7886395","17":"3.513908"},{"1":"1983","2":"0.9507601","3":"3.026145","4":"0.4529042","5":"3.792417","6":"0.6889631","7":"3.261896","8":"0.92222340","9":"2.781023","10":"0.90197690","11":"4.949908","12":"NA","13":"NA","14":"0.56790170","15":"3.458572","16":"0.7474549","17":"3.544993"},{"1":"1984","2":"0.9208025","3":"3.101244","4":"0.4223034","5":"3.682976","6":"0.6726753","7":"3.258815","8":"0.89471820","9":"2.944163","10":"0.84567620","11":"4.942833","12":"NA","13":"NA","14":"0.47977030","15":"3.309495","16":"0.7059910","17":"3.539921"},{"1":"1985","2":"0.8996133","3":"3.200880","4":"0.3917901","5":"3.738055","6":"0.6365330","7":"3.212435","8":"0.86642760","9":"3.001313","10":"0.80189690","11":"4.922246","12":"NA","13":"NA","14":"0.43232440","15":"3.410516","16":"0.6714309","17":"3.580908"},{"1":"1986","2":"0.8765891","3":"3.270525","4":"0.3419330","5":"3.755674","6":"0.5865595","7":"3.211550","8":"0.85877390","9":"3.250525","10":"0.80112800","11":"5.372878","12":"NA","13":"NA","14":"0.40007330","15":"3.636201","16":"0.6441761","17":"3.749559"},{"1":"1987","2":"0.8789665","3":"3.401303","4":"0.3280651","5":"3.940125","6":"0.5680745","7":"3.252522","8":"0.82096210","9":"3.457419","10":"0.90052330","11":"6.231144","12":"NA","13":"NA","14":"0.36718910","15":"3.679318","16":"0.6439634","17":"3.993638"},{"1":"1988","2":"0.8478523","3":"3.408494","4":"0.3390966","5":"4.231590","6":"0.5498085","7":"3.222524","8":"0.84781340","9":"3.716459","10":"1.01407500","11":"6.685701","12":"NA","13":"NA","14":"0.33283060","15":"3.647151","16":"0.6552461","17":"4.151986"},{"1":"1989","2":"0.8339881","3":"3.401533","4":"0.3337033","5":"4.436543","6":"0.5370681","7":"3.313510","8":"0.83403580","9":"3.898324","10":"1.14424000","11":"7.035301","12":"NA","13":"NA","14":"0.31029870","15":"3.757195","16":"0.6655557","17":"4.307068"},{"1":"1990","2":"0.8595036","3":"3.425410","4":"0.3213641","5":"4.462528","6":"0.5289706","7":"3.344375","8":"0.72308610","9":"3.817370","10":"1.25096500","11":"7.119275","12":"NA","13":"NA","14":"0.28799930","15":"3.763592","16":"0.6619814","17":"4.322092"},{"1":"1991","2":"0.7745124","3":"3.118780","4":"0.3174739","5":"4.614971","6":"0.5211382","7":"3.337155","8":"0.61816970","9":"3.775208","10":"1.27453600","11":"6.801290","12":"NA","13":"NA","14":"0.25755490","15":"3.829902","16":"0.6272309","17":"4.246218"},{"1":"1992","2":"0.7222767","3":"3.143069","4":"0.2935957","5":"4.355422","6":"0.4936109","7":"3.273763","8":"0.49903240","9":"3.800560","10":"1.26159400","11":"6.426906","12":"NA","13":"NA","14":"0.19159750","15":"3.818645","16":"0.5769512","17":"4.136394"},{"1":"1993","2":"0.6827952","3":"3.278842","4":"0.2590353","5":"4.447897","6":"0.4404143","7":"3.311777","8":"0.37393440","9":"3.916970","10":"1.25223900","11":"6.264809","12":"NA","13":"NA","14":"0.13233770","15":"3.835537","16":"0.5234593","17":"4.175972"},{"1":"1994","2":"0.6504732","3":"3.316222","4":"0.2190626","5":"4.487134","6":"0.3844730","7":"3.265471","8":"0.31977080","9":"3.883329","10":"1.24683700","11":"6.210901","12":"NA","13":"NA","14":"0.10453160","15":"3.769563","16":"0.4875247","17":"4.155437"},{"1":"1995","2":"0.5779907","3":"3.385428","4":"0.3181907","5":"4.613816","6":"0.3409627","7":"3.173948","8":"0.18621574","9":"4.264322","10":"1.11272323","11":"6.165440","12":"1.062080","13":"2.5003991","14":"-0.01015096","15":"3.891953","16":"0.5125731","17":"3.999330"},{"1":"1996","2":"0.4922176","3":"3.492594","4":"0.2708890","5":"4.674306","6":"0.2891040","7":"3.297292","8":"0.04883918","9":"4.396181","10":"1.06029630","11":"6.087643","12":"1.100759","13":"2.4344251","14":"0.01051010","15":"3.968230","16":"0.4675165","17":"4.050096"},{"1":"1997","2":"0.4595755","3":"3.596153","4":"0.2395061","5":"4.724667","6":"0.2513431","7":"3.383261","8":"0.03361297","9":"4.516655","10":"1.03373075","11":"6.008512","12":"1.168976","13":"2.3903620","14":"0.06276285","15":"4.069162","16":"0.4642153","17":"4.098396"},{"1":"1998","2":"0.4229443","3":"3.695170","4":"0.2444649","5":"4.855223","6":"0.2294585","7":"3.397187","8":"0.01145423","9":"4.781518","10":"1.03942382","11":"6.209908","12":"1.295221","13":"2.4877925","14":"0.12571324","15":"4.265827","16":"0.4812400","17":"4.241804"},{"1":"1999","2":"0.3920051","3":"3.748546","4":"0.2945388","5":"5.138811","6":"0.2752688","7":"3.566447","8":"0.01666648","9":"4.929449","10":"0.99654120","11":"6.382850","12":"1.301801","13":"2.3947988","14":"0.19284114","15":"4.484062","16":"0.4956661","17":"4.377852"},{"1":"2000","2":"0.3750041","3":"3.757570","4":"0.3620185","5":"5.315041","6":"0.3253981","7":"3.720494","8":"0.04167610","9":"5.144637","10":"0.92694992","11":"6.371627","12":"1.266711","13":"2.1235237","14":"0.24440868","15":"4.460623","16":"0.5060237","17":"4.413360"},{"1":"2001","2":"0.3420957","3":"3.759231","4":"0.4111004","5":"5.544425","6":"0.3224427","7":"3.778800","8":"0.05643485","9":"5.127055","10":"0.86239475","11":"6.298085","12":"1.459666","13":"2.1430416","14":"0.27004132","15":"4.417081","16":"0.5320252","17":"4.438245"},{"1":"2002","2":"0.3002321","3":"3.783311","4":"0.4553619","5":"5.816341","6":"0.3164292","7":"3.893585","8":"0.04788728","9":"5.149401","10":"0.77602887","11":"6.254906","12":"1.555976","13":"2.2259414","14":"0.26549011","15":"4.321101","16":"0.5310579","17":"4.492084"},{"1":"2003","2":"0.2507073","3":"3.814120","4":"0.5072935","5":"6.238559","6":"0.3277472","7":"4.137745","8":"0.03161745","9":"5.305499","10":"0.69695836","11":"6.154943","12":"1.586331","13":"2.2268794","14":"0.25429934","15":"4.384949","16":"0.5221363","17":"4.608956"},{"1":"2004","2":"0.2024097","3":"3.810018","4":"0.5773532","5":"6.859021","6":"0.3704143","7":"4.466534","8":"0.03058806","9":"5.453795","10":"0.64557618","11":"6.029074","12":"1.666888","13":"2.1851928","14":"0.22911941","15":"4.676707","16":"0.5317642","17":"4.782906"},{"1":"2005","2":"0.1673112","3":"3.897755","4":"0.6615449","5":"7.377613","6":"0.4493050","7":"4.878516","8":"0.04279286","9":"5.628391","10":"0.63917983","11":"6.092587","12":"1.749523","13":"2.1392467","14":"0.22655702","15":"4.929497","16":"0.5623162","17":"4.991944"},{"1":"2006","2":"0.1574306","3":"3.820329","4":"0.7507362","5":"7.707107","6":"0.5494373","7":"5.216921","8":"0.06440135","9":"5.740703","10":"0.66539401","11":"6.208144","12":"1.931264","13":"2.1668105","14":"0.27519721","15":"5.022759","16":"0.6276944","17":"5.126111"},{"1":"2007","2":"0.1842021","3":"3.825864","4":"0.8352044","5":"7.991676","6":"0.6255011","7":"5.412782","8":"0.05150459","9":"5.838665","10":"0.68938506","11":"6.160019","12":"2.089367","13":"2.2743731","14":"0.31006292","15":"5.085441","16":"0.6836039","17":"5.226974"},{"1":"2008","2":"0.1991092","3":"3.893898","4":"0.8753186","5":"8.034274","6":"0.5773055","7":"5.315536","8":"-0.02833927","9":"5.352996","10":"0.64253807","11":"6.125224","12":"1.971432","13":"2.1704721","14":"0.21646091","15":"4.723100","16":"0.6362607","17":"5.087929"},{"1":"2009","2":"0.1995597","3":"4.132523","4":"0.8151094","5":"7.731181","6":"0.4899447","7":"5.347286","8":"-0.13180329","9":"5.021092","10":"0.53687960","11":"6.450859","12":"2.279538","13":"2.4426501","14":"0.02929429","15":"4.469103","16":"0.6026461","17":"5.084956"},{"1":"2010","2":"0.1732544","3":"4.096322","4":"0.7371387","5":"7.692125","6":"0.4562767","7":"5.455635","8":"-0.21362586","9":"5.479091","10":"0.38551483","11":"6.271574","12":"2.361421","13":"2.3929520","14":"-0.10685690","15":"4.402678","16":"0.5418746","17":"5.112911"},{"1":"2011","2":"0.1425285","3":"4.071341","4":"0.6943916","5":"7.610707","6":"0.4324422","7":"5.582475","8":"-0.32206973","9":"5.483580","10":"0.25148743","11":"6.219902","12":"2.372106","13":"2.3566232","14":"-0.19141020","15":"4.362327","16":"0.4827823","17":"5.098136"},{"1":"2012","2":"0.1432936","3":"4.134913","4":"0.6107365","5":"7.303093","6":"0.3629602","7":"5.655198","8":"-0.43769264","9":"5.703866","10":"0.15417218","11":"6.194554","12":"2.420273","13":"2.3955042","14":"-0.23970124","15":"4.339180","16":"0.4305774","17":"5.103758"},{"1":"2013","2":"0.1571628","3":"4.226473","4":"0.5061417","5":"7.113755","6":"0.3037324","7":"5.635610","8":"-0.43486899","9":"5.646983","10":"0.14775753","11":"6.239836","12":"2.730430","13":"2.4910398","14":"-0.26922482","15":"4.678563","16":"0.4487329","17":"5.147466"},{"1":"2014","2":"0.1542024","3":"4.255683","4":"0.3619758","5":"7.037822","6":"0.2324145","7":"5.582631","8":"-0.47626394","9":"5.849473","10":"0.16963848","11":"6.275792","12":"3.163658","13":"2.5279558","14":"-0.28567502","15":"4.908185","16":"0.4742786","17":"5.205363"},{"1":"2015","2":"0.1728468","3":"4.312161","4":"0.2425946","5":"6.833396","6":"0.1426092","7":"5.533938","8":"-0.53374809","9":"6.101383","10":"0.13765885","11":"6.146430","12":"3.695339","13":"2.7116034","14":"-0.30884099","15":"5.016471","16":"0.5069228","17":"5.236484"},{"1":"2016","2":"0.2074619","3":"4.359101","4":"0.2193690","5":"6.790277","6":"0.1108829","7":"5.647025","8":"-0.58235788","9":"6.256257","10":"0.08187253","11":"6.165404","12":"3.994416","13":"2.9474621","14":"-0.32733789","15":"5.178541","16":"0.5291866","17":"5.334867"},{"1":"2017","2":"0.2467750","3":"4.419456","4":"0.2045213","5":"6.688774","6":"0.1204700","7":"5.740609","8":"-0.58932400","9":"6.304605","10":"0.06974822","11":"6.169096","12":"3.995240","13":"1.5419959","14":"-0.31652460","15":"5.394610","16":"0.5329865","17":"5.179878"},{"1":"2018","2":"0.3016775","3":"4.513276","4":"0.2054314","5":"6.617785","6":"0.1506514","7":"5.803434","8":"-0.53749311","9":"6.204275","10":"0.07431349","11":"6.195373","12":"3.911210","13":"0.1693022","14":"-0.31464568","15":"5.407139","16":"0.5415922","17":"4.987226"},{"1":"2019","2":"0.3628729","3":"4.699964","4":"0.2032113","5":"6.641635","6":"0.1665744","7":"5.997541","8":"-0.55601621","9":"6.284134","10":"0.07381691","11":"6.228940","12":"4.438136","13":"0.1917931","14":"-0.32255229","15":"5.603682","16":"0.6237203","17":"5.092527"},{"1":"2020","2":"0.1802559","3":"5.018459","4":"-0.1605915","5":"7.034594","6":"-0.1279124","7":"6.326760","8":"-1.05782545","9":"6.818655","10":"-0.33760664","11":"6.675096","12":"4.976573","13":"0.3277966","14":"-0.60250711","15":"5.921504","16":"0.4100552","17":"5.446124"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f8 %>% 
  select(year, Germany_public = Germany, Germany_private = 'Germany (private)', 
         Spain_public = Spain, Spain_private = 'Spain (private)', 
         France_public = France, France_private = 'France (private)', 
         UK_public  = UK, UK_private = 'UK (private)', 
         Japan_public = Japan, Japan_private = 'Japan (private)', 
         Norway_public = Norway, Norway_private = 'Norway (private)',
         USA_public = USA, USA_private = 'USA (private)') %>%
  pivot_longer(!year, names_to = c("country",".value"), names_sep = "_") %>%
  pivot_longer(3:4, names_to = "type", values_to = "value") %>%
  ggplot() +
  stat_smooth(aes(x = year, y = value, color = country, linetype = type), 
              span = 0.25, se = FALSE, size=0.75) +
  scale_y_continuous(labels = scales::percent_format(accuracy = 1)) +
  labs(title = "Figure 8. The rise of private versus the decline of public 
       wealth in rich countries, 1970-2020", 
       x = "", y = "wealth as as % of national income", color = "", type = "")
```

---

#### Step 1


```r
df_f8 %>% 
  select(year, Germany_public = Germany, Germany_private = 'Germany (private)', 
         Spain_public = Spain, Spain_private = 'Spain (private)', 
         France_public = France, France_private = 'France (private)', 
         UK_public  = UK, UK_private = 'UK (private)', 
         Japan_public = Japan, Japan_private = 'Japan (private)', 
         Norway_public = Norway, Norway_private = 'Norway (private)',
         USA_public = USA, USA_private = 'USA (private)') 
```


---


<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["Germany_public"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["Germany_private"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Spain_public"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["Spain_private"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["France_public"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["France_private"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["UK_public"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["UK_private"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["Japan_public"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["Japan_private"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["Norway_public"],"name":[12],"type":["dbl"],"align":["right"]},{"label":["Norway_private"],"name":[13],"type":["dbl"],"align":["right"]},{"label":["USA_public"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["USA_private"],"name":[15],"type":["dbl"],"align":["right"]}],"data":[{"1":"1970","2":"1.1116530","3":"2.298287","4":"0.6038899","5":"4.061005","6":"0.4216273","7":"3.120332","8":"0.60128810","9":"2.849942","10":"0.71940960","11":"3.092434","12":"NA","13":"NA","14":"0.36390920","15":"3.264223"},{"1":"1971","2":"1.1170860","3":"2.248584","4":"0.6569503","5":"4.531124","6":"0.4426854","7":"3.057913","8":"0.68890840","9":"2.856148","10":"0.78210390","11":"3.356449","12":"NA","13":"NA","14":"0.38012850","15":"3.261986"},{"1":"1972","2":"1.1143400","3":"2.267685","4":"0.6244062","5":"4.356174","6":"0.4668727","7":"3.082564","8":"0.78986150","9":"2.944858","10":"0.84188520","11":"3.847256","12":"NA","13":"NA","14":"0.37432040","15":"3.340595"},{"1":"1973","2":"1.1066390","3":"2.233598","4":"0.5957342","5":"4.460879","6":"0.4781224","7":"3.062226","8":"0.92906140","9":"2.916999","10":"0.89474570","11":"4.158962","12":"NA","13":"NA","14":"0.40660970","15":"3.247478"},{"1":"1974","2":"1.1332370","3":"2.252788","4":"0.5860708","5":"4.641235","6":"0.4979704","7":"3.034183","8":"1.08790600","9":"2.942605","10":"0.93590400","11":"3.983348","12":"NA","13":"NA","14":"0.50054130","15":"3.072135"},{"1":"1975","2":"1.1155300","3":"2.350618","4":"0.6017208","5":"4.826020","6":"0.5450546","7":"3.119721","8":"1.00039000","9":"2.651910","10":"0.94407140","11":"3.832413","12":"NA","13":"NA","14":"0.52876290","15":"3.057138"},{"1":"1976","2":"1.0339160","3":"2.341541","4":"0.5807208","5":"4.460111","6":"0.5613294","7":"3.077914","8":"0.91778720","9":"2.536953","10":"0.90228480","11":"3.754025","12":"NA","13":"NA","14":"0.48457710","15":"3.111119"},{"1":"1977","2":"1.0051520","3":"2.421246","4":"0.5855834","5":"4.097454","6":"0.5674292","7":"3.098735","8":"0.86698500","9":"2.467270","10":"0.87971750","11":"3.736542","12":"NA","13":"NA","14":"0.47339750","15":"3.096011"},{"1":"1978","2":"0.9895794","3":"2.517136","4":"0.6040155","5":"4.099272","6":"0.5800219","7":"3.198225","8":"0.88060180","9":"2.514017","10":"0.85960620","11":"3.801498","12":"NA","13":"NA","14":"0.47283040","15":"3.052021"},{"1":"1979","2":"0.9889561","3":"2.547218","4":"0.6211699","5":"4.203296","6":"0.6241281","7":"3.297995","8":"0.95529160","9":"2.618359","10":"0.88377380","11":"4.094389","12":"NA","13":"NA","14":"0.51814040","15":"3.152546"},{"1":"1980","2":"1.0082360","3":"2.619206","4":"0.5345857","5":"3.998411","6":"0.6858925","7":"3.330940","8":"1.02314000","9":"2.644479","10":"0.93260660","11":"4.397739","12":"NA","13":"NA","14":"0.61595070","15":"3.372149"},{"1":"1981","2":"1.0177520","3":"2.761267","4":"0.5024298","5":"4.137168","6":"0.7139040","7":"3.331905","8":"1.06498500","9":"2.701759","10":"0.95314710","11":"4.630446","12":"NA","13":"NA","14":"0.63743420","15":"3.348484"},{"1":"1982","2":"0.9902356","3":"2.916600","4":"0.4789951","5":"3.940957","6":"0.6943125","7":"3.247173","8":"1.00022900","9":"2.716308","10":"0.93725780","11":"4.801749","12":"NA","13":"NA","14":"0.63080690","15":"3.460664"},{"1":"1983","2":"0.9507601","3":"3.026145","4":"0.4529042","5":"3.792417","6":"0.6889631","7":"3.261896","8":"0.92222340","9":"2.781023","10":"0.90197690","11":"4.949908","12":"NA","13":"NA","14":"0.56790170","15":"3.458572"},{"1":"1984","2":"0.9208025","3":"3.101244","4":"0.4223034","5":"3.682976","6":"0.6726753","7":"3.258815","8":"0.89471820","9":"2.944163","10":"0.84567620","11":"4.942833","12":"NA","13":"NA","14":"0.47977030","15":"3.309495"},{"1":"1985","2":"0.8996133","3":"3.200880","4":"0.3917901","5":"3.738055","6":"0.6365330","7":"3.212435","8":"0.86642760","9":"3.001313","10":"0.80189690","11":"4.922246","12":"NA","13":"NA","14":"0.43232440","15":"3.410516"},{"1":"1986","2":"0.8765891","3":"3.270525","4":"0.3419330","5":"3.755674","6":"0.5865595","7":"3.211550","8":"0.85877390","9":"3.250525","10":"0.80112800","11":"5.372878","12":"NA","13":"NA","14":"0.40007330","15":"3.636201"},{"1":"1987","2":"0.8789665","3":"3.401303","4":"0.3280651","5":"3.940125","6":"0.5680745","7":"3.252522","8":"0.82096210","9":"3.457419","10":"0.90052330","11":"6.231144","12":"NA","13":"NA","14":"0.36718910","15":"3.679318"},{"1":"1988","2":"0.8478523","3":"3.408494","4":"0.3390966","5":"4.231590","6":"0.5498085","7":"3.222524","8":"0.84781340","9":"3.716459","10":"1.01407500","11":"6.685701","12":"NA","13":"NA","14":"0.33283060","15":"3.647151"},{"1":"1989","2":"0.8339881","3":"3.401533","4":"0.3337033","5":"4.436543","6":"0.5370681","7":"3.313510","8":"0.83403580","9":"3.898324","10":"1.14424000","11":"7.035301","12":"NA","13":"NA","14":"0.31029870","15":"3.757195"},{"1":"1990","2":"0.8595036","3":"3.425410","4":"0.3213641","5":"4.462528","6":"0.5289706","7":"3.344375","8":"0.72308610","9":"3.817370","10":"1.25096500","11":"7.119275","12":"NA","13":"NA","14":"0.28799930","15":"3.763592"},{"1":"1991","2":"0.7745124","3":"3.118780","4":"0.3174739","5":"4.614971","6":"0.5211382","7":"3.337155","8":"0.61816970","9":"3.775208","10":"1.27453600","11":"6.801290","12":"NA","13":"NA","14":"0.25755490","15":"3.829902"},{"1":"1992","2":"0.7222767","3":"3.143069","4":"0.2935957","5":"4.355422","6":"0.4936109","7":"3.273763","8":"0.49903240","9":"3.800560","10":"1.26159400","11":"6.426906","12":"NA","13":"NA","14":"0.19159750","15":"3.818645"},{"1":"1993","2":"0.6827952","3":"3.278842","4":"0.2590353","5":"4.447897","6":"0.4404143","7":"3.311777","8":"0.37393440","9":"3.916970","10":"1.25223900","11":"6.264809","12":"NA","13":"NA","14":"0.13233770","15":"3.835537"},{"1":"1994","2":"0.6504732","3":"3.316222","4":"0.2190626","5":"4.487134","6":"0.3844730","7":"3.265471","8":"0.31977080","9":"3.883329","10":"1.24683700","11":"6.210901","12":"NA","13":"NA","14":"0.10453160","15":"3.769563"},{"1":"1995","2":"0.5779907","3":"3.385428","4":"0.3181907","5":"4.613816","6":"0.3409627","7":"3.173948","8":"0.18621574","9":"4.264322","10":"1.11272323","11":"6.165440","12":"1.062080","13":"2.5003991","14":"-0.01015096","15":"3.891953"},{"1":"1996","2":"0.4922176","3":"3.492594","4":"0.2708890","5":"4.674306","6":"0.2891040","7":"3.297292","8":"0.04883918","9":"4.396181","10":"1.06029630","11":"6.087643","12":"1.100759","13":"2.4344251","14":"0.01051010","15":"3.968230"},{"1":"1997","2":"0.4595755","3":"3.596153","4":"0.2395061","5":"4.724667","6":"0.2513431","7":"3.383261","8":"0.03361297","9":"4.516655","10":"1.03373075","11":"6.008512","12":"1.168976","13":"2.3903620","14":"0.06276285","15":"4.069162"},{"1":"1998","2":"0.4229443","3":"3.695170","4":"0.2444649","5":"4.855223","6":"0.2294585","7":"3.397187","8":"0.01145423","9":"4.781518","10":"1.03942382","11":"6.209908","12":"1.295221","13":"2.4877925","14":"0.12571324","15":"4.265827"},{"1":"1999","2":"0.3920051","3":"3.748546","4":"0.2945388","5":"5.138811","6":"0.2752688","7":"3.566447","8":"0.01666648","9":"4.929449","10":"0.99654120","11":"6.382850","12":"1.301801","13":"2.3947988","14":"0.19284114","15":"4.484062"},{"1":"2000","2":"0.3750041","3":"3.757570","4":"0.3620185","5":"5.315041","6":"0.3253981","7":"3.720494","8":"0.04167610","9":"5.144637","10":"0.92694992","11":"6.371627","12":"1.266711","13":"2.1235237","14":"0.24440868","15":"4.460623"},{"1":"2001","2":"0.3420957","3":"3.759231","4":"0.4111004","5":"5.544425","6":"0.3224427","7":"3.778800","8":"0.05643485","9":"5.127055","10":"0.86239475","11":"6.298085","12":"1.459666","13":"2.1430416","14":"0.27004132","15":"4.417081"},{"1":"2002","2":"0.3002321","3":"3.783311","4":"0.4553619","5":"5.816341","6":"0.3164292","7":"3.893585","8":"0.04788728","9":"5.149401","10":"0.77602887","11":"6.254906","12":"1.555976","13":"2.2259414","14":"0.26549011","15":"4.321101"},{"1":"2003","2":"0.2507073","3":"3.814120","4":"0.5072935","5":"6.238559","6":"0.3277472","7":"4.137745","8":"0.03161745","9":"5.305499","10":"0.69695836","11":"6.154943","12":"1.586331","13":"2.2268794","14":"0.25429934","15":"4.384949"},{"1":"2004","2":"0.2024097","3":"3.810018","4":"0.5773532","5":"6.859021","6":"0.3704143","7":"4.466534","8":"0.03058806","9":"5.453795","10":"0.64557618","11":"6.029074","12":"1.666888","13":"2.1851928","14":"0.22911941","15":"4.676707"},{"1":"2005","2":"0.1673112","3":"3.897755","4":"0.6615449","5":"7.377613","6":"0.4493050","7":"4.878516","8":"0.04279286","9":"5.628391","10":"0.63917983","11":"6.092587","12":"1.749523","13":"2.1392467","14":"0.22655702","15":"4.929497"},{"1":"2006","2":"0.1574306","3":"3.820329","4":"0.7507362","5":"7.707107","6":"0.5494373","7":"5.216921","8":"0.06440135","9":"5.740703","10":"0.66539401","11":"6.208144","12":"1.931264","13":"2.1668105","14":"0.27519721","15":"5.022759"},{"1":"2007","2":"0.1842021","3":"3.825864","4":"0.8352044","5":"7.991676","6":"0.6255011","7":"5.412782","8":"0.05150459","9":"5.838665","10":"0.68938506","11":"6.160019","12":"2.089367","13":"2.2743731","14":"0.31006292","15":"5.085441"},{"1":"2008","2":"0.1991092","3":"3.893898","4":"0.8753186","5":"8.034274","6":"0.5773055","7":"5.315536","8":"-0.02833927","9":"5.352996","10":"0.64253807","11":"6.125224","12":"1.971432","13":"2.1704721","14":"0.21646091","15":"4.723100"},{"1":"2009","2":"0.1995597","3":"4.132523","4":"0.8151094","5":"7.731181","6":"0.4899447","7":"5.347286","8":"-0.13180329","9":"5.021092","10":"0.53687960","11":"6.450859","12":"2.279538","13":"2.4426501","14":"0.02929429","15":"4.469103"},{"1":"2010","2":"0.1732544","3":"4.096322","4":"0.7371387","5":"7.692125","6":"0.4562767","7":"5.455635","8":"-0.21362586","9":"5.479091","10":"0.38551483","11":"6.271574","12":"2.361421","13":"2.3929520","14":"-0.10685690","15":"4.402678"},{"1":"2011","2":"0.1425285","3":"4.071341","4":"0.6943916","5":"7.610707","6":"0.4324422","7":"5.582475","8":"-0.32206973","9":"5.483580","10":"0.25148743","11":"6.219902","12":"2.372106","13":"2.3566232","14":"-0.19141020","15":"4.362327"},{"1":"2012","2":"0.1432936","3":"4.134913","4":"0.6107365","5":"7.303093","6":"0.3629602","7":"5.655198","8":"-0.43769264","9":"5.703866","10":"0.15417218","11":"6.194554","12":"2.420273","13":"2.3955042","14":"-0.23970124","15":"4.339180"},{"1":"2013","2":"0.1571628","3":"4.226473","4":"0.5061417","5":"7.113755","6":"0.3037324","7":"5.635610","8":"-0.43486899","9":"5.646983","10":"0.14775753","11":"6.239836","12":"2.730430","13":"2.4910398","14":"-0.26922482","15":"4.678563"},{"1":"2014","2":"0.1542024","3":"4.255683","4":"0.3619758","5":"7.037822","6":"0.2324145","7":"5.582631","8":"-0.47626394","9":"5.849473","10":"0.16963848","11":"6.275792","12":"3.163658","13":"2.5279558","14":"-0.28567502","15":"4.908185"},{"1":"2015","2":"0.1728468","3":"4.312161","4":"0.2425946","5":"6.833396","6":"0.1426092","7":"5.533938","8":"-0.53374809","9":"6.101383","10":"0.13765885","11":"6.146430","12":"3.695339","13":"2.7116034","14":"-0.30884099","15":"5.016471"},{"1":"2016","2":"0.2074619","3":"4.359101","4":"0.2193690","5":"6.790277","6":"0.1108829","7":"5.647025","8":"-0.58235788","9":"6.256257","10":"0.08187253","11":"6.165404","12":"3.994416","13":"2.9474621","14":"-0.32733789","15":"5.178541"},{"1":"2017","2":"0.2467750","3":"4.419456","4":"0.2045213","5":"6.688774","6":"0.1204700","7":"5.740609","8":"-0.58932400","9":"6.304605","10":"0.06974822","11":"6.169096","12":"3.995240","13":"1.5419959","14":"-0.31652460","15":"5.394610"},{"1":"2018","2":"0.3016775","3":"4.513276","4":"0.2054314","5":"6.617785","6":"0.1506514","7":"5.803434","8":"-0.53749311","9":"6.204275","10":"0.07431349","11":"6.195373","12":"3.911210","13":"0.1693022","14":"-0.31464568","15":"5.407139"},{"1":"2019","2":"0.3628729","3":"4.699964","4":"0.2032113","5":"6.641635","6":"0.1665744","7":"5.997541","8":"-0.55601621","9":"6.284134","10":"0.07381691","11":"6.228940","12":"4.438136","13":"0.1917931","14":"-0.32255229","15":"5.603682"},{"1":"2020","2":"0.1802559","3":"5.018459","4":"-0.1605915","5":"7.034594","6":"-0.1279124","7":"6.326760","8":"-1.05782545","9":"6.818655","10":"-0.33760664","11":"6.675096","12":"4.976573","13":"0.3277966","14":"-0.60250711","15":"5.921504"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>




---

#### Step 2.


```r
df_f8 %>% 
  select(year, Germany_public = Germany, Germany_private = 'Germany (private)', 
         Spain_public = Spain, Spain_private = 'Spain (private)', 
         France_public = France, France_private = 'France (private)', 
         UK_public  = UK, UK_private = 'UK (private)', 
         Japan_public = Japan, Japan_private = 'Japan (private)', 
         Norway_public = Norway, Norway_private = 'Norway (private)',
         USA_public = USA, USA_private = 'USA (private)') %>%
  pivot_longer(!year, names_to = c("country",".value"), names_sep = "_") 
```


---

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["country"],"name":[2],"type":["chr"],"align":["left"]},{"label":["public"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["private"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"1970","2":"Germany","3":"1.11165300","4":"2.2982870"},{"1":"1970","2":"Spain","3":"0.60388990","4":"4.0610050"},{"1":"1970","2":"France","3":"0.42162730","4":"3.1203320"},{"1":"1970","2":"UK","3":"0.60128810","4":"2.8499420"},{"1":"1970","2":"Japan","3":"0.71940960","4":"3.0924340"},{"1":"1970","2":"Norway","3":"NA","4":"NA"},{"1":"1970","2":"USA","3":"0.36390920","4":"3.2642230"},{"1":"1971","2":"Germany","3":"1.11708600","4":"2.2485840"},{"1":"1971","2":"Spain","3":"0.65695030","4":"4.5311240"},{"1":"1971","2":"France","3":"0.44268540","4":"3.0579130"},{"1":"1971","2":"UK","3":"0.68890840","4":"2.8561480"},{"1":"1971","2":"Japan","3":"0.78210390","4":"3.3564490"},{"1":"1971","2":"Norway","3":"NA","4":"NA"},{"1":"1971","2":"USA","3":"0.38012850","4":"3.2619860"},{"1":"1972","2":"Germany","3":"1.11434000","4":"2.2676850"},{"1":"1972","2":"Spain","3":"0.62440620","4":"4.3561740"},{"1":"1972","2":"France","3":"0.46687270","4":"3.0825640"},{"1":"1972","2":"UK","3":"0.78986150","4":"2.9448580"},{"1":"1972","2":"Japan","3":"0.84188520","4":"3.8472560"},{"1":"1972","2":"Norway","3":"NA","4":"NA"},{"1":"1972","2":"USA","3":"0.37432040","4":"3.3405950"},{"1":"1973","2":"Germany","3":"1.10663900","4":"2.2335980"},{"1":"1973","2":"Spain","3":"0.59573420","4":"4.4608790"},{"1":"1973","2":"France","3":"0.47812240","4":"3.0622260"},{"1":"1973","2":"UK","3":"0.92906140","4":"2.9169990"},{"1":"1973","2":"Japan","3":"0.89474570","4":"4.1589620"},{"1":"1973","2":"Norway","3":"NA","4":"NA"},{"1":"1973","2":"USA","3":"0.40660970","4":"3.2474780"},{"1":"1974","2":"Germany","3":"1.13323700","4":"2.2527880"},{"1":"1974","2":"Spain","3":"0.58607080","4":"4.6412350"},{"1":"1974","2":"France","3":"0.49797040","4":"3.0341830"},{"1":"1974","2":"UK","3":"1.08790600","4":"2.9426050"},{"1":"1974","2":"Japan","3":"0.93590400","4":"3.9833480"},{"1":"1974","2":"Norway","3":"NA","4":"NA"},{"1":"1974","2":"USA","3":"0.50054130","4":"3.0721350"},{"1":"1975","2":"Germany","3":"1.11553000","4":"2.3506180"},{"1":"1975","2":"Spain","3":"0.60172080","4":"4.8260200"},{"1":"1975","2":"France","3":"0.54505460","4":"3.1197210"},{"1":"1975","2":"UK","3":"1.00039000","4":"2.6519100"},{"1":"1975","2":"Japan","3":"0.94407140","4":"3.8324130"},{"1":"1975","2":"Norway","3":"NA","4":"NA"},{"1":"1975","2":"USA","3":"0.52876290","4":"3.0571380"},{"1":"1976","2":"Germany","3":"1.03391600","4":"2.3415410"},{"1":"1976","2":"Spain","3":"0.58072080","4":"4.4601110"},{"1":"1976","2":"France","3":"0.56132940","4":"3.0779140"},{"1":"1976","2":"UK","3":"0.91778720","4":"2.5369530"},{"1":"1976","2":"Japan","3":"0.90228480","4":"3.7540250"},{"1":"1976","2":"Norway","3":"NA","4":"NA"},{"1":"1976","2":"USA","3":"0.48457710","4":"3.1111190"},{"1":"1977","2":"Germany","3":"1.00515200","4":"2.4212460"},{"1":"1977","2":"Spain","3":"0.58558340","4":"4.0974540"},{"1":"1977","2":"France","3":"0.56742920","4":"3.0987350"},{"1":"1977","2":"UK","3":"0.86698500","4":"2.4672700"},{"1":"1977","2":"Japan","3":"0.87971750","4":"3.7365420"},{"1":"1977","2":"Norway","3":"NA","4":"NA"},{"1":"1977","2":"USA","3":"0.47339750","4":"3.0960110"},{"1":"1978","2":"Germany","3":"0.98957940","4":"2.5171360"},{"1":"1978","2":"Spain","3":"0.60401550","4":"4.0992720"},{"1":"1978","2":"France","3":"0.58002190","4":"3.1982250"},{"1":"1978","2":"UK","3":"0.88060180","4":"2.5140170"},{"1":"1978","2":"Japan","3":"0.85960620","4":"3.8014980"},{"1":"1978","2":"Norway","3":"NA","4":"NA"},{"1":"1978","2":"USA","3":"0.47283040","4":"3.0520210"},{"1":"1979","2":"Germany","3":"0.98895610","4":"2.5472180"},{"1":"1979","2":"Spain","3":"0.62116990","4":"4.2032960"},{"1":"1979","2":"France","3":"0.62412810","4":"3.2979950"},{"1":"1979","2":"UK","3":"0.95529160","4":"2.6183590"},{"1":"1979","2":"Japan","3":"0.88377380","4":"4.0943890"},{"1":"1979","2":"Norway","3":"NA","4":"NA"},{"1":"1979","2":"USA","3":"0.51814040","4":"3.1525460"},{"1":"1980","2":"Germany","3":"1.00823600","4":"2.6192060"},{"1":"1980","2":"Spain","3":"0.53458570","4":"3.9984110"},{"1":"1980","2":"France","3":"0.68589250","4":"3.3309400"},{"1":"1980","2":"UK","3":"1.02314000","4":"2.6444790"},{"1":"1980","2":"Japan","3":"0.93260660","4":"4.3977390"},{"1":"1980","2":"Norway","3":"NA","4":"NA"},{"1":"1980","2":"USA","3":"0.61595070","4":"3.3721490"},{"1":"1981","2":"Germany","3":"1.01775200","4":"2.7612670"},{"1":"1981","2":"Spain","3":"0.50242980","4":"4.1371680"},{"1":"1981","2":"France","3":"0.71390400","4":"3.3319050"},{"1":"1981","2":"UK","3":"1.06498500","4":"2.7017590"},{"1":"1981","2":"Japan","3":"0.95314710","4":"4.6304460"},{"1":"1981","2":"Norway","3":"NA","4":"NA"},{"1":"1981","2":"USA","3":"0.63743420","4":"3.3484840"},{"1":"1982","2":"Germany","3":"0.99023560","4":"2.9166000"},{"1":"1982","2":"Spain","3":"0.47899510","4":"3.9409570"},{"1":"1982","2":"France","3":"0.69431250","4":"3.2471730"},{"1":"1982","2":"UK","3":"1.00022900","4":"2.7163080"},{"1":"1982","2":"Japan","3":"0.93725780","4":"4.8017490"},{"1":"1982","2":"Norway","3":"NA","4":"NA"},{"1":"1982","2":"USA","3":"0.63080690","4":"3.4606640"},{"1":"1983","2":"Germany","3":"0.95076010","4":"3.0261450"},{"1":"1983","2":"Spain","3":"0.45290420","4":"3.7924170"},{"1":"1983","2":"France","3":"0.68896310","4":"3.2618960"},{"1":"1983","2":"UK","3":"0.92222340","4":"2.7810230"},{"1":"1983","2":"Japan","3":"0.90197690","4":"4.9499080"},{"1":"1983","2":"Norway","3":"NA","4":"NA"},{"1":"1983","2":"USA","3":"0.56790170","4":"3.4585720"},{"1":"1984","2":"Germany","3":"0.92080250","4":"3.1012440"},{"1":"1984","2":"Spain","3":"0.42230340","4":"3.6829760"},{"1":"1984","2":"France","3":"0.67267530","4":"3.2588150"},{"1":"1984","2":"UK","3":"0.89471820","4":"2.9441630"},{"1":"1984","2":"Japan","3":"0.84567620","4":"4.9428330"},{"1":"1984","2":"Norway","3":"NA","4":"NA"},{"1":"1984","2":"USA","3":"0.47977030","4":"3.3094950"},{"1":"1985","2":"Germany","3":"0.89961330","4":"3.2008800"},{"1":"1985","2":"Spain","3":"0.39179010","4":"3.7380550"},{"1":"1985","2":"France","3":"0.63653300","4":"3.2124350"},{"1":"1985","2":"UK","3":"0.86642760","4":"3.0013130"},{"1":"1985","2":"Japan","3":"0.80189690","4":"4.9222460"},{"1":"1985","2":"Norway","3":"NA","4":"NA"},{"1":"1985","2":"USA","3":"0.43232440","4":"3.4105160"},{"1":"1986","2":"Germany","3":"0.87658910","4":"3.2705250"},{"1":"1986","2":"Spain","3":"0.34193300","4":"3.7556740"},{"1":"1986","2":"France","3":"0.58655950","4":"3.2115500"},{"1":"1986","2":"UK","3":"0.85877390","4":"3.2505250"},{"1":"1986","2":"Japan","3":"0.80112800","4":"5.3728780"},{"1":"1986","2":"Norway","3":"NA","4":"NA"},{"1":"1986","2":"USA","3":"0.40007330","4":"3.6362010"},{"1":"1987","2":"Germany","3":"0.87896650","4":"3.4013030"},{"1":"1987","2":"Spain","3":"0.32806510","4":"3.9401250"},{"1":"1987","2":"France","3":"0.56807450","4":"3.2525220"},{"1":"1987","2":"UK","3":"0.82096210","4":"3.4574190"},{"1":"1987","2":"Japan","3":"0.90052330","4":"6.2311440"},{"1":"1987","2":"Norway","3":"NA","4":"NA"},{"1":"1987","2":"USA","3":"0.36718910","4":"3.6793180"},{"1":"1988","2":"Germany","3":"0.84785230","4":"3.4084940"},{"1":"1988","2":"Spain","3":"0.33909660","4":"4.2315900"},{"1":"1988","2":"France","3":"0.54980850","4":"3.2225240"},{"1":"1988","2":"UK","3":"0.84781340","4":"3.7164590"},{"1":"1988","2":"Japan","3":"1.01407500","4":"6.6857010"},{"1":"1988","2":"Norway","3":"NA","4":"NA"},{"1":"1988","2":"USA","3":"0.33283060","4":"3.6471510"},{"1":"1989","2":"Germany","3":"0.83398810","4":"3.4015330"},{"1":"1989","2":"Spain","3":"0.33370330","4":"4.4365430"},{"1":"1989","2":"France","3":"0.53706810","4":"3.3135100"},{"1":"1989","2":"UK","3":"0.83403580","4":"3.8983240"},{"1":"1989","2":"Japan","3":"1.14424000","4":"7.0353010"},{"1":"1989","2":"Norway","3":"NA","4":"NA"},{"1":"1989","2":"USA","3":"0.31029870","4":"3.7571950"},{"1":"1990","2":"Germany","3":"0.85950360","4":"3.4254100"},{"1":"1990","2":"Spain","3":"0.32136410","4":"4.4625280"},{"1":"1990","2":"France","3":"0.52897060","4":"3.3443750"},{"1":"1990","2":"UK","3":"0.72308610","4":"3.8173700"},{"1":"1990","2":"Japan","3":"1.25096500","4":"7.1192750"},{"1":"1990","2":"Norway","3":"NA","4":"NA"},{"1":"1990","2":"USA","3":"0.28799930","4":"3.7635920"},{"1":"1991","2":"Germany","3":"0.77451240","4":"3.1187800"},{"1":"1991","2":"Spain","3":"0.31747390","4":"4.6149710"},{"1":"1991","2":"France","3":"0.52113820","4":"3.3371550"},{"1":"1991","2":"UK","3":"0.61816970","4":"3.7752080"},{"1":"1991","2":"Japan","3":"1.27453600","4":"6.8012900"},{"1":"1991","2":"Norway","3":"NA","4":"NA"},{"1":"1991","2":"USA","3":"0.25755490","4":"3.8299020"},{"1":"1992","2":"Germany","3":"0.72227670","4":"3.1430690"},{"1":"1992","2":"Spain","3":"0.29359570","4":"4.3554220"},{"1":"1992","2":"France","3":"0.49361090","4":"3.2737630"},{"1":"1992","2":"UK","3":"0.49903240","4":"3.8005600"},{"1":"1992","2":"Japan","3":"1.26159400","4":"6.4269060"},{"1":"1992","2":"Norway","3":"NA","4":"NA"},{"1":"1992","2":"USA","3":"0.19159750","4":"3.8186450"},{"1":"1993","2":"Germany","3":"0.68279520","4":"3.2788420"},{"1":"1993","2":"Spain","3":"0.25903530","4":"4.4478970"},{"1":"1993","2":"France","3":"0.44041430","4":"3.3117770"},{"1":"1993","2":"UK","3":"0.37393440","4":"3.9169700"},{"1":"1993","2":"Japan","3":"1.25223900","4":"6.2648090"},{"1":"1993","2":"Norway","3":"NA","4":"NA"},{"1":"1993","2":"USA","3":"0.13233770","4":"3.8355370"},{"1":"1994","2":"Germany","3":"0.65047320","4":"3.3162220"},{"1":"1994","2":"Spain","3":"0.21906260","4":"4.4871340"},{"1":"1994","2":"France","3":"0.38447300","4":"3.2654710"},{"1":"1994","2":"UK","3":"0.31977080","4":"3.8833290"},{"1":"1994","2":"Japan","3":"1.24683700","4":"6.2109010"},{"1":"1994","2":"Norway","3":"NA","4":"NA"},{"1":"1994","2":"USA","3":"0.10453160","4":"3.7695630"},{"1":"1995","2":"Germany","3":"0.57799065","4":"3.3854282"},{"1":"1995","2":"Spain","3":"0.31819066","4":"4.6138163"},{"1":"1995","2":"France","3":"0.34096268","4":"3.1739478"},{"1":"1995","2":"UK","3":"0.18621574","4":"4.2643223"},{"1":"1995","2":"Japan","3":"1.11272323","4":"6.1654401"},{"1":"1995","2":"Norway","3":"1.06207967","4":"2.5003991"},{"1":"1995","2":"USA","3":"-0.01015096","4":"3.8919528"},{"1":"1996","2":"Germany","3":"0.49221757","4":"3.4925940"},{"1":"1996","2":"Spain","3":"0.27088898","4":"4.6743059"},{"1":"1996","2":"France","3":"0.28910396","4":"3.2972925"},{"1":"1996","2":"UK","3":"0.04883918","4":"4.3961811"},{"1":"1996","2":"Japan","3":"1.06029630","4":"6.0876427"},{"1":"1996","2":"Norway","3":"1.10075939","4":"2.4344251"},{"1":"1996","2":"USA","3":"0.01051010","4":"3.9682305"},{"1":"1997","2":"Germany","3":"0.45957553","4":"3.5961525"},{"1":"1997","2":"Spain","3":"0.23950605","4":"4.7246671"},{"1":"1997","2":"France","3":"0.25134310","4":"3.3832614"},{"1":"1997","2":"UK","3":"0.03361297","4":"4.5166550"},{"1":"1997","2":"Japan","3":"1.03373075","4":"6.0085120"},{"1":"1997","2":"Norway","3":"1.16897571","4":"2.3903620"},{"1":"1997","2":"USA","3":"0.06276285","4":"4.0691619"},{"1":"1998","2":"Germany","3":"0.42294434","4":"3.6951704"},{"1":"1998","2":"Spain","3":"0.24446492","4":"4.8552227"},{"1":"1998","2":"France","3":"0.22945850","4":"3.3971868"},{"1":"1998","2":"UK","3":"0.01145423","4":"4.7815185"},{"1":"1998","2":"Japan","3":"1.03942382","4":"6.2099080"},{"1":"1998","2":"Norway","3":"1.29522109","4":"2.4877925"},{"1":"1998","2":"USA","3":"0.12571324","4":"4.2658267"},{"1":"1999","2":"Germany","3":"0.39200506","4":"3.7485456"},{"1":"1999","2":"Spain","3":"0.29453880","4":"5.1388106"},{"1":"1999","2":"France","3":"0.27526882","4":"3.5664468"},{"1":"1999","2":"UK","3":"0.01666648","4":"4.9294486"},{"1":"1999","2":"Japan","3":"0.99654120","4":"6.3828502"},{"1":"1999","2":"Norway","3":"1.30180120","4":"2.3947988"},{"1":"1999","2":"USA","3":"0.19284114","4":"4.4840617"},{"1":"2000","2":"Germany","3":"0.37500408","4":"3.7575696"},{"1":"2000","2":"Spain","3":"0.36201853","4":"5.3150411"},{"1":"2000","2":"France","3":"0.32539812","4":"3.7204938"},{"1":"2000","2":"UK","3":"0.04167610","4":"5.1446371"},{"1":"2000","2":"Japan","3":"0.92694992","4":"6.3716273"},{"1":"2000","2":"Norway","3":"1.26671052","4":"2.1235237"},{"1":"2000","2":"USA","3":"0.24440868","4":"4.4606233"},{"1":"2001","2":"Germany","3":"0.34209570","4":"3.7592313"},{"1":"2001","2":"Spain","3":"0.41110042","4":"5.5444245"},{"1":"2001","2":"France","3":"0.32244271","4":"3.7787995"},{"1":"2001","2":"UK","3":"0.05643485","4":"5.1270552"},{"1":"2001","2":"Japan","3":"0.86239475","4":"6.2980852"},{"1":"2001","2":"Norway","3":"1.45966637","4":"2.1430416"},{"1":"2001","2":"USA","3":"0.27004132","4":"4.4170809"},{"1":"2002","2":"Germany","3":"0.30023211","4":"3.7833109"},{"1":"2002","2":"Spain","3":"0.45536190","4":"5.8163409"},{"1":"2002","2":"France","3":"0.31642923","4":"3.8935850"},{"1":"2002","2":"UK","3":"0.04788728","4":"5.1494012"},{"1":"2002","2":"Japan","3":"0.77602887","4":"6.2549057"},{"1":"2002","2":"Norway","3":"1.55597591","4":"2.2259414"},{"1":"2002","2":"USA","3":"0.26549011","4":"4.3211007"},{"1":"2003","2":"Germany","3":"0.25070733","4":"3.8141201"},{"1":"2003","2":"Spain","3":"0.50729346","4":"6.2385592"},{"1":"2003","2":"France","3":"0.32774720","4":"4.1377454"},{"1":"2003","2":"UK","3":"0.03161745","4":"5.3054991"},{"1":"2003","2":"Japan","3":"0.69695836","4":"6.1549425"},{"1":"2003","2":"Norway","3":"1.58633137","4":"2.2268794"},{"1":"2003","2":"USA","3":"0.25429934","4":"4.3849492"},{"1":"2004","2":"Germany","3":"0.20240971","4":"3.8100178"},{"1":"2004","2":"Spain","3":"0.57735318","4":"6.8590212"},{"1":"2004","2":"France","3":"0.37041435","4":"4.4665337"},{"1":"2004","2":"UK","3":"0.03058806","4":"5.4537950"},{"1":"2004","2":"Japan","3":"0.64557618","4":"6.0290742"},{"1":"2004","2":"Norway","3":"1.66688848","4":"2.1851928"},{"1":"2004","2":"USA","3":"0.22911941","4":"4.6767073"},{"1":"2005","2":"Germany","3":"0.16731116","4":"3.8977549"},{"1":"2005","2":"Spain","3":"0.66154492","4":"7.3776131"},{"1":"2005","2":"France","3":"0.44930500","4":"4.8785162"},{"1":"2005","2":"UK","3":"0.04279286","4":"5.6283913"},{"1":"2005","2":"Japan","3":"0.63917983","4":"6.0925875"},{"1":"2005","2":"Norway","3":"1.74952257","4":"2.1392467"},{"1":"2005","2":"USA","3":"0.22655702","4":"4.9294968"},{"1":"2006","2":"Germany","3":"0.15743059","4":"3.8203292"},{"1":"2006","2":"Spain","3":"0.75073624","4":"7.7071066"},{"1":"2006","2":"France","3":"0.54943728","4":"5.2169213"},{"1":"2006","2":"UK","3":"0.06440135","4":"5.7407026"},{"1":"2006","2":"Japan","3":"0.66539401","4":"6.2081442"},{"1":"2006","2":"Norway","3":"1.93126416","4":"2.1668105"},{"1":"2006","2":"USA","3":"0.27519721","4":"5.0227594"},{"1":"2007","2":"Germany","3":"0.18420206","4":"3.8258641"},{"1":"2007","2":"Spain","3":"0.83520442","4":"7.9916759"},{"1":"2007","2":"France","3":"0.62550110","4":"5.4127817"},{"1":"2007","2":"UK","3":"0.05150459","4":"5.8386655"},{"1":"2007","2":"Japan","3":"0.68938506","4":"6.1600189"},{"1":"2007","2":"Norway","3":"2.08936715","4":"2.2743731"},{"1":"2007","2":"USA","3":"0.31006292","4":"5.0854411"},{"1":"2008","2":"Germany","3":"0.19910918","4":"3.8938982"},{"1":"2008","2":"Spain","3":"0.87531859","4":"8.0342741"},{"1":"2008","2":"France","3":"0.57730550","4":"5.3155365"},{"1":"2008","2":"UK","3":"-0.02833927","4":"5.3529959"},{"1":"2008","2":"Japan","3":"0.64253807","4":"6.1252236"},{"1":"2008","2":"Norway","3":"1.97143221","4":"2.1704721"},{"1":"2008","2":"USA","3":"0.21646091","4":"4.7230997"},{"1":"2009","2":"Germany","3":"0.19955969","4":"4.1325226"},{"1":"2009","2":"Spain","3":"0.81510937","4":"7.7311811"},{"1":"2009","2":"France","3":"0.48994470","4":"5.3472857"},{"1":"2009","2":"UK","3":"-0.13180329","4":"5.0210919"},{"1":"2009","2":"Japan","3":"0.53687960","4":"6.4508591"},{"1":"2009","2":"Norway","3":"2.27953839","4":"2.4426501"},{"1":"2009","2":"USA","3":"0.02929429","4":"4.4691029"},{"1":"2010","2":"Germany","3":"0.17325440","4":"4.0963221"},{"1":"2010","2":"Spain","3":"0.73713875","4":"7.6921248"},{"1":"2010","2":"France","3":"0.45627671","4":"5.4556351"},{"1":"2010","2":"UK","3":"-0.21362586","4":"5.4790907"},{"1":"2010","2":"Japan","3":"0.38551483","4":"6.2715735"},{"1":"2010","2":"Norway","3":"2.36142063","4":"2.3929520"},{"1":"2010","2":"USA","3":"-0.10685690","4":"4.4026775"},{"1":"2011","2":"Germany","3":"0.14252852","4":"4.0713406"},{"1":"2011","2":"Spain","3":"0.69439161","4":"7.6107073"},{"1":"2011","2":"France","3":"0.43244216","4":"5.5824752"},{"1":"2011","2":"UK","3":"-0.32206973","4":"5.4835801"},{"1":"2011","2":"Japan","3":"0.25148743","4":"6.2199020"},{"1":"2011","2":"Norway","3":"2.37210631","4":"2.3566232"},{"1":"2011","2":"USA","3":"-0.19141020","4":"4.3623271"},{"1":"2012","2":"Germany","3":"0.14329356","4":"4.1349130"},{"1":"2012","2":"Spain","3":"0.61073655","4":"7.3030934"},{"1":"2012","2":"France","3":"0.36296016","4":"5.6551981"},{"1":"2012","2":"UK","3":"-0.43769264","4":"5.7038655"},{"1":"2012","2":"Japan","3":"0.15417218","4":"6.1945543"},{"1":"2012","2":"Norway","3":"2.42027330","4":"2.3955042"},{"1":"2012","2":"USA","3":"-0.23970124","4":"4.3391805"},{"1":"2013","2":"Germany","3":"0.15716285","4":"4.2264733"},{"1":"2013","2":"Spain","3":"0.50614172","4":"7.1137547"},{"1":"2013","2":"France","3":"0.30373242","4":"5.6356101"},{"1":"2013","2":"UK","3":"-0.43486899","4":"5.6469827"},{"1":"2013","2":"Japan","3":"0.14775753","4":"6.2398362"},{"1":"2013","2":"Norway","3":"2.73042965","4":"2.4910398"},{"1":"2013","2":"USA","3":"-0.26922482","4":"4.6785631"},{"1":"2014","2":"Germany","3":"0.15420237","4":"4.2556834"},{"1":"2014","2":"Spain","3":"0.36197579","4":"7.0378218"},{"1":"2014","2":"France","3":"0.23241447","4":"5.5826306"},{"1":"2014","2":"UK","3":"-0.47626394","4":"5.8494730"},{"1":"2014","2":"Japan","3":"0.16963848","4":"6.2757916"},{"1":"2014","2":"Norway","3":"3.16365790","4":"2.5279558"},{"1":"2014","2":"USA","3":"-0.28567502","4":"4.9081850"},{"1":"2015","2":"Germany","3":"0.17284682","4":"4.3121614"},{"1":"2015","2":"Spain","3":"0.24259460","4":"6.8333960"},{"1":"2015","2":"France","3":"0.14260918","4":"5.5339379"},{"1":"2015","2":"UK","3":"-0.53374809","4":"6.1013832"},{"1":"2015","2":"Japan","3":"0.13765885","4":"6.1464300"},{"1":"2015","2":"Norway","3":"3.69533944","4":"2.7116034"},{"1":"2015","2":"USA","3":"-0.30884099","4":"5.0164714"},{"1":"2016","2":"Germany","3":"0.20746191","4":"4.3591008"},{"1":"2016","2":"Spain","3":"0.21936896","4":"6.7902770"},{"1":"2016","2":"France","3":"0.11088289","4":"5.6470251"},{"1":"2016","2":"UK","3":"-0.58235788","4":"6.2562571"},{"1":"2016","2":"Japan","3":"0.08187253","4":"6.1654043"},{"1":"2016","2":"Norway","3":"3.99441552","4":"2.9474621"},{"1":"2016","2":"USA","3":"-0.32733789","4":"5.1785407"},{"1":"2017","2":"Germany","3":"0.24677505","4":"4.4194560"},{"1":"2017","2":"Spain","3":"0.20452128","4":"6.6887736"},{"1":"2017","2":"France","3":"0.12046999","4":"5.7406087"},{"1":"2017","2":"UK","3":"-0.58932400","4":"6.3046050"},{"1":"2017","2":"Japan","3":"0.06974822","4":"6.1690965"},{"1":"2017","2":"Norway","3":"3.99523973","4":"1.5419959"},{"1":"2017","2":"USA","3":"-0.31652460","4":"5.3946104"},{"1":"2018","2":"Germany","3":"0.30167750","4":"4.5132761"},{"1":"2018","2":"Spain","3":"0.20543142","4":"6.6177850"},{"1":"2018","2":"France","3":"0.15065138","4":"5.8034344"},{"1":"2018","2":"UK","3":"-0.53749311","4":"6.2042751"},{"1":"2018","2":"Japan","3":"0.07431349","4":"6.1953726"},{"1":"2018","2":"Norway","3":"3.91121030","4":"0.1693022"},{"1":"2018","2":"USA","3":"-0.31464568","4":"5.4071393"},{"1":"2019","2":"Germany","3":"0.36287290","4":"4.6999640"},{"1":"2019","2":"Spain","3":"0.20321131","4":"6.6416354"},{"1":"2019","2":"France","3":"0.16657437","4":"5.9975414"},{"1":"2019","2":"UK","3":"-0.55601621","4":"6.2841344"},{"1":"2019","2":"Japan","3":"0.07381691","4":"6.2289405"},{"1":"2019","2":"Norway","3":"4.43813562","4":"0.1917931"},{"1":"2019","2":"USA","3":"-0.32255229","4":"5.6036820"},{"1":"2020","2":"Germany","3":"0.18025590","4":"5.0184588"},{"1":"2020","2":"Spain","3":"-0.16059151","4":"7.0345941"},{"1":"2020","2":"France","3":"-0.12791239","4":"6.3267603"},{"1":"2020","2":"UK","3":"-1.05782545","4":"6.8186555"},{"1":"2020","2":"Japan","3":"-0.33760664","4":"6.6750960"},{"1":"2020","2":"Norway","3":"4.97657347","4":"0.3277966"},{"1":"2020","2":"USA","3":"-0.60250711","4":"5.9215035"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

#### Step 3.


```r
df_f8 %>% 
  select(year, Germany_public = Germany, Germany_private = 'Germany (private)', 
         Spain_public = Spain, Spain_private = 'Spain (private)', 
         France_public = France, France_private = 'France (private)', 
         UK_public  = UK, UK_private = 'UK (private)', 
         Japan_public = Japan, Japan_private = 'Japan (private)', 
         Norway_public = Norway, Norway_private = 'Norway (private)',
         USA_public = USA, USA_private = 'USA (private)') %>%
  pivot_longer(!year, names_to = c("country",".value"), names_sep = "_") %>%
  pivot_longer(3:4, names_to = "type", values_to = "value")
```

---


<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["year"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["country"],"name":[2],"type":["chr"],"align":["left"]},{"label":["type"],"name":[3],"type":["chr"],"align":["left"]},{"label":["value"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"1970","2":"Germany","3":"public","4":"1.11165300"},{"1":"1970","2":"Germany","3":"private","4":"2.29828700"},{"1":"1970","2":"Spain","3":"public","4":"0.60388990"},{"1":"1970","2":"Spain","3":"private","4":"4.06100500"},{"1":"1970","2":"France","3":"public","4":"0.42162730"},{"1":"1970","2":"France","3":"private","4":"3.12033200"},{"1":"1970","2":"UK","3":"public","4":"0.60128810"},{"1":"1970","2":"UK","3":"private","4":"2.84994200"},{"1":"1970","2":"Japan","3":"public","4":"0.71940960"},{"1":"1970","2":"Japan","3":"private","4":"3.09243400"},{"1":"1970","2":"Norway","3":"public","4":"NA"},{"1":"1970","2":"Norway","3":"private","4":"NA"},{"1":"1970","2":"USA","3":"public","4":"0.36390920"},{"1":"1970","2":"USA","3":"private","4":"3.26422300"},{"1":"1971","2":"Germany","3":"public","4":"1.11708600"},{"1":"1971","2":"Germany","3":"private","4":"2.24858400"},{"1":"1971","2":"Spain","3":"public","4":"0.65695030"},{"1":"1971","2":"Spain","3":"private","4":"4.53112400"},{"1":"1971","2":"France","3":"public","4":"0.44268540"},{"1":"1971","2":"France","3":"private","4":"3.05791300"},{"1":"1971","2":"UK","3":"public","4":"0.68890840"},{"1":"1971","2":"UK","3":"private","4":"2.85614800"},{"1":"1971","2":"Japan","3":"public","4":"0.78210390"},{"1":"1971","2":"Japan","3":"private","4":"3.35644900"},{"1":"1971","2":"Norway","3":"public","4":"NA"},{"1":"1971","2":"Norway","3":"private","4":"NA"},{"1":"1971","2":"USA","3":"public","4":"0.38012850"},{"1":"1971","2":"USA","3":"private","4":"3.26198600"},{"1":"1972","2":"Germany","3":"public","4":"1.11434000"},{"1":"1972","2":"Germany","3":"private","4":"2.26768500"},{"1":"1972","2":"Spain","3":"public","4":"0.62440620"},{"1":"1972","2":"Spain","3":"private","4":"4.35617400"},{"1":"1972","2":"France","3":"public","4":"0.46687270"},{"1":"1972","2":"France","3":"private","4":"3.08256400"},{"1":"1972","2":"UK","3":"public","4":"0.78986150"},{"1":"1972","2":"UK","3":"private","4":"2.94485800"},{"1":"1972","2":"Japan","3":"public","4":"0.84188520"},{"1":"1972","2":"Japan","3":"private","4":"3.84725600"},{"1":"1972","2":"Norway","3":"public","4":"NA"},{"1":"1972","2":"Norway","3":"private","4":"NA"},{"1":"1972","2":"USA","3":"public","4":"0.37432040"},{"1":"1972","2":"USA","3":"private","4":"3.34059500"},{"1":"1973","2":"Germany","3":"public","4":"1.10663900"},{"1":"1973","2":"Germany","3":"private","4":"2.23359800"},{"1":"1973","2":"Spain","3":"public","4":"0.59573420"},{"1":"1973","2":"Spain","3":"private","4":"4.46087900"},{"1":"1973","2":"France","3":"public","4":"0.47812240"},{"1":"1973","2":"France","3":"private","4":"3.06222600"},{"1":"1973","2":"UK","3":"public","4":"0.92906140"},{"1":"1973","2":"UK","3":"private","4":"2.91699900"},{"1":"1973","2":"Japan","3":"public","4":"0.89474570"},{"1":"1973","2":"Japan","3":"private","4":"4.15896200"},{"1":"1973","2":"Norway","3":"public","4":"NA"},{"1":"1973","2":"Norway","3":"private","4":"NA"},{"1":"1973","2":"USA","3":"public","4":"0.40660970"},{"1":"1973","2":"USA","3":"private","4":"3.24747800"},{"1":"1974","2":"Germany","3":"public","4":"1.13323700"},{"1":"1974","2":"Germany","3":"private","4":"2.25278800"},{"1":"1974","2":"Spain","3":"public","4":"0.58607080"},{"1":"1974","2":"Spain","3":"private","4":"4.64123500"},{"1":"1974","2":"France","3":"public","4":"0.49797040"},{"1":"1974","2":"France","3":"private","4":"3.03418300"},{"1":"1974","2":"UK","3":"public","4":"1.08790600"},{"1":"1974","2":"UK","3":"private","4":"2.94260500"},{"1":"1974","2":"Japan","3":"public","4":"0.93590400"},{"1":"1974","2":"Japan","3":"private","4":"3.98334800"},{"1":"1974","2":"Norway","3":"public","4":"NA"},{"1":"1974","2":"Norway","3":"private","4":"NA"},{"1":"1974","2":"USA","3":"public","4":"0.50054130"},{"1":"1974","2":"USA","3":"private","4":"3.07213500"},{"1":"1975","2":"Germany","3":"public","4":"1.11553000"},{"1":"1975","2":"Germany","3":"private","4":"2.35061800"},{"1":"1975","2":"Spain","3":"public","4":"0.60172080"},{"1":"1975","2":"Spain","3":"private","4":"4.82602000"},{"1":"1975","2":"France","3":"public","4":"0.54505460"},{"1":"1975","2":"France","3":"private","4":"3.11972100"},{"1":"1975","2":"UK","3":"public","4":"1.00039000"},{"1":"1975","2":"UK","3":"private","4":"2.65191000"},{"1":"1975","2":"Japan","3":"public","4":"0.94407140"},{"1":"1975","2":"Japan","3":"private","4":"3.83241300"},{"1":"1975","2":"Norway","3":"public","4":"NA"},{"1":"1975","2":"Norway","3":"private","4":"NA"},{"1":"1975","2":"USA","3":"public","4":"0.52876290"},{"1":"1975","2":"USA","3":"private","4":"3.05713800"},{"1":"1976","2":"Germany","3":"public","4":"1.03391600"},{"1":"1976","2":"Germany","3":"private","4":"2.34154100"},{"1":"1976","2":"Spain","3":"public","4":"0.58072080"},{"1":"1976","2":"Spain","3":"private","4":"4.46011100"},{"1":"1976","2":"France","3":"public","4":"0.56132940"},{"1":"1976","2":"France","3":"private","4":"3.07791400"},{"1":"1976","2":"UK","3":"public","4":"0.91778720"},{"1":"1976","2":"UK","3":"private","4":"2.53695300"},{"1":"1976","2":"Japan","3":"public","4":"0.90228480"},{"1":"1976","2":"Japan","3":"private","4":"3.75402500"},{"1":"1976","2":"Norway","3":"public","4":"NA"},{"1":"1976","2":"Norway","3":"private","4":"NA"},{"1":"1976","2":"USA","3":"public","4":"0.48457710"},{"1":"1976","2":"USA","3":"private","4":"3.11111900"},{"1":"1977","2":"Germany","3":"public","4":"1.00515200"},{"1":"1977","2":"Germany","3":"private","4":"2.42124600"},{"1":"1977","2":"Spain","3":"public","4":"0.58558340"},{"1":"1977","2":"Spain","3":"private","4":"4.09745400"},{"1":"1977","2":"France","3":"public","4":"0.56742920"},{"1":"1977","2":"France","3":"private","4":"3.09873500"},{"1":"1977","2":"UK","3":"public","4":"0.86698500"},{"1":"1977","2":"UK","3":"private","4":"2.46727000"},{"1":"1977","2":"Japan","3":"public","4":"0.87971750"},{"1":"1977","2":"Japan","3":"private","4":"3.73654200"},{"1":"1977","2":"Norway","3":"public","4":"NA"},{"1":"1977","2":"Norway","3":"private","4":"NA"},{"1":"1977","2":"USA","3":"public","4":"0.47339750"},{"1":"1977","2":"USA","3":"private","4":"3.09601100"},{"1":"1978","2":"Germany","3":"public","4":"0.98957940"},{"1":"1978","2":"Germany","3":"private","4":"2.51713600"},{"1":"1978","2":"Spain","3":"public","4":"0.60401550"},{"1":"1978","2":"Spain","3":"private","4":"4.09927200"},{"1":"1978","2":"France","3":"public","4":"0.58002190"},{"1":"1978","2":"France","3":"private","4":"3.19822500"},{"1":"1978","2":"UK","3":"public","4":"0.88060180"},{"1":"1978","2":"UK","3":"private","4":"2.51401700"},{"1":"1978","2":"Japan","3":"public","4":"0.85960620"},{"1":"1978","2":"Japan","3":"private","4":"3.80149800"},{"1":"1978","2":"Norway","3":"public","4":"NA"},{"1":"1978","2":"Norway","3":"private","4":"NA"},{"1":"1978","2":"USA","3":"public","4":"0.47283040"},{"1":"1978","2":"USA","3":"private","4":"3.05202100"},{"1":"1979","2":"Germany","3":"public","4":"0.98895610"},{"1":"1979","2":"Germany","3":"private","4":"2.54721800"},{"1":"1979","2":"Spain","3":"public","4":"0.62116990"},{"1":"1979","2":"Spain","3":"private","4":"4.20329600"},{"1":"1979","2":"France","3":"public","4":"0.62412810"},{"1":"1979","2":"France","3":"private","4":"3.29799500"},{"1":"1979","2":"UK","3":"public","4":"0.95529160"},{"1":"1979","2":"UK","3":"private","4":"2.61835900"},{"1":"1979","2":"Japan","3":"public","4":"0.88377380"},{"1":"1979","2":"Japan","3":"private","4":"4.09438900"},{"1":"1979","2":"Norway","3":"public","4":"NA"},{"1":"1979","2":"Norway","3":"private","4":"NA"},{"1":"1979","2":"USA","3":"public","4":"0.51814040"},{"1":"1979","2":"USA","3":"private","4":"3.15254600"},{"1":"1980","2":"Germany","3":"public","4":"1.00823600"},{"1":"1980","2":"Germany","3":"private","4":"2.61920600"},{"1":"1980","2":"Spain","3":"public","4":"0.53458570"},{"1":"1980","2":"Spain","3":"private","4":"3.99841100"},{"1":"1980","2":"France","3":"public","4":"0.68589250"},{"1":"1980","2":"France","3":"private","4":"3.33094000"},{"1":"1980","2":"UK","3":"public","4":"1.02314000"},{"1":"1980","2":"UK","3":"private","4":"2.64447900"},{"1":"1980","2":"Japan","3":"public","4":"0.93260660"},{"1":"1980","2":"Japan","3":"private","4":"4.39773900"},{"1":"1980","2":"Norway","3":"public","4":"NA"},{"1":"1980","2":"Norway","3":"private","4":"NA"},{"1":"1980","2":"USA","3":"public","4":"0.61595070"},{"1":"1980","2":"USA","3":"private","4":"3.37214900"},{"1":"1981","2":"Germany","3":"public","4":"1.01775200"},{"1":"1981","2":"Germany","3":"private","4":"2.76126700"},{"1":"1981","2":"Spain","3":"public","4":"0.50242980"},{"1":"1981","2":"Spain","3":"private","4":"4.13716800"},{"1":"1981","2":"France","3":"public","4":"0.71390400"},{"1":"1981","2":"France","3":"private","4":"3.33190500"},{"1":"1981","2":"UK","3":"public","4":"1.06498500"},{"1":"1981","2":"UK","3":"private","4":"2.70175900"},{"1":"1981","2":"Japan","3":"public","4":"0.95314710"},{"1":"1981","2":"Japan","3":"private","4":"4.63044600"},{"1":"1981","2":"Norway","3":"public","4":"NA"},{"1":"1981","2":"Norway","3":"private","4":"NA"},{"1":"1981","2":"USA","3":"public","4":"0.63743420"},{"1":"1981","2":"USA","3":"private","4":"3.34848400"},{"1":"1982","2":"Germany","3":"public","4":"0.99023560"},{"1":"1982","2":"Germany","3":"private","4":"2.91660000"},{"1":"1982","2":"Spain","3":"public","4":"0.47899510"},{"1":"1982","2":"Spain","3":"private","4":"3.94095700"},{"1":"1982","2":"France","3":"public","4":"0.69431250"},{"1":"1982","2":"France","3":"private","4":"3.24717300"},{"1":"1982","2":"UK","3":"public","4":"1.00022900"},{"1":"1982","2":"UK","3":"private","4":"2.71630800"},{"1":"1982","2":"Japan","3":"public","4":"0.93725780"},{"1":"1982","2":"Japan","3":"private","4":"4.80174900"},{"1":"1982","2":"Norway","3":"public","4":"NA"},{"1":"1982","2":"Norway","3":"private","4":"NA"},{"1":"1982","2":"USA","3":"public","4":"0.63080690"},{"1":"1982","2":"USA","3":"private","4":"3.46066400"},{"1":"1983","2":"Germany","3":"public","4":"0.95076010"},{"1":"1983","2":"Germany","3":"private","4":"3.02614500"},{"1":"1983","2":"Spain","3":"public","4":"0.45290420"},{"1":"1983","2":"Spain","3":"private","4":"3.79241700"},{"1":"1983","2":"France","3":"public","4":"0.68896310"},{"1":"1983","2":"France","3":"private","4":"3.26189600"},{"1":"1983","2":"UK","3":"public","4":"0.92222340"},{"1":"1983","2":"UK","3":"private","4":"2.78102300"},{"1":"1983","2":"Japan","3":"public","4":"0.90197690"},{"1":"1983","2":"Japan","3":"private","4":"4.94990800"},{"1":"1983","2":"Norway","3":"public","4":"NA"},{"1":"1983","2":"Norway","3":"private","4":"NA"},{"1":"1983","2":"USA","3":"public","4":"0.56790170"},{"1":"1983","2":"USA","3":"private","4":"3.45857200"},{"1":"1984","2":"Germany","3":"public","4":"0.92080250"},{"1":"1984","2":"Germany","3":"private","4":"3.10124400"},{"1":"1984","2":"Spain","3":"public","4":"0.42230340"},{"1":"1984","2":"Spain","3":"private","4":"3.68297600"},{"1":"1984","2":"France","3":"public","4":"0.67267530"},{"1":"1984","2":"France","3":"private","4":"3.25881500"},{"1":"1984","2":"UK","3":"public","4":"0.89471820"},{"1":"1984","2":"UK","3":"private","4":"2.94416300"},{"1":"1984","2":"Japan","3":"public","4":"0.84567620"},{"1":"1984","2":"Japan","3":"private","4":"4.94283300"},{"1":"1984","2":"Norway","3":"public","4":"NA"},{"1":"1984","2":"Norway","3":"private","4":"NA"},{"1":"1984","2":"USA","3":"public","4":"0.47977030"},{"1":"1984","2":"USA","3":"private","4":"3.30949500"},{"1":"1985","2":"Germany","3":"public","4":"0.89961330"},{"1":"1985","2":"Germany","3":"private","4":"3.20088000"},{"1":"1985","2":"Spain","3":"public","4":"0.39179010"},{"1":"1985","2":"Spain","3":"private","4":"3.73805500"},{"1":"1985","2":"France","3":"public","4":"0.63653300"},{"1":"1985","2":"France","3":"private","4":"3.21243500"},{"1":"1985","2":"UK","3":"public","4":"0.86642760"},{"1":"1985","2":"UK","3":"private","4":"3.00131300"},{"1":"1985","2":"Japan","3":"public","4":"0.80189690"},{"1":"1985","2":"Japan","3":"private","4":"4.92224600"},{"1":"1985","2":"Norway","3":"public","4":"NA"},{"1":"1985","2":"Norway","3":"private","4":"NA"},{"1":"1985","2":"USA","3":"public","4":"0.43232440"},{"1":"1985","2":"USA","3":"private","4":"3.41051600"},{"1":"1986","2":"Germany","3":"public","4":"0.87658910"},{"1":"1986","2":"Germany","3":"private","4":"3.27052500"},{"1":"1986","2":"Spain","3":"public","4":"0.34193300"},{"1":"1986","2":"Spain","3":"private","4":"3.75567400"},{"1":"1986","2":"France","3":"public","4":"0.58655950"},{"1":"1986","2":"France","3":"private","4":"3.21155000"},{"1":"1986","2":"UK","3":"public","4":"0.85877390"},{"1":"1986","2":"UK","3":"private","4":"3.25052500"},{"1":"1986","2":"Japan","3":"public","4":"0.80112800"},{"1":"1986","2":"Japan","3":"private","4":"5.37287800"},{"1":"1986","2":"Norway","3":"public","4":"NA"},{"1":"1986","2":"Norway","3":"private","4":"NA"},{"1":"1986","2":"USA","3":"public","4":"0.40007330"},{"1":"1986","2":"USA","3":"private","4":"3.63620100"},{"1":"1987","2":"Germany","3":"public","4":"0.87896650"},{"1":"1987","2":"Germany","3":"private","4":"3.40130300"},{"1":"1987","2":"Spain","3":"public","4":"0.32806510"},{"1":"1987","2":"Spain","3":"private","4":"3.94012500"},{"1":"1987","2":"France","3":"public","4":"0.56807450"},{"1":"1987","2":"France","3":"private","4":"3.25252200"},{"1":"1987","2":"UK","3":"public","4":"0.82096210"},{"1":"1987","2":"UK","3":"private","4":"3.45741900"},{"1":"1987","2":"Japan","3":"public","4":"0.90052330"},{"1":"1987","2":"Japan","3":"private","4":"6.23114400"},{"1":"1987","2":"Norway","3":"public","4":"NA"},{"1":"1987","2":"Norway","3":"private","4":"NA"},{"1":"1987","2":"USA","3":"public","4":"0.36718910"},{"1":"1987","2":"USA","3":"private","4":"3.67931800"},{"1":"1988","2":"Germany","3":"public","4":"0.84785230"},{"1":"1988","2":"Germany","3":"private","4":"3.40849400"},{"1":"1988","2":"Spain","3":"public","4":"0.33909660"},{"1":"1988","2":"Spain","3":"private","4":"4.23159000"},{"1":"1988","2":"France","3":"public","4":"0.54980850"},{"1":"1988","2":"France","3":"private","4":"3.22252400"},{"1":"1988","2":"UK","3":"public","4":"0.84781340"},{"1":"1988","2":"UK","3":"private","4":"3.71645900"},{"1":"1988","2":"Japan","3":"public","4":"1.01407500"},{"1":"1988","2":"Japan","3":"private","4":"6.68570100"},{"1":"1988","2":"Norway","3":"public","4":"NA"},{"1":"1988","2":"Norway","3":"private","4":"NA"},{"1":"1988","2":"USA","3":"public","4":"0.33283060"},{"1":"1988","2":"USA","3":"private","4":"3.64715100"},{"1":"1989","2":"Germany","3":"public","4":"0.83398810"},{"1":"1989","2":"Germany","3":"private","4":"3.40153300"},{"1":"1989","2":"Spain","3":"public","4":"0.33370330"},{"1":"1989","2":"Spain","3":"private","4":"4.43654300"},{"1":"1989","2":"France","3":"public","4":"0.53706810"},{"1":"1989","2":"France","3":"private","4":"3.31351000"},{"1":"1989","2":"UK","3":"public","4":"0.83403580"},{"1":"1989","2":"UK","3":"private","4":"3.89832400"},{"1":"1989","2":"Japan","3":"public","4":"1.14424000"},{"1":"1989","2":"Japan","3":"private","4":"7.03530100"},{"1":"1989","2":"Norway","3":"public","4":"NA"},{"1":"1989","2":"Norway","3":"private","4":"NA"},{"1":"1989","2":"USA","3":"public","4":"0.31029870"},{"1":"1989","2":"USA","3":"private","4":"3.75719500"},{"1":"1990","2":"Germany","3":"public","4":"0.85950360"},{"1":"1990","2":"Germany","3":"private","4":"3.42541000"},{"1":"1990","2":"Spain","3":"public","4":"0.32136410"},{"1":"1990","2":"Spain","3":"private","4":"4.46252800"},{"1":"1990","2":"France","3":"public","4":"0.52897060"},{"1":"1990","2":"France","3":"private","4":"3.34437500"},{"1":"1990","2":"UK","3":"public","4":"0.72308610"},{"1":"1990","2":"UK","3":"private","4":"3.81737000"},{"1":"1990","2":"Japan","3":"public","4":"1.25096500"},{"1":"1990","2":"Japan","3":"private","4":"7.11927500"},{"1":"1990","2":"Norway","3":"public","4":"NA"},{"1":"1990","2":"Norway","3":"private","4":"NA"},{"1":"1990","2":"USA","3":"public","4":"0.28799930"},{"1":"1990","2":"USA","3":"private","4":"3.76359200"},{"1":"1991","2":"Germany","3":"public","4":"0.77451240"},{"1":"1991","2":"Germany","3":"private","4":"3.11878000"},{"1":"1991","2":"Spain","3":"public","4":"0.31747390"},{"1":"1991","2":"Spain","3":"private","4":"4.61497100"},{"1":"1991","2":"France","3":"public","4":"0.52113820"},{"1":"1991","2":"France","3":"private","4":"3.33715500"},{"1":"1991","2":"UK","3":"public","4":"0.61816970"},{"1":"1991","2":"UK","3":"private","4":"3.77520800"},{"1":"1991","2":"Japan","3":"public","4":"1.27453600"},{"1":"1991","2":"Japan","3":"private","4":"6.80129000"},{"1":"1991","2":"Norway","3":"public","4":"NA"},{"1":"1991","2":"Norway","3":"private","4":"NA"},{"1":"1991","2":"USA","3":"public","4":"0.25755490"},{"1":"1991","2":"USA","3":"private","4":"3.82990200"},{"1":"1992","2":"Germany","3":"public","4":"0.72227670"},{"1":"1992","2":"Germany","3":"private","4":"3.14306900"},{"1":"1992","2":"Spain","3":"public","4":"0.29359570"},{"1":"1992","2":"Spain","3":"private","4":"4.35542200"},{"1":"1992","2":"France","3":"public","4":"0.49361090"},{"1":"1992","2":"France","3":"private","4":"3.27376300"},{"1":"1992","2":"UK","3":"public","4":"0.49903240"},{"1":"1992","2":"UK","3":"private","4":"3.80056000"},{"1":"1992","2":"Japan","3":"public","4":"1.26159400"},{"1":"1992","2":"Japan","3":"private","4":"6.42690600"},{"1":"1992","2":"Norway","3":"public","4":"NA"},{"1":"1992","2":"Norway","3":"private","4":"NA"},{"1":"1992","2":"USA","3":"public","4":"0.19159750"},{"1":"1992","2":"USA","3":"private","4":"3.81864500"},{"1":"1993","2":"Germany","3":"public","4":"0.68279520"},{"1":"1993","2":"Germany","3":"private","4":"3.27884200"},{"1":"1993","2":"Spain","3":"public","4":"0.25903530"},{"1":"1993","2":"Spain","3":"private","4":"4.44789700"},{"1":"1993","2":"France","3":"public","4":"0.44041430"},{"1":"1993","2":"France","3":"private","4":"3.31177700"},{"1":"1993","2":"UK","3":"public","4":"0.37393440"},{"1":"1993","2":"UK","3":"private","4":"3.91697000"},{"1":"1993","2":"Japan","3":"public","4":"1.25223900"},{"1":"1993","2":"Japan","3":"private","4":"6.26480900"},{"1":"1993","2":"Norway","3":"public","4":"NA"},{"1":"1993","2":"Norway","3":"private","4":"NA"},{"1":"1993","2":"USA","3":"public","4":"0.13233770"},{"1":"1993","2":"USA","3":"private","4":"3.83553700"},{"1":"1994","2":"Germany","3":"public","4":"0.65047320"},{"1":"1994","2":"Germany","3":"private","4":"3.31622200"},{"1":"1994","2":"Spain","3":"public","4":"0.21906260"},{"1":"1994","2":"Spain","3":"private","4":"4.48713400"},{"1":"1994","2":"France","3":"public","4":"0.38447300"},{"1":"1994","2":"France","3":"private","4":"3.26547100"},{"1":"1994","2":"UK","3":"public","4":"0.31977080"},{"1":"1994","2":"UK","3":"private","4":"3.88332900"},{"1":"1994","2":"Japan","3":"public","4":"1.24683700"},{"1":"1994","2":"Japan","3":"private","4":"6.21090100"},{"1":"1994","2":"Norway","3":"public","4":"NA"},{"1":"1994","2":"Norway","3":"private","4":"NA"},{"1":"1994","2":"USA","3":"public","4":"0.10453160"},{"1":"1994","2":"USA","3":"private","4":"3.76956300"},{"1":"1995","2":"Germany","3":"public","4":"0.57799065"},{"1":"1995","2":"Germany","3":"private","4":"3.38542819"},{"1":"1995","2":"Spain","3":"public","4":"0.31819066"},{"1":"1995","2":"Spain","3":"private","4":"4.61381626"},{"1":"1995","2":"France","3":"public","4":"0.34096268"},{"1":"1995","2":"France","3":"private","4":"3.17394781"},{"1":"1995","2":"UK","3":"public","4":"0.18621574"},{"1":"1995","2":"UK","3":"private","4":"4.26432228"},{"1":"1995","2":"Japan","3":"public","4":"1.11272323"},{"1":"1995","2":"Japan","3":"private","4":"6.16544008"},{"1":"1995","2":"Norway","3":"public","4":"1.06207967"},{"1":"1995","2":"Norway","3":"private","4":"2.50039911"},{"1":"1995","2":"USA","3":"public","4":"-0.01015096"},{"1":"1995","2":"USA","3":"private","4":"3.89195275"},{"1":"1996","2":"Germany","3":"public","4":"0.49221757"},{"1":"1996","2":"Germany","3":"private","4":"3.49259400"},{"1":"1996","2":"Spain","3":"public","4":"0.27088898"},{"1":"1996","2":"Spain","3":"private","4":"4.67430592"},{"1":"1996","2":"France","3":"public","4":"0.28910396"},{"1":"1996","2":"France","3":"private","4":"3.29729247"},{"1":"1996","2":"UK","3":"public","4":"0.04883918"},{"1":"1996","2":"UK","3":"private","4":"4.39618111"},{"1":"1996","2":"Japan","3":"public","4":"1.06029630"},{"1":"1996","2":"Japan","3":"private","4":"6.08764267"},{"1":"1996","2":"Norway","3":"public","4":"1.10075939"},{"1":"1996","2":"Norway","3":"private","4":"2.43442512"},{"1":"1996","2":"USA","3":"public","4":"0.01051010"},{"1":"1996","2":"USA","3":"private","4":"3.96823049"},{"1":"1997","2":"Germany","3":"public","4":"0.45957553"},{"1":"1997","2":"Germany","3":"private","4":"3.59615254"},{"1":"1997","2":"Spain","3":"public","4":"0.23950605"},{"1":"1997","2":"Spain","3":"private","4":"4.72466707"},{"1":"1997","2":"France","3":"public","4":"0.25134310"},{"1":"1997","2":"France","3":"private","4":"3.38326144"},{"1":"1997","2":"UK","3":"public","4":"0.03361297"},{"1":"1997","2":"UK","3":"private","4":"4.51665497"},{"1":"1997","2":"Japan","3":"public","4":"1.03373075"},{"1":"1997","2":"Japan","3":"private","4":"6.00851202"},{"1":"1997","2":"Norway","3":"public","4":"1.16897571"},{"1":"1997","2":"Norway","3":"private","4":"2.39036202"},{"1":"1997","2":"USA","3":"public","4":"0.06276285"},{"1":"1997","2":"USA","3":"private","4":"4.06916189"},{"1":"1998","2":"Germany","3":"public","4":"0.42294434"},{"1":"1998","2":"Germany","3":"private","4":"3.69517040"},{"1":"1998","2":"Spain","3":"public","4":"0.24446492"},{"1":"1998","2":"Spain","3":"private","4":"4.85522270"},{"1":"1998","2":"France","3":"public","4":"0.22945850"},{"1":"1998","2":"France","3":"private","4":"3.39718676"},{"1":"1998","2":"UK","3":"public","4":"0.01145423"},{"1":"1998","2":"UK","3":"private","4":"4.78151846"},{"1":"1998","2":"Japan","3":"public","4":"1.03942382"},{"1":"1998","2":"Japan","3":"private","4":"6.20990801"},{"1":"1998","2":"Norway","3":"public","4":"1.29522109"},{"1":"1998","2":"Norway","3":"private","4":"2.48779249"},{"1":"1998","2":"USA","3":"public","4":"0.12571324"},{"1":"1998","2":"USA","3":"private","4":"4.26582670"},{"1":"1999","2":"Germany","3":"public","4":"0.39200506"},{"1":"1999","2":"Germany","3":"private","4":"3.74854565"},{"1":"1999","2":"Spain","3":"public","4":"0.29453880"},{"1":"1999","2":"Spain","3":"private","4":"5.13881063"},{"1":"1999","2":"France","3":"public","4":"0.27526882"},{"1":"1999","2":"France","3":"private","4":"3.56644678"},{"1":"1999","2":"UK","3":"public","4":"0.01666648"},{"1":"1999","2":"UK","3":"private","4":"4.92944860"},{"1":"1999","2":"Japan","3":"public","4":"0.99654120"},{"1":"1999","2":"Japan","3":"private","4":"6.38285017"},{"1":"1999","2":"Norway","3":"public","4":"1.30180120"},{"1":"1999","2":"Norway","3":"private","4":"2.39479876"},{"1":"1999","2":"USA","3":"public","4":"0.19284114"},{"1":"1999","2":"USA","3":"private","4":"4.48406172"},{"1":"2000","2":"Germany","3":"public","4":"0.37500408"},{"1":"2000","2":"Germany","3":"private","4":"3.75756955"},{"1":"2000","2":"Spain","3":"public","4":"0.36201853"},{"1":"2000","2":"Spain","3":"private","4":"5.31504107"},{"1":"2000","2":"France","3":"public","4":"0.32539812"},{"1":"2000","2":"France","3":"private","4":"3.72049379"},{"1":"2000","2":"UK","3":"public","4":"0.04167610"},{"1":"2000","2":"UK","3":"private","4":"5.14463711"},{"1":"2000","2":"Japan","3":"public","4":"0.92694992"},{"1":"2000","2":"Japan","3":"private","4":"6.37162733"},{"1":"2000","2":"Norway","3":"public","4":"1.26671052"},{"1":"2000","2":"Norway","3":"private","4":"2.12352371"},{"1":"2000","2":"USA","3":"public","4":"0.24440868"},{"1":"2000","2":"USA","3":"private","4":"4.46062326"},{"1":"2001","2":"Germany","3":"public","4":"0.34209570"},{"1":"2001","2":"Germany","3":"private","4":"3.75923133"},{"1":"2001","2":"Spain","3":"public","4":"0.41110042"},{"1":"2001","2":"Spain","3":"private","4":"5.54442453"},{"1":"2001","2":"France","3":"public","4":"0.32244271"},{"1":"2001","2":"France","3":"private","4":"3.77879953"},{"1":"2001","2":"UK","3":"public","4":"0.05643485"},{"1":"2001","2":"UK","3":"private","4":"5.12705517"},{"1":"2001","2":"Japan","3":"public","4":"0.86239475"},{"1":"2001","2":"Japan","3":"private","4":"6.29808521"},{"1":"2001","2":"Norway","3":"public","4":"1.45966637"},{"1":"2001","2":"Norway","3":"private","4":"2.14304161"},{"1":"2001","2":"USA","3":"public","4":"0.27004132"},{"1":"2001","2":"USA","3":"private","4":"4.41708088"},{"1":"2002","2":"Germany","3":"public","4":"0.30023211"},{"1":"2002","2":"Germany","3":"private","4":"3.78331089"},{"1":"2002","2":"Spain","3":"public","4":"0.45536190"},{"1":"2002","2":"Spain","3":"private","4":"5.81634092"},{"1":"2002","2":"France","3":"public","4":"0.31642923"},{"1":"2002","2":"France","3":"private","4":"3.89358497"},{"1":"2002","2":"UK","3":"public","4":"0.04788728"},{"1":"2002","2":"UK","3":"private","4":"5.14940119"},{"1":"2002","2":"Japan","3":"public","4":"0.77602887"},{"1":"2002","2":"Japan","3":"private","4":"6.25490570"},{"1":"2002","2":"Norway","3":"public","4":"1.55597591"},{"1":"2002","2":"Norway","3":"private","4":"2.22594142"},{"1":"2002","2":"USA","3":"public","4":"0.26549011"},{"1":"2002","2":"USA","3":"private","4":"4.32110071"},{"1":"2003","2":"Germany","3":"public","4":"0.25070733"},{"1":"2003","2":"Germany","3":"private","4":"3.81412005"},{"1":"2003","2":"Spain","3":"public","4":"0.50729346"},{"1":"2003","2":"Spain","3":"private","4":"6.23855925"},{"1":"2003","2":"France","3":"public","4":"0.32774720"},{"1":"2003","2":"France","3":"private","4":"4.13774538"},{"1":"2003","2":"UK","3":"public","4":"0.03161745"},{"1":"2003","2":"UK","3":"private","4":"5.30549908"},{"1":"2003","2":"Japan","3":"public","4":"0.69695836"},{"1":"2003","2":"Japan","3":"private","4":"6.15494251"},{"1":"2003","2":"Norway","3":"public","4":"1.58633137"},{"1":"2003","2":"Norway","3":"private","4":"2.22687936"},{"1":"2003","2":"USA","3":"public","4":"0.25429934"},{"1":"2003","2":"USA","3":"private","4":"4.38494921"},{"1":"2004","2":"Germany","3":"public","4":"0.20240971"},{"1":"2004","2":"Germany","3":"private","4":"3.81001782"},{"1":"2004","2":"Spain","3":"public","4":"0.57735318"},{"1":"2004","2":"Spain","3":"private","4":"6.85902119"},{"1":"2004","2":"France","3":"public","4":"0.37041435"},{"1":"2004","2":"France","3":"private","4":"4.46653366"},{"1":"2004","2":"UK","3":"public","4":"0.03058806"},{"1":"2004","2":"UK","3":"private","4":"5.45379496"},{"1":"2004","2":"Japan","3":"public","4":"0.64557618"},{"1":"2004","2":"Japan","3":"private","4":"6.02907419"},{"1":"2004","2":"Norway","3":"public","4":"1.66688848"},{"1":"2004","2":"Norway","3":"private","4":"2.18519282"},{"1":"2004","2":"USA","3":"public","4":"0.22911941"},{"1":"2004","2":"USA","3":"private","4":"4.67670727"},{"1":"2005","2":"Germany","3":"public","4":"0.16731116"},{"1":"2005","2":"Germany","3":"private","4":"3.89775491"},{"1":"2005","2":"Spain","3":"public","4":"0.66154492"},{"1":"2005","2":"Spain","3":"private","4":"7.37761307"},{"1":"2005","2":"France","3":"public","4":"0.44930500"},{"1":"2005","2":"France","3":"private","4":"4.87851620"},{"1":"2005","2":"UK","3":"public","4":"0.04279286"},{"1":"2005","2":"UK","3":"private","4":"5.62839127"},{"1":"2005","2":"Japan","3":"public","4":"0.63917983"},{"1":"2005","2":"Japan","3":"private","4":"6.09258747"},{"1":"2005","2":"Norway","3":"public","4":"1.74952257"},{"1":"2005","2":"Norway","3":"private","4":"2.13924670"},{"1":"2005","2":"USA","3":"public","4":"0.22655702"},{"1":"2005","2":"USA","3":"private","4":"4.92949677"},{"1":"2006","2":"Germany","3":"public","4":"0.15743059"},{"1":"2006","2":"Germany","3":"private","4":"3.82032919"},{"1":"2006","2":"Spain","3":"public","4":"0.75073624"},{"1":"2006","2":"Spain","3":"private","4":"7.70710659"},{"1":"2006","2":"France","3":"public","4":"0.54943728"},{"1":"2006","2":"France","3":"private","4":"5.21692133"},{"1":"2006","2":"UK","3":"public","4":"0.06440135"},{"1":"2006","2":"UK","3":"private","4":"5.74070263"},{"1":"2006","2":"Japan","3":"public","4":"0.66539401"},{"1":"2006","2":"Japan","3":"private","4":"6.20814419"},{"1":"2006","2":"Norway","3":"public","4":"1.93126416"},{"1":"2006","2":"Norway","3":"private","4":"2.16681051"},{"1":"2006","2":"USA","3":"public","4":"0.27519721"},{"1":"2006","2":"USA","3":"private","4":"5.02275944"},{"1":"2007","2":"Germany","3":"public","4":"0.18420206"},{"1":"2007","2":"Germany","3":"private","4":"3.82586408"},{"1":"2007","2":"Spain","3":"public","4":"0.83520442"},{"1":"2007","2":"Spain","3":"private","4":"7.99167585"},{"1":"2007","2":"France","3":"public","4":"0.62550110"},{"1":"2007","2":"France","3":"private","4":"5.41278172"},{"1":"2007","2":"UK","3":"public","4":"0.05150459"},{"1":"2007","2":"UK","3":"private","4":"5.83866549"},{"1":"2007","2":"Japan","3":"public","4":"0.68938506"},{"1":"2007","2":"Japan","3":"private","4":"6.16001892"},{"1":"2007","2":"Norway","3":"public","4":"2.08936715"},{"1":"2007","2":"Norway","3":"private","4":"2.27437305"},{"1":"2007","2":"USA","3":"public","4":"0.31006292"},{"1":"2007","2":"USA","3":"private","4":"5.08544111"},{"1":"2008","2":"Germany","3":"public","4":"0.19910918"},{"1":"2008","2":"Germany","3":"private","4":"3.89389825"},{"1":"2008","2":"Spain","3":"public","4":"0.87531859"},{"1":"2008","2":"Spain","3":"private","4":"8.03427410"},{"1":"2008","2":"France","3":"public","4":"0.57730550"},{"1":"2008","2":"France","3":"private","4":"5.31553650"},{"1":"2008","2":"UK","3":"public","4":"-0.02833927"},{"1":"2008","2":"UK","3":"private","4":"5.35299587"},{"1":"2008","2":"Japan","3":"public","4":"0.64253807"},{"1":"2008","2":"Japan","3":"private","4":"6.12522364"},{"1":"2008","2":"Norway","3":"public","4":"1.97143221"},{"1":"2008","2":"Norway","3":"private","4":"2.17047215"},{"1":"2008","2":"USA","3":"public","4":"0.21646091"},{"1":"2008","2":"USA","3":"private","4":"4.72309971"},{"1":"2009","2":"Germany","3":"public","4":"0.19955969"},{"1":"2009","2":"Germany","3":"private","4":"4.13252258"},{"1":"2009","2":"Spain","3":"public","4":"0.81510937"},{"1":"2009","2":"Spain","3":"private","4":"7.73118114"},{"1":"2009","2":"France","3":"public","4":"0.48994470"},{"1":"2009","2":"France","3":"private","4":"5.34728575"},{"1":"2009","2":"UK","3":"public","4":"-0.13180329"},{"1":"2009","2":"UK","3":"private","4":"5.02109194"},{"1":"2009","2":"Japan","3":"public","4":"0.53687960"},{"1":"2009","2":"Japan","3":"private","4":"6.45085907"},{"1":"2009","2":"Norway","3":"public","4":"2.27953839"},{"1":"2009","2":"Norway","3":"private","4":"2.44265008"},{"1":"2009","2":"USA","3":"public","4":"0.02929429"},{"1":"2009","2":"USA","3":"private","4":"4.46910286"},{"1":"2010","2":"Germany","3":"public","4":"0.17325440"},{"1":"2010","2":"Germany","3":"private","4":"4.09632206"},{"1":"2010","2":"Spain","3":"public","4":"0.73713875"},{"1":"2010","2":"Spain","3":"private","4":"7.69212484"},{"1":"2010","2":"France","3":"public","4":"0.45627671"},{"1":"2010","2":"France","3":"private","4":"5.45563507"},{"1":"2010","2":"UK","3":"public","4":"-0.21362586"},{"1":"2010","2":"UK","3":"private","4":"5.47909069"},{"1":"2010","2":"Japan","3":"public","4":"0.38551483"},{"1":"2010","2":"Japan","3":"private","4":"6.27157354"},{"1":"2010","2":"Norway","3":"public","4":"2.36142063"},{"1":"2010","2":"Norway","3":"private","4":"2.39295197"},{"1":"2010","2":"USA","3":"public","4":"-0.10685690"},{"1":"2010","2":"USA","3":"private","4":"4.40267754"},{"1":"2011","2":"Germany","3":"public","4":"0.14252852"},{"1":"2011","2":"Germany","3":"private","4":"4.07134056"},{"1":"2011","2":"Spain","3":"public","4":"0.69439161"},{"1":"2011","2":"Spain","3":"private","4":"7.61070728"},{"1":"2011","2":"France","3":"public","4":"0.43244216"},{"1":"2011","2":"France","3":"private","4":"5.58247519"},{"1":"2011","2":"UK","3":"public","4":"-0.32206973"},{"1":"2011","2":"UK","3":"private","4":"5.48358011"},{"1":"2011","2":"Japan","3":"public","4":"0.25148743"},{"1":"2011","2":"Japan","3":"private","4":"6.21990204"},{"1":"2011","2":"Norway","3":"public","4":"2.37210631"},{"1":"2011","2":"Norway","3":"private","4":"2.35662317"},{"1":"2011","2":"USA","3":"public","4":"-0.19141020"},{"1":"2011","2":"USA","3":"private","4":"4.36232710"},{"1":"2012","2":"Germany","3":"public","4":"0.14329356"},{"1":"2012","2":"Germany","3":"private","4":"4.13491297"},{"1":"2012","2":"Spain","3":"public","4":"0.61073655"},{"1":"2012","2":"Spain","3":"private","4":"7.30309343"},{"1":"2012","2":"France","3":"public","4":"0.36296016"},{"1":"2012","2":"France","3":"private","4":"5.65519810"},{"1":"2012","2":"UK","3":"public","4":"-0.43769264"},{"1":"2012","2":"UK","3":"private","4":"5.70386553"},{"1":"2012","2":"Japan","3":"public","4":"0.15417218"},{"1":"2012","2":"Japan","3":"private","4":"6.19455433"},{"1":"2012","2":"Norway","3":"public","4":"2.42027330"},{"1":"2012","2":"Norway","3":"private","4":"2.39550424"},{"1":"2012","2":"USA","3":"public","4":"-0.23970124"},{"1":"2012","2":"USA","3":"private","4":"4.33918047"},{"1":"2013","2":"Germany","3":"public","4":"0.15716285"},{"1":"2013","2":"Germany","3":"private","4":"4.22647333"},{"1":"2013","2":"Spain","3":"public","4":"0.50614172"},{"1":"2013","2":"Spain","3":"private","4":"7.11375475"},{"1":"2013","2":"France","3":"public","4":"0.30373242"},{"1":"2013","2":"France","3":"private","4":"5.63561010"},{"1":"2013","2":"UK","3":"public","4":"-0.43486899"},{"1":"2013","2":"UK","3":"private","4":"5.64698267"},{"1":"2013","2":"Japan","3":"public","4":"0.14775753"},{"1":"2013","2":"Japan","3":"private","4":"6.23983622"},{"1":"2013","2":"Norway","3":"public","4":"2.73042965"},{"1":"2013","2":"Norway","3":"private","4":"2.49103975"},{"1":"2013","2":"USA","3":"public","4":"-0.26922482"},{"1":"2013","2":"USA","3":"private","4":"4.67856312"},{"1":"2014","2":"Germany","3":"public","4":"0.15420237"},{"1":"2014","2":"Germany","3":"private","4":"4.25568342"},{"1":"2014","2":"Spain","3":"public","4":"0.36197579"},{"1":"2014","2":"Spain","3":"private","4":"7.03782177"},{"1":"2014","2":"France","3":"public","4":"0.23241447"},{"1":"2014","2":"France","3":"private","4":"5.58263063"},{"1":"2014","2":"UK","3":"public","4":"-0.47626394"},{"1":"2014","2":"UK","3":"private","4":"5.84947300"},{"1":"2014","2":"Japan","3":"public","4":"0.16963848"},{"1":"2014","2":"Japan","3":"private","4":"6.27579165"},{"1":"2014","2":"Norway","3":"public","4":"3.16365790"},{"1":"2014","2":"Norway","3":"private","4":"2.52795577"},{"1":"2014","2":"USA","3":"public","4":"-0.28567502"},{"1":"2014","2":"USA","3":"private","4":"4.90818501"},{"1":"2015","2":"Germany","3":"public","4":"0.17284682"},{"1":"2015","2":"Germany","3":"private","4":"4.31216145"},{"1":"2015","2":"Spain","3":"public","4":"0.24259460"},{"1":"2015","2":"Spain","3":"private","4":"6.83339596"},{"1":"2015","2":"France","3":"public","4":"0.14260918"},{"1":"2015","2":"France","3":"private","4":"5.53393793"},{"1":"2015","2":"UK","3":"public","4":"-0.53374809"},{"1":"2015","2":"UK","3":"private","4":"6.10138321"},{"1":"2015","2":"Japan","3":"public","4":"0.13765885"},{"1":"2015","2":"Japan","3":"private","4":"6.14643002"},{"1":"2015","2":"Norway","3":"public","4":"3.69533944"},{"1":"2015","2":"Norway","3":"private","4":"2.71160340"},{"1":"2015","2":"USA","3":"public","4":"-0.30884099"},{"1":"2015","2":"USA","3":"private","4":"5.01647139"},{"1":"2016","2":"Germany","3":"public","4":"0.20746191"},{"1":"2016","2":"Germany","3":"private","4":"4.35910082"},{"1":"2016","2":"Spain","3":"public","4":"0.21936896"},{"1":"2016","2":"Spain","3":"private","4":"6.79027700"},{"1":"2016","2":"France","3":"public","4":"0.11088289"},{"1":"2016","2":"France","3":"private","4":"5.64702511"},{"1":"2016","2":"UK","3":"public","4":"-0.58235788"},{"1":"2016","2":"UK","3":"private","4":"6.25625706"},{"1":"2016","2":"Japan","3":"public","4":"0.08187253"},{"1":"2016","2":"Japan","3":"private","4":"6.16540432"},{"1":"2016","2":"Norway","3":"public","4":"3.99441552"},{"1":"2016","2":"Norway","3":"private","4":"2.94746208"},{"1":"2016","2":"USA","3":"public","4":"-0.32733789"},{"1":"2016","2":"USA","3":"private","4":"5.17854071"},{"1":"2017","2":"Germany","3":"public","4":"0.24677505"},{"1":"2017","2":"Germany","3":"private","4":"4.41945601"},{"1":"2017","2":"Spain","3":"public","4":"0.20452128"},{"1":"2017","2":"Spain","3":"private","4":"6.68877363"},{"1":"2017","2":"France","3":"public","4":"0.12046999"},{"1":"2017","2":"France","3":"private","4":"5.74060869"},{"1":"2017","2":"UK","3":"public","4":"-0.58932400"},{"1":"2017","2":"UK","3":"private","4":"6.30460501"},{"1":"2017","2":"Japan","3":"public","4":"0.06974822"},{"1":"2017","2":"Japan","3":"private","4":"6.16909647"},{"1":"2017","2":"Norway","3":"public","4":"3.99523973"},{"1":"2017","2":"Norway","3":"private","4":"1.54199588"},{"1":"2017","2":"USA","3":"public","4":"-0.31652460"},{"1":"2017","2":"USA","3":"private","4":"5.39461040"},{"1":"2018","2":"Germany","3":"public","4":"0.30167750"},{"1":"2018","2":"Germany","3":"private","4":"4.51327610"},{"1":"2018","2":"Spain","3":"public","4":"0.20543142"},{"1":"2018","2":"Spain","3":"private","4":"6.61778498"},{"1":"2018","2":"France","3":"public","4":"0.15065138"},{"1":"2018","2":"France","3":"private","4":"5.80343437"},{"1":"2018","2":"UK","3":"public","4":"-0.53749311"},{"1":"2018","2":"UK","3":"private","4":"6.20427513"},{"1":"2018","2":"Japan","3":"public","4":"0.07431349"},{"1":"2018","2":"Japan","3":"private","4":"6.19537258"},{"1":"2018","2":"Norway","3":"public","4":"3.91121030"},{"1":"2018","2":"Norway","3":"private","4":"0.16930218"},{"1":"2018","2":"USA","3":"public","4":"-0.31464568"},{"1":"2018","2":"USA","3":"private","4":"5.40713930"},{"1":"2019","2":"Germany","3":"public","4":"0.36287290"},{"1":"2019","2":"Germany","3":"private","4":"4.69996405"},{"1":"2019","2":"Spain","3":"public","4":"0.20321131"},{"1":"2019","2":"Spain","3":"private","4":"6.64163542"},{"1":"2019","2":"France","3":"public","4":"0.16657437"},{"1":"2019","2":"France","3":"private","4":"5.99754143"},{"1":"2019","2":"UK","3":"public","4":"-0.55601621"},{"1":"2019","2":"UK","3":"private","4":"6.28413439"},{"1":"2019","2":"Japan","3":"public","4":"0.07381691"},{"1":"2019","2":"Japan","3":"private","4":"6.22894049"},{"1":"2019","2":"Norway","3":"public","4":"4.43813562"},{"1":"2019","2":"Norway","3":"private","4":"0.19179313"},{"1":"2019","2":"USA","3":"public","4":"-0.32255229"},{"1":"2019","2":"USA","3":"private","4":"5.60368204"},{"1":"2020","2":"Germany","3":"public","4":"0.18025590"},{"1":"2020","2":"Germany","3":"private","4":"5.01845884"},{"1":"2020","2":"Spain","3":"public","4":"-0.16059151"},{"1":"2020","2":"Spain","3":"private","4":"7.03459406"},{"1":"2020","2":"France","3":"public","4":"-0.12791239"},{"1":"2020","2":"France","3":"private","4":"6.32676029"},{"1":"2020","2":"UK","3":"public","4":"-1.05782545"},{"1":"2020","2":"UK","3":"private","4":"6.81865549"},{"1":"2020","2":"Japan","3":"public","4":"-0.33760664"},{"1":"2020","2":"Japan","3":"private","4":"6.67509604"},{"1":"2020","2":"Norway","3":"public","4":"4.97657347"},{"1":"2020","2":"Norway","3":"private","4":"0.32779658"},{"1":"2020","2":"USA","3":"public","4":"-0.60250711"},{"1":"2020","2":"USA","3":"private","4":"5.92150354"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---

#### Step 3. Final Step


```r
df_f8 %>% 
  select(year, Germany_public = Germany, Germany_private = 'Germany (private)', 
         Spain_public = Spain, Spain_private = 'Spain (private)', 
         France_public = France, France_private = 'France (private)', 
         UK_public  = UK, UK_private = 'UK (private)', 
         Japan_public = Japan, Japan_private = 'Japan (private)', 
         Norway_public = Norway, Norway_private = 'Norway (private)',
         USA_public = USA, USA_private = 'USA (private)') %>%
  pivot_longer(!year, names_to = c("country",".value"), names_sep = "_") %>%
  pivot_longer(3:4, names_to = "type", values_to = "value") %>%
  ggplot() +
  stat_smooth(aes(x = year, y = value, color = country, linetype = type), 
              formula = y~x, method = "loess", span = 0.25, se = FALSE, size=0.75) +
  scale_y_continuous(labels = scales::percent_format(accuracy = 1)) +
  labs(title = "Figure 8. The rise of private versus the decline of public wealth 
       \nin rich countries, 1970-2020", 
       x = "", y = "wealth as as % of national income", color = "", type = "")
```


---

![](eda4_files/figure-html/unnamed-chunk-52-1.png)<!-- -->

---

### F15: Per capita emissions acriss the world, 2019 - add row names + dodge


```r
df_f15 <- read_excel("data/WIR2022s.xlsx", sheet = "data-F15"); df_f15
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["regionWID"],"name":[1],"type":["chr"],"align":["left"]},{"label":["group"],"name":[2],"type":["chr"],"align":["left"]},{"label":["tcap"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["mark"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"East Asia","2":"Bottom 50%","3":"3.1186423","4":"1"},{"1":"NA","2":"Middle 40%","3":"7.9053422","4":"1"},{"1":"NA","2":"Top 10%","3":"38.9214325","4":"1"},{"1":"Europe","2":"Bottom 50%","3":"5.0919490","4":"2"},{"1":"NA","2":"Middle 40%","3":"10.6416652","4":"2"},{"1":"NA","2":"Top 10%","3":"29.1887054","4":"2"},{"1":"North America","2":"Bottom 50%","3":"9.6736345","4":"3"},{"1":"NA","2":"Middle 40%","3":"21.6508063","4":"3"},{"1":"NA","2":"Top 10%","3":"72.9800415","4":"3"},{"1":"South & South-East Asia","2":"Bottom 50%","3":"1.0377777","4":"4"},{"1":"NA","2":"Middle 40%","3":"2.4828077","4":"4"},{"1":"NA","2":"Top 10%","3":"10.5726061","4":"4"},{"1":"Russia & Central Asia","2":"Bottom 50%","3":"4.5784392","4":"5"},{"1":"NA","2":"Middle 40%","3":"10.1762814","4":"5"},{"1":"NA","2":"Top 10%","3":"35.1469002","4":"5"},{"1":"MENA","2":"Bottom 50%","3":"2.2593942","4":"6"},{"1":"NA","2":"Middle 40%","3":"7.3215994","4":"6"},{"1":"NA","2":"Top 10%","3":"33.6021652","4":"6"},{"1":"Latin America","2":"Bottom 50%","3":"1.9950299","4":"7"},{"1":"NA","2":"Middle 40%","3":"4.7466710","4":"7"},{"1":"NA","2":"Top 10%","3":"19.1952705","4":"7"},{"1":"Sub-Saharan Africa","2":"Bottom 50%","3":"0.5113959","4":"8"},{"1":"NA","2":"Middle 40%","3":"1.6974200","4":"8"},{"1":"NA","2":"Top 10%","3":"7.3439846","4":"8"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

---


```r
df_f15 %>% mutate(region = rep(regionWID[!is.na(regionWID)], each = 3)) %>%
  select(region, group, tcap) %>%
  ggplot(aes(x = region, y = tcap, fill = group)) +
  geom_col(position = "dodge") + 
  scale_x_discrete(labels = function(x) stringr::str_wrap(x, width = 10)) +
  labs(title = "Figure 15 Per capita emissions across the world, 2019", 
       x = "", y = "tonnes of CO2e per person per year", fill = "")
```


---

![](eda4_files/figure-html/unnamed-chunk-54-1.png)<!-- -->


## EDA Workflow

### EDA Step 0

1. Choose and clarify a topic to study.
2. List questions to study
3. Find data:
  - link to data with a url: universal resource locator in a webpage
  - download data in csv, Excel, etc.

Repeat the process during your EDA.


![image](data/data-science.png)

### EDA by R Studio: Step 1

In RStudio,

1.1. Project

  * Create a new project: File > New Project; or  
  * Open a project: File > Open Project, Open Project in New Session, Open Recent Project  
  * _Check there is a file `project_name.Rproj` in your project folder (directory)_

 
1.2. data folder (directory) `data`

  * Create a data folder: Press New Folder at the right bottom pane; or 
  * Confirm the data folder previously created: Press Files at the right bottom pane
  * _If you follow 1, the data folder exists in your project folder_

 
1.3. Move (or copy) data for the project to the data folder

  * If you downloaded the data, it is in your Download folder. Move it to `data`.
  * _Check in your RStudio that your data is in `data`: Press Files at the right bottom pane and click `data`, the data folder._
  

---

### EDA by R Studio: Step 2

2.1. Project Notebook: Memo

  - Create an R Notebook: File > New File > R Notebook
  
    + You can use R Notebook template in Moodle by moving the template (template.Rmd or template.nb.Rmd) file in your project folder or copy and paste the text file into your new R Notebook.
    + If you use template.nb.Rmd (R Notebook File), choose Open in Editor.
    
  - Add descriptive title. 
  
2.2. Setup Code Chunk 

  - Create a code chunk and add packages to use in the project and RUN the code.
  
      + library(tidyverse)
      + library(WDI)
      + or any other packages

---

2.3. Choose `Source` or `Visual` editor mode, and start editing Project Notebook

  - Set up Headings such as: About, Data, Analysis and Visualizations, Conclusions
  - Under About or Data, paste url of the sites and/or the data

      + eg. World Development Indicator:
      https://datatopics.worldbank.org/world-development-indicators/)
      + eg. Public expenditure on education:
      https://data.un.org/_Docs/SYB/CSV/SYB65_245_202209_Public%
      20expenditure%20on%20education.csv)


2.4. Edit a new file by saving as for a report

  - File > Save As...

---

### EDA by R Studio: Step 3 - Importing Data

Assign a name you can recall easily when you import data. You may need to reload the data with options.

3.1. Use a package:

  * WDI, wir, eurostat, etc/
  * `wdi_shortname <- WDI(indicator = "indicator's name", ... )
  * Store the data and use it: `write_csv(wdi_shortname, "data/wdi_shortname.csv")`
  * `wdi_shortname <- read_csv("data/wdi_shortname.csv")`
  
3.2. Use `readr` to read from `data`, your data folder

  * `df1_shortname <- read_csv("data/file_name.csv")`

---

3.3. Use `readr` to read using the url of the data

  * `df2_shortname <- read_csv("url_of_the_data")`
  * Store the data and use it: `write_csv(df2_shortname, "data/df2_shortname.csv")`
  * `df2_shortname <- read_csv("data/df2_shortname.csv")`
  
3.5. Use `readxl` to read Excel data. Add `library(readxl)` in the setup and run.

  * `df4 <- read_excel("data/file_name.xlsx", sheet = 1)`
  
References: Cheat Sheet - `readr`, [readr](https://readr.tidyverse.org), [readxl](https://readxl.tidyverse.org)


---

### EDA by R Studio: Step 4 - Data Trasnformation

4.1. Look at the data: suppose `df` is the data frame

  * It is a good option to change into a tibble: `dt <- as_tibble(df)`
  * `head(df)`, `str(df)`, `summary(df)`, `dt`, `glimpse(dt)`

4.2. Look at each variable

  * categorical? numerical? 
  * factor? - [forcats](https://forcats.tidyverse.org)
  
4.3. Variation of each data: suppose `x1` is a column name.

  * `df %>% ggplot() + geom_histogram(aes(x1), bins = 30)`
  * `df %>% drop_na(x1)`: see the rows with a value in `x1`. If the value is NA, the row is not shown.
  
    - `df_wo_na <- df %>% drop_na(x1)` if you want to use only the rows without NA in `x1`
    
---

4.4. Use `dpylr` and `tidyr` to change column names, tidy data, and/or summarize data

  * `rename`, `select`, `filter`, `arrange`, `mutate`, `pivot_longer()`, `pivot_wider()`, `group_by` and `summarize`


References: Cheat Sheet - `dplyr` and `tidyr`, [dplyr](https://dplyr.tidyverse.org), [tidyr](https://tidyr.tidyverse.org)

---

### EDA by R Studio: Step 5 - Visualize Data

5.1. In combination with Stap 4 - data transformation, try various data visualization.

  * What type of variation occurs within my variables?
  * What type of covariation occurs between my variables?


5.2. Keep a record of what you can observe by the visualization

5.3. Edit the list of questions by adding or polishing

5.4. Select several informative chart and add options

5.5. Look at examples from the textbooks or teaching site to have better visualization

References: Cheat Sheet - `ggplot2` [ggplot2](https://ggplot2.tidyverse.org), [ggplot2 book](https://ggplot2-book.org)

---

### EDA by R Studio: Step 6 - Conclusions and Questions for Further Study

1. EDA is an iterative cycle that helps you understand what your data says. When you do EDA, you:

2. Generate questions about your data

3. Search for answers by visualising, transforming, and/or modeling your data

Use what you learn to refine your questions and/or generate new questions

EDA is an important part of any data analysis. You can use EDA to make discoveries about the world; or you can use EDA to ensure the quality of your data, asking questions about whether the data meets your standards or not.

---

### Example: WDI

* Government expenditure on education, total (% of GDP)

  - https://data.worldbank.org/indicator/SE.XPD.TOTL.GD.ZS
  
* ID: SE.XPD.TOTL.GD.ZS

---

### Example: WIR2022

![](eda4_files/figure-html/unnamed-chunk-55-1.png)<!-- -->

## The Week Five Assignment (in Moodle)

**`tidyr` and WIR2022**

* Create an R Notebook of a Data Analysis containing the following and submit the rendered HTML file (eg. `a3_123456.nb.html`  by replacing 123456 with your ID)
  1. create an R Notebook using the R Notebook Template in Moodle,  save as `a3_123456.Rmd`, 
  2. write your name and ID and the contents, 
  3. run each code block, 
  4. preview to create `a3_123456.nb.html`,
  5. submit  `a3_123456.nb.html` to Moodle.

1. Choose a data with at least two categorical variables and at least two numerical variables.

    - Information of the data: Name, Indicator, Description, Source, etc.
    - Explain why you chose the indicator
    - List questions you want to study

---

2. Explore the data using visualization using `ggplot2`

    - Create various charts
    - Create at least one chart with at least two categocial variables and at least one numerical variable.
    - Create at least one chart with at least two numerical variables and at least one categorical variable.

3. Observations based on your data visualization, and difficulties and questions encountered if any.

**Due:** 2023-01-23 23:59:00. Submit your R Notebook file in Moodle (The Fourth Assignment). Due on Monday!




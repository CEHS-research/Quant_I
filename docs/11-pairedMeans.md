# t TEST FOR THE DIFFERENCE IN 2 PAIRED MEANS

**Chapter Links**

* [Chapter 11 Slides (pdf)](http://tysonbarrett.com/EDUC-6600/Slides/u03_Ch11_paired.html#1)

* [Cancer Dataset - SPSS format](https://usu.box.com/s/9c92zof5whb76bphmzxn3vqx5702qgq6)


**Unit Assignment Links**

* Unit 3 Writen Part: [Skeleton - pdf](https://usu.box.com/s/vjcsotiqwu1mwnwgzbfyig6k451ymgow)

* Unit 3 R Part: [Directions - pdf](https://usu.box.com/s/ectr9zx8qfbbm59h0qcexjreje5r9aio) and [Skeleton - Rmd](https://usu.box.com/s/k3vzw6nuq5tw66bxeptcyzth38pj69f9)

* Unit 3 Reading to Summarize: [Article - pdf](https://usu.box.com/s/qmo57s03tbq02ks75p7eb5gad0ap05kg)

* Inho's Dataset: [Excel](https://usu.box.com/s/hyky7eb24l6vvzj2xboedhcx1xolrpw1)







Required Packages 


```r
library(tidyverse)    # Loads several very helpful 'tidy' packages
library(haven)        # Read in SPSS datasets
library(car)          # Companion for Applied Regression (and ANOVA)
```




Example: Cancer Experiment 

The `Cancer` dataset was introduced in [chapter 3][Example: Cancer Experiment].







-------------------------------------------------------



## Restructure the Data and Run the Test

Before a paired t-test is ran, the dataset must be restructured from WIDE form (variables sitting side-by-side) to LONG form (variable values stacked on-top-of each other).

Notice for this dataset, there are $n = 23$ participants with complete data on the oral condition at weeks 2 and 6, since two out of the 25 do not have scores at the sixth week.



```r
# This dataset is in WIDE format: paired variables side-by-side
cancer_clean %>% 
  dplyr::filter(complete.cases(totalcw2, totalcw6))
```

```
# A tibble: 23 x 9
   id    trt       age weighin stage totalcin totalcw2 totalcw4 totalcw6
   <fct> <fct>   <dbl>   <dbl> <fct>    <dbl>    <dbl>    <dbl>    <dbl>
 1 1     Placebo  52.0     124 2         6.00     6.00     6.00     7.00
 2 5     Placebo  77.0     160 1         9.00     6.00    10.0      9.00
 3 6     Placebo  60.0     136 4         7.00     9.00    17.0     19.0 
 4 9     Placebo  61.0     180 1         6.00     7.00     9.00     3.00
 5 11    Placebo  59.0     176 2         6.00     7.00    16.0     13.0 
 6 15    Placebo  69.0     168 1         6.00     6.00     6.00    11.0 
 7 21    Placebo  67.0     186 1         6.00    11.0     11.0     10.0 
 8 26    Placebo  56.0     158 3         6.00    11.0     15.0     15.0 
 9 31    Placebo  61.0     213 1         6.00     9.00     6.00     8.00
10 35    Placebo  51.0     189 1         6.00     4.00     8.00     7.00
# ... with 13 more rows
```




The `tidyr::gather()` function requires the following FOUR options:

* **key** - A new variable name that will store the original variable names:  `key = new_group_var`

* **value** - A new variable name that will store the original variable values: `value = new_continuous_var`

* **variable list** - List the original variable names:  `orig_continous_var1, orig_continuous_var2`

* **na.rm** - Do not get ride of blank values (na.rm = remove the NA or blank values):  `na.rm = FALSE`



```r
# This dataset is in LONG format: total oral condiditon (at weeks 2 & 6) is stored in 1 variable, stacked
cancer_clean %>% 
  dplyr::filter(complete.cases(totalcw2, totalcw6)) %>% 
  tidyr::gather(key = time,
                value = totalc,
                totalcw2, totalcw6)
```

```
# A tibble: 46 x 9
   id    trt       age weighin stage totalcin totalcw4 time     totalc
   <fct> <fct>   <dbl>   <dbl> <fct>    <dbl>    <dbl> <chr>     <dbl>
 1 1     Placebo  52.0     124 2         6.00     6.00 totalcw2   6.00
 2 5     Placebo  77.0     160 1         9.00    10.0  totalcw2   6.00
 3 6     Placebo  60.0     136 4         7.00    17.0  totalcw2   9.00
 4 9     Placebo  61.0     180 1         6.00     9.00 totalcw2   7.00
 5 11    Placebo  59.0     176 2         6.00    16.0  totalcw2   7.00
 6 15    Placebo  69.0     168 1         6.00     6.00 totalcw2   6.00
 7 21    Placebo  67.0     186 1         6.00    11.0  totalcw2  11.0 
 8 26    Placebo  56.0     158 3         6.00    15.0  totalcw2  11.0 
 9 31    Placebo  61.0     213 1         6.00     6.00 totalcw2   9.00
10 35    Placebo  51.0     189 1         6.00     8.00 totalcw2   4.00
# ... with 36 more rows
```


The `t.test()` function, needs at least THREE arguments:

* **formula** - The formula specifies the two variabels, where order matters.  The name of the dependent variable  (DV or outcome) is on the left side of the tilda symbol and the independent variable (IV or predictor) is on the right side: `dependent_y_var ~ predictor_x_var`

* **data** - Since the datset is not the first argument in the function, you must use the period to signify that the datset is being piped from above: `data = .` 

* **paired** - The default is independent groups, so include: `paired = TRUE` 



```r
cancer_clean %>% 
  dplyr::filter(complete.cases(totalcw2, totalcw6)) %>% 
  tidyr::gather(key = time,
                value = totalc,
                totalcw2, totalcw6,
                na.rm = FALSE) %>% 
  t.test(totalc ~ time,
         data = .,
         paired = TRUE)
```

```

	Paired t-test

data:  totalc by time
t = -1.8028, df = 22, p-value = 0.08513
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -2.8048027  0.1961071
sample estimates:
mean of the differences 
              -1.304348 
```













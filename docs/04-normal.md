# STANDARDIZING SCORES

**Chapter Links**

* [Chapter 4 Slide Show](http://tysonbarrett.com/EDUC-6600/Slides/01_Ch4_Zscores.html#1)

* [Cancer Dataset - SPSS format](https://usu.box.com/s/9c92zof5whb76bphmzxn3vqx5702qgq6)

**Assignment Links**

* [Unit 1 Assignment - Write Up Skeleton](https://usu.box.com/s/bn0m44cp5zrkev3ppjdilfsvic4bubvu)

* [Unit 1 Assignment - Rmd Skeleton](https://usu.box.com/s/zjjwexn827ziifxlcoe6emr2brfifk0x)

* [Inho's Dataset - Excel format](https://usu.box.com/s/hyky7eb24l6vvzj2xboedhcx1xolrpw1)








## Example: Cancer Experiment {-}

see chapter 3


### Required Packages {-}


```r
library(tidyverse)    # Loads several very helpful 'tidy' packages
library(haven)        # Read in SPSS datasets
library(furniture)    # Nice tables (by our own Tyson Barrett)
library(psych)        # Lots of nice tid-bits
```

### Data Import {-}

The `Cancer` dataset is saved in SPSS format, which is evident from the `.sav` ending on the file name.

The `haven` package is downloaded as part of the `tidyverse` set of packages, but is not automatically loaded.  It must have its own `library()` function call *(see above)*.  The `haven::read_spss()` function works very simarly to the `readxl::read_excel()` function we used last chapter [@R-haven].

* Make sure the **dataset** is saved in the same *folder* as this file
* Make sure the that *folder* is the **working directory**


```r
cancer_raw <- haven::read_spss("cancer.sav")
```





```r
tibble::glimpse(cancer_raw)
```

```
Observations: 25
Variables: 9
$ ID       <dbl> 1, 5, 6, 9, 11, 15, 21, 26, 31, 35, 39, 41, 45, 2, 12...
$ TRT      <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1,...
$ AGE      <dbl> 52, 77, 60, 61, 59, 69, 67, 56, 61, 51, 46, 65, 67, 4...
$ WEIGHIN  <dbl> 124.0, 160.0, 136.5, 179.6, 175.8, 167.6, 186.0, 158....
$ STAGE    <dbl> 2, 1, 4, 1, 2, 1, 1, 3, 1, 1, 4, 1, 1, 2, 4, 1, 2, 1,...
$ TOTALCIN <dbl> 6, 9, 7, 6, 6, 6, 6, 6, 6, 6, 7, 6, 8, 7, 6, 4, 6, 6,...
$ TOTALCW2 <dbl> 6, 6, 9, 7, 7, 6, 11, 11, 9, 4, 8, 6, 8, 16, 10, 6, 1...
$ TOTALCW4 <dbl> 6, 10, 17, 9, 16, 6, 11, 15, 6, 8, 11, 9, 9, 9, 11, 8...
$ TOTALCW6 <dbl> 7, 9, 19, 3, 13, 11, 10, 15, 8, 7, 11, 6, 10, 10, 9, ...
```


### Data Wrangling {-}


```r
cancer_clean <- cancer_raw %>% 
  dplyr::rename_all(tolower) %>% 
  dplyr::mutate(id = factor(id)) %>% 
  dplyr::mutate(trt = factor(trt,
                             labels = c("Placebo", 
                                        "Aloe Juice"))) %>% 
  dplyr::mutate(stage = factor(stage))

tibble::glimpse(cancer_clean)
```

```
Observations: 25
Variables: 9
$ id       <fct> 1, 5, 6, 9, 11, 15, 21, 26, 31, 35, 39, 41, 45, 2, 12...
$ trt      <fct> Placebo, Placebo, Placebo, Placebo, Placebo, Placebo,...
$ age      <dbl> 52, 77, 60, 61, 59, 69, 67, 56, 61, 51, 46, 65, 67, 4...
$ weighin  <dbl> 124.0, 160.0, 136.5, 179.6, 175.8, 167.6, 186.0, 158....
$ stage    <fct> 2, 1, 4, 1, 2, 1, 1, 3, 1, 1, 4, 1, 1, 2, 4, 1, 2, 1,...
$ totalcin <dbl> 6, 9, 7, 6, 6, 6, 6, 6, 6, 6, 7, 6, 8, 7, 6, 4, 6, 6,...
$ totalcw2 <dbl> 6, 6, 9, 7, 7, 6, 11, 11, 9, 4, 8, 6, 8, 16, 10, 6, 1...
$ totalcw4 <dbl> 6, 10, 17, 9, 16, 6, 11, 15, 6, 8, 11, 9, 9, 9, 11, 8...
$ totalcw6 <dbl> 7, 9, 19, 3, 13, 11, 10, 15, 8, 7, 11, 6, 10, 10, 9, ...
```


---------------------------------------




### Standardize Variables - Manually

You can manually create a stadradized version of the `age` variable.


First, you must find the **mean** and **standard deviation** of the `age` variable.


```r
cancer_clean %>%
  furniture::table1(age)
```

```

-----------------------
     Mean/Count (SD/%)
     n = 25           
 age                  
     59.6 (12.9)      
-----------------------
```


Second, write an equation to do the calculation.


```r
cancer_clean %>%
  dplyr::mutate(agez = (age - 59.6) / 12.9) %>% 
  dplyr::select(id, trt, age, agez)
```

```
# A tibble: 25 x 4
   id    trt       age    agez
   <fct> <fct>   <dbl>   <dbl>
 1 1     Placebo  52.0 -0.589 
 2 5     Placebo  77.0  1.35  
 3 6     Placebo  60.0  0.0310
 4 9     Placebo  61.0  0.109 
 5 11    Placebo  59.0 -0.0465
 6 15    Placebo  69.0  0.729 
 7 21    Placebo  67.0  0.574 
 8 26    Placebo  56.0 -0.279 
 9 31    Placebo  61.0  0.109 
10 35    Placebo  51.0 -0.667 
# ... with 15 more rows
```


### Standardize Variables - with the `scale()` funciton

A quicker way is to use a funciton.  Notice the differences due to rounding.


```r
cancer_new <- cancer_clean %>%
  dplyr::mutate(agez = (age - 59.6) / 12.9) %>% 
  dplyr::mutate(ageZ = scale(age))%>%
  dplyr::select(id, trt, age, agez, ageZ)

cancer_new
```

```
# A tibble: 25 x 5
   id    trt       age    agez    ageZ
   <fct> <fct>   <dbl>   <dbl>   <dbl>
 1 1     Placebo  52.0 -0.589  -0.591 
 2 5     Placebo  77.0  1.35    1.34  
 3 6     Placebo  60.0  0.0310  0.0278
 4 9     Placebo  61.0  0.109   0.105 
 5 11    Placebo  59.0 -0.0465 -0.0495
 6 15    Placebo  69.0  0.729   0.724 
 7 21    Placebo  67.0  0.574   0.569 
 8 26    Placebo  56.0 -0.279  -0.281 
 9 31    Placebo  61.0  0.109   0.105 
10 35    Placebo  51.0 -0.667  -0.668 
# ... with 15 more rows
```

You can check that the new variable does in deed have mean of zero and spread of one.


```r
cancer_new %>% 
  furniture::table1(age, agez, ageZ,
                    digits = 8)
```

```

--------------------------------
      Mean/Count (SD/%)        
      n = 25                   
 age                           
      59.64000000 (12.93213053)
 agez                          
      0.00310078 (1.00249074)  
 ageZ                          
      -0.00000000 (1.00000000) 
--------------------------------
```


Both the mean and the standard deviation are different.


```r
cancer_new %>% 
  tidyr::gather(key = "variable",
                value = "value",
                age, ageZ) %>% 
  ggplot(aes(value)) +
  geom_histogram(bins = 8) +
  facet_grid(. ~ variable)
```

<img src="04-normal_files/figure-html/unnamed-chunk-9-1.png" width="672" />

However, if you let the scale of the x-axis change, you see the shape of the two variables is identical.


```r
cancer_new %>% 
  tidyr::gather(key = "variable",
                value = "value",
                age, ageZ) %>% 
  ggplot(aes(value)) +
  geom_histogram(bins = 8) +
  facet_grid(. ~ variable, scale = "free_x")
```

<img src="04-normal_files/figure-html/unnamed-chunk-10-1.png" width="672" />




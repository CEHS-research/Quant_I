# Linear Regression

**Chapter Links**

* [Chapter 10 Slide Show](http://tysonbarrett.com/EDUC-6600/Slides/u03_Ch10_LinReg.html#1)

* [Interactive Online App - Correlation and Regression](http://digitalfirst.bfwpub.com/stats_applet/stats_applet_5_correg.html)

* [Cancer Dataset - SPSS format](https://usu.box.com/s/9c92zof5whb76bphmzxn3vqx5702qgq6)



**Assignment Links**

* [Unit 3 Assignment - Write Up Skeleton .pdf](https://usu.box.com/s/vjcsotiqwu1mwnwgzbfyig6k451ymgow)

* [Unit 3 Assignment - R Directions .pdf](https://usu.box.com/s/ectr9zx8qfbbm59h0qcexjreje5r9aio)

* [Unit 3 Assignment - R Skeleton .Rmd](https://usu.box.com/s/k3vzw6nuq5tw66bxeptcyzth38pj69f9)

* [Inho's Dataset - Excel format](https://usu.box.com/s/hyky7eb24l6vvzj2xboedhcx1xolrpw1)








Required Packages 


```r
library(tidyverse)    # Loads several very helpful 'tidy' packages
library(haven)        # Read in SPSS datasets
library(car)          # Companion for Applied Regression (and ANOVA)
```




Example: Cancer Experiment 

The `Cancer` dataset was introduced in [chapter 3][Example: Cancer Experiment].






Check Means and SD’s


```r
cancer_clean %>% 
  dplyr::group_by(trt) %>% 
  furniture::table1(totalcin, totalcw4)
```

```

--------------------------------
                 trt 
          Placebo    Aloe Juice
          n = 14     n = 11    
 totalcin                      
          6.6 (0.9)  6.5 (2.1) 
 totalcw4                      
          10.1 (3.6) 10.6 (3.5)
--------------------------------
```


-------------------------------------------------------


## Fitting a Simple Regression Model


### Minimal Example

Always plot your data first!


```r
cancer_clean %>% 
  ggplot(aes(x = age,
             y = weighin)) +
  geom_point() +
  geom_smooth(method = "lm")
```

<img src="10-reg_files/figure-html/unnamed-chunk-3-1.png" width="672" />

The `lm()` function needs at least TWO arguments:

* **formula** - The name of the *outcome* or dependent variable (DV) goes on the left of the tilda symbol and the name of the *predictor* or independent variable (IV) comes after: `continuous_y ~ continuous_x`

* **data** - Since the datset is not the first argument in the function, you must use the period to signify that the datset is being piped from above `data = .` 





```r
cancer_clean %>% 
  lm(weighin ~ age,    # formula: order DOES matter
     data = .)         # data piped from above
```

```

Call:
lm(formula = weighin ~ age, data = .)

Coefficients:
(Intercept)          age  
   220.6899      -0.7111  
```


> **NOTE:** To view more complete information, add a `summary()` step using a pipe AFTER the `lm()` step


```r
cancer_clean %>% 
  lm(weighin ~ age,    # formula: order DOES matter
     data = .) %>%     # data piped from above
  summary()
```

```

Call:
lm(formula = weighin ~ age, data = .)

Residuals:
    Min      1Q  Median      3Q     Max 
-59.713 -19.535  -2.935  12.954  71.998 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) 220.6899    30.1076    7.33 1.86e-07 ***
age          -0.7111     0.4938   -1.44    0.163    
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 31.28 on 23 degrees of freedom
Multiple R-squared:  0.08271,	Adjusted R-squared:  0.04282 
F-statistic: 2.074 on 1 and 23 DF,  p-value: 0.1633
```

### Variable Designation Matters!

In simple linear regression (with only one predictor DV), the slope estimate ($\hat{\beta_1}$) is different depending on the designation of $x$ and $y$ (two ordering), but the $p-values$ are the same.



```r
cancer_clean %>% 
  lm(age ~ weighin,    # formula: order DOES matter
     data = .) %>%     # data piped from above
  summary()
```

```

Call:
lm(formula = age ~ weighin, data = .)

Residuals:
    Min      1Q  Median      3Q     Max 
-27.160  -6.277   1.514   8.258  21.908 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) 80.37531   14.61964   5.498 1.37e-05 ***
weighin     -0.11631    0.08077  -1.440    0.163    
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 12.65 on 23 degrees of freedom
Multiple R-squared:  0.08271,	Adjusted R-squared:  0.04282 
F-statistic: 2.074 on 1 and 23 DF,  p-value: 0.1633
```












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


## 

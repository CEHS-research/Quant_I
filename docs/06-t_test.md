# t TEST FOR THE MEAN OF 1 SAMPLE

**Chapter Links**

* [Chapter 6 Slide Show](http://tysonbarrett.com/EDUC-6600/Slides/u02_Ch6_CI_tDist.html#1)

* [Interactive Online App - Confidence Intervals](http://digitalfirst.bfwpub.com/stats_applet/stats_applet_4_ci.html)

* [Cancer Dataset - SPSS format](https://usu.box.com/s/9c92zof5whb76bphmzxn3vqx5702qgq6)



**Assignment Links**

* [Unit 2 Assignment - Write Up Skeleton](https://usu.box.com/s/mr5ersj8oqu6mj3tyup697ljg2527p8h)

* [Unit 2 Assignment - Rmd Skeleton](https://usu.box.com/s/85s7t82tih6f06v8bpvjo0qt275gafsr)

* [Inho's Dataset - Excel format](https://usu.box.com/s/hyky7eb24l6vvzj2xboedhcx1xolrpw1)






Required Packages 


```r
library(tidyverse)    # Loads several very helpful 'tidy' packages
library(haven)        # Read in SPSS datasets
```




Example: Cancer Experiment 

The `Cancer` dataset was introduced in [chapter 3][Example: Cancer Experiment].








## 1 Sample Mean vs. historic control

example: Do the patients weigh more than 165 pounds at intake, on average?



```r
cancer_clean %>% 
  dplyr::pull(weighin) %>% 
  t.test(mu = 165)
```

```

	One Sample t-test

data:  .
t = 2.0765, df = 24, p-value = 0.04872
alternative hypothesis: true mean is not equal to 165
95 percent confidence interval:
 165.0807 191.4793
sample estimates:
mean of x 
   178.28 
```



## Change the Confidence Level

Find a 99% confience level for the population mean weight.


```r
cancer_clean %>% 
  dplyr::pull(weighin) %>% 
  t.test(mu = 165,
         conf.level = 0.99)
```

```

	One Sample t-test

data:  .
t = 2.0765, df = 24, p-value = 0.04872
alternative hypothesis: true mean is not equal to 165
99 percent confidence interval:
 160.3927 196.1673
sample estimates:
mean of x 
   178.28 
```


## Restrict to a Subsample

Do the patients with .dcoral[stage 3 & 4] cancer weigh more than 165 pounds at intake, on average?


```r
cancer_clean %>% 
  dplyr::filter(stage %in% c("3", "4")) %>% 
  dplyr::pull(weighin) %>% 
  t.test(mu = 165)
```

```

	One Sample t-test

data:  .
t = 0.82627, df = 5, p-value = 0.4463
alternative hypothesis: true mean is not equal to 165
95 percent confidence interval:
 137.0283 219.4717
sample estimates:
mean of x 
   178.25 
```



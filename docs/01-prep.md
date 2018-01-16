# Preparing Datasets 


## Load Needed Packages




You will need TWO packages:

* `tidyverse` Easily Install and Load the 'Tidyverse'
* `readxl` Read Excel Files


```r
library(tidyverse)
library(readxl)
```

## Read in the Data from Excel and store the data as `data`



```r
data <- read_excel("Ihno_dataset.xls")
```


Print out the dataset


```r
data
```



```r
#data
```

> NOTE: The pound or hashtag symbol at the front of a line within an R code chunk designates what follows as a comment and does not try to run the code.


List out the variable names


```r
# variables names
names(data)
```

```
 [1] "Sub_num"  "Gender"   "Major"    "Reason"   "Exp_cond" "Coffee"  
 [7] "Num_cups" "Phobia"   "Prevmath" "Mathquiz" "Statquiz" "Exp_sqz" 
[13] "Hr_base"  "Hr_pre"   "Hr_post"  "Anx_base" "Anx_pre"  "Anx_post"
```

How many row (participants) and columns (variables)


```r
# data frame's dimentions
dim(data)
```

```
[1] 100  18
```




## Setting variables to factors and labeling values



```r
dataF <- data %>% 
  dplyr::mutate(GenderF = Gender %>% 
                  factor(levels = c(1, 2),
                         labels = c("Female", "Male"))) %>% 
  dplyr::mutate(MajorF = Major %>% 
                  factor(levels = c(1, 2, 3, 4,5),
                         labels = c("Psychology",
                                    "Premed",
                                    "Biology",
                                    "Sociology",
                                    "Economics"))) %>% 
  dplyr::mutate(ReasonF = Reason %>% 
                  factor(levels = c(1, 2, 3),
                         labels = c("Program requirement",
                                    "Personal interest",
                                    "Advisor recommendation"))) %>% 
  dplyr::mutate(Exp_condF = Exp_cond %>% 
                  factor(levels = c(1, 2, 3, 4),
                         labels = c("Easy",
                                    "Moderate",
                                    "Difficult",
                                    "Impossible"))) %>% 
  dplyr::mutate(CoffeeF = Coffee %>% 
                  factor(levels = c(0, 1),
                         labels = c("Not a regular coffee drinker",
                                    "Regularly drinks coffee"))) 
```


```r
glimpse(data)
```

```
Observations: 100
Variables: 18
$ Sub_num  <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16...
$ Gender   <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
$ Major    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
$ Reason   <dbl> 3, 2, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1,...
$ Exp_cond <dbl> 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 3, 4, 4, 4, 4,...
$ Coffee   <dbl> 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1,...
$ Num_cups <dbl> 0, 0, 0, 0, 1, 1, 0, 2, 0, 2, 1, 0, 1, 2, 3, 0, 0, 3,...
$ Phobia   <dbl> 1, 1, 4, 4, 10, 4, 4, 4, 4, 5, 5, 4, 7, 4, 3, 8, 4, 5...
$ Prevmath <dbl> 3, 4, 1, 0, 1, 1, 2, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1, 1,...
$ Mathquiz <dbl> 43, 49, 26, 29, 31, 20, 13, 23, 38, NA, 29, 32, 18, N...
$ Statquiz <dbl> 6, 9, 8, 7, 6, 7, 3, 7, 8, 7, 8, 8, 1, 5, 8, 3, 8, 7,...
$ Exp_sqz  <dbl> 7, 11, 8, 8, 6, 6, 4, 7, 7, 6, 10, 7, 3, 4, 6, 1, 7, ...
$ Hr_base  <dbl> 71, 73, 69, 72, 71, 70, 71, 77, 73, 78, 74, 73, 73, 7...
$ Hr_pre   <dbl> 68, 75, 76, 73, 83, 71, 70, 87, 72, 76, 72, 74, 76, 8...
$ Hr_post  <dbl> 65, 68, 72, 78, 74, 76, 66, 84, 67, 74, 73, 74, 78, 7...
$ Anx_base <dbl> 17, 17, 19, 19, 26, 12, 12, 17, 20, 20, 21, 32, 19, 1...
$ Anx_pre  <dbl> 22, 19, 14, 13, 30, 15, 16, 19, 14, 24, 25, 35, 23, 2...
$ Anx_post <dbl> 20, 16, 15, 16, 25, 19, 17, 22, 17, 19, 22, 33, 20, 2...
```


```r
glimpse(dataF)
```

```
Observations: 100
Variables: 23
$ Sub_num   <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 1...
$ Gender    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
$ Major     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
$ Reason    <dbl> 3, 2, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1...
$ Exp_cond  <dbl> 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 3, 4, 4, 4, 4...
$ Coffee    <dbl> 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1...
$ Num_cups  <dbl> 0, 0, 0, 0, 1, 1, 0, 2, 0, 2, 1, 0, 1, 2, 3, 0, 0, 3...
$ Phobia    <dbl> 1, 1, 4, 4, 10, 4, 4, 4, 4, 5, 5, 4, 7, 4, 3, 8, 4, ...
$ Prevmath  <dbl> 3, 4, 1, 0, 1, 1, 2, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1, 1...
$ Mathquiz  <dbl> 43, 49, 26, 29, 31, 20, 13, 23, 38, NA, 29, 32, 18, ...
$ Statquiz  <dbl> 6, 9, 8, 7, 6, 7, 3, 7, 8, 7, 8, 8, 1, 5, 8, 3, 8, 7...
$ Exp_sqz   <dbl> 7, 11, 8, 8, 6, 6, 4, 7, 7, 6, 10, 7, 3, 4, 6, 1, 7,...
$ Hr_base   <dbl> 71, 73, 69, 72, 71, 70, 71, 77, 73, 78, 74, 73, 73, ...
$ Hr_pre    <dbl> 68, 75, 76, 73, 83, 71, 70, 87, 72, 76, 72, 74, 76, ...
$ Hr_post   <dbl> 65, 68, 72, 78, 74, 76, 66, 84, 67, 74, 73, 74, 78, ...
$ Anx_base  <dbl> 17, 17, 19, 19, 26, 12, 12, 17, 20, 20, 21, 32, 19, ...
$ Anx_pre   <dbl> 22, 19, 14, 13, 30, 15, 16, 19, 14, 24, 25, 35, 23, ...
$ Anx_post  <dbl> 20, 16, 15, 16, 25, 19, 17, 22, 17, 19, 22, 33, 20, ...
$ GenderF   <fctr> Female, Female, Female, Female, Female, Female, Fem...
$ MajorF    <fctr> Psychology, Psychology, Psychology, Psychology, Psy...
$ ReasonF   <fctr> Advisor recommendation, Personal interest, Program ...
$ Exp_condF <fctr> Easy, Easy, Easy, Easy, Easy, Moderate, Moderate, M...
$ CoffeeF   <fctr> Regularly drinks coffee, Not a regular coffee drink...
```

## Creating new variables

### Question 2: Create a new variable = `mathquiz` + 50



```r
data2 <- dataF %>% 
  dplyr::mutate(Mathquiz_p50 = Mathquiz + 50) 
```



```r
data2 %>% 
  dplyr::select(Sub_num, Mathquiz, Mathquiz_p50) %>% 
  head()
```

```
# A tibble: 6 x 3
  Sub_num Mathquiz Mathquiz_p50
    <dbl>    <dbl>        <dbl>
1    1.00     43.0         93.0
2    2.00     49.0         99.0
3    3.00     26.0         76.0
4    4.00     29.0         79.0
5    5.00     31.0         81.0
6    6.00     20.0         70.0
```



### Question 3: Create a new variable = `Hr_base` / 60


```r
data3 <- data2 %>% 
  dplyr::mutate(Hr_base_bpm = Hr_base / 60) 
```



```r
data3 %>% 
  dplyr::select(Sub_num, Hr_base, Hr_base_bpm) %>% 
  head(n = 10)
```

```
# A tibble: 10 x 3
   Sub_num Hr_base Hr_base_bpm
     <dbl>   <dbl>       <dbl>
 1    1.00    71.0        1.18
 2    2.00    73.0        1.22
 3    3.00    69.0        1.15
 4    4.00    72.0        1.20
 5    5.00    71.0        1.18
 6    6.00    70.0        1.17
 7    7.00    71.0        1.18
 8    8.00    77.0        1.28
 9    9.00    73.0        1.22
10   10.0     78.0        1.30
```


### Question 4a: Create a new variable  = `Statquiz` + 2, then * 10



```r
data4a <- data3 %>% 
  dplyr::mutate(Statquiz_4a = (Statquiz + 2) * 10 )
```


### Question 4b: Create a new variable  = `Statquiz` * 10, then + 2


```r
data4b <- data4a %>% 
  dplyr::mutate(Statquiz_4b = (Statquiz * 10) + 2 )
```


```r
data4b %>% 
  dplyr::select(Sub_num, Statquiz, Statquiz_4a, Statquiz_4b) %>% 
  head()
```

```
# A tibble: 6 x 4
  Sub_num Statquiz Statquiz_4a Statquiz_4b
    <dbl>    <dbl>       <dbl>       <dbl>
1    1.00     6.00        80.0        62.0
2    2.00     9.00       110          92.0
3    3.00     8.00       100          82.0
4    4.00     7.00        90.0        72.0
5    5.00     6.00        80.0        62.0
6    6.00     7.00        90.0        72.0
```



### Question 5a: Create a new variable = `sum` of the 3 anxiety measures 



```r
data5a <- data4b %>% 
  dplyr::mutate(Anx_plus = Anx_base + Anx_pre + Anx_post) %>%
  dplyr::mutate(Anx_sum1 = sum(Anx_base, Anx_pre, Anx_post)) %>%
  dplyr::rowwise() %>% 
  dplyr::mutate(Anx_sum = sum(c(Anx_base, Anx_pre, Anx_post))) %>% 
  dplyr::ungroup()
```




```r
data5a %>% 
  dplyr::select(Sub_num, 
                Anx_base, Anx_pre, Anx_post, 
                Anx_plus, Anx_sum1, Anx_sum) %>% 
  head()
```

```
# A tibble: 6 x 7
  Sub_num Anx_base Anx_pre Anx_post Anx_plus Anx_sum1 Anx_sum
    <dbl>    <dbl>   <dbl>    <dbl>    <dbl>    <dbl>   <dbl>
1    1.00     17.0    22.0     20.0     59.0     5741    59.0
2    2.00     17.0    19.0     16.0     52.0     5741    52.0
3    3.00     19.0    14.0     15.0     48.0     5741    48.0
4    4.00     19.0    13.0     16.0     48.0     5741    48.0
5    5.00     26.0    30.0     25.0     81.0     5741    81.0
6    6.00     12.0    15.0     19.0     46.0     5741    46.0
```

\clearpage

### Question 5b: Create a new variable = `average` of the 3 heart rates 



```r
data5b <- data5a %>% 
  dplyr::mutate(Hr_avg = (Hr_base + Hr_pre + Hr_post)/3) %>%
  # dplyr::mutate(Hr_mean1 = mean(Hr_base, Hr_pre, Hr_post, na.rm = TRUE)) %>%
  dplyr::rowwise() %>% 
  dplyr::mutate(Hr_mean = mean(c(Hr_base, Hr_pre, Hr_post))) %>% 
  dplyr::ungroup()
```



```r
data5b %>% 
  dplyr::select(Sub_num, 
                Hr_base, Hr_pre, Hr_post, 
                Hr_avg,  Hr_mean) %>% 
  head()
```

```
# A tibble: 6 x 6
  Sub_num Hr_base Hr_pre Hr_post Hr_avg Hr_mean
    <dbl>   <dbl>  <dbl>   <dbl>  <dbl>   <dbl>
1    1.00    71.0   68.0    65.0   68.0    68.0
2    2.00    73.0   75.0    68.0   72.0    72.0
3    3.00    69.0   76.0    72.0   72.3    72.3
4    4.00    72.0   73.0    78.0   74.3    74.3
5    5.00    71.0   83.0    74.0   76.0    76.0
6    6.00    70.0   71.0    76.0   72.3    72.3
```

\clearpage

### Question 6: Create a new variable = `Statquiz` minus `Exp_sqz`


```r
data6 <- data5b %>% 
  dplyr::mutate(StatDiff = Statquiz - Exp_sqz)
```


```r
data6 %>% 
  dplyr::select(Sub_num, Exp_cond, Exp_cond,
                Statquiz, Exp_sqz, StatDiff) %>% 
  head()
```

```
# A tibble: 6 x 5
  Sub_num Exp_cond Statquiz Exp_sqz StatDiff
    <dbl>    <dbl>    <dbl>   <dbl>    <dbl>
1    1.00     1.00     6.00    7.00    -1.00
2    2.00     1.00     9.00   11.0     -2.00
3    3.00     1.00     8.00    8.00     0   
4    4.00     1.00     7.00    8.00    -1.00
5    5.00     1.00     6.00    6.00     0   
6    6.00     2.00     7.00    6.00     1.00
```

\clearpage

## Putting it all together


```r
data_clean <- read_excel("Ihno_dataset.xls") %>% 
  dplyr::mutate(GenderF = Gender %>% 
                  factor(levels = c(1, 2),
                         labels = c("Female", "Male"))) %>% 
  dplyr::mutate(MajorF = Major %>% 
                  factor(levels = c(1, 2, 3, 4,5),
                         labels = c("Psychology",
                                    "Premed",
                                    "Biology",
                                    "Sociology",
                                    "Economics"))) %>% 
  dplyr::mutate(ReasonF = Reason %>% 
                  factor(levels = c(1, 2, 3),
                         labels = c("Program requirement",
                                    "Personal interest",
                                    "Advisor recommendation"))) %>% 
  dplyr::mutate(Exp_condF = Exp_cond %>% 
                  factor(levels = c(1, 2, 3, 4),
                         labels = c("Easy",
                                    "Moderate",
                                    "Difficult",
                                    "Impossible"))) %>% 
  dplyr::mutate(CoffeeF = Coffee %>% 
                  factor(levels = c(0, 1),
                         labels = c("Not a regular coffee drinker",
                                    "Regularly drinks coffee")))  %>% 
  dplyr::mutate(Mathquiz_p50 = Mathquiz + 50) %>% 
  dplyr::mutate(Hr_base_bpm = Hr_base / 60) %>% 
  dplyr::mutate(Statquiz_4a = (Statquiz +  2) * 10 ) %>% 
  dplyr::mutate(Statquiz_4b = (Statquiz * 10) + 2 ) %>%
  dplyr::rowwise() %>% 
  dplyr::mutate(Anx_sum = sum(c(Anx_base, Anx_pre, Anx_post), na.rm = TRUE)) %>% 
  dplyr::mutate(Hr_mean = mean(c(Hr_base, Hr_pre, Hr_post), na.rm = TRUE)) %>%  
  dplyr::ungroup() %>% 
  dplyr::mutate(StatDiff = Statquiz - Exp_sqz)
```




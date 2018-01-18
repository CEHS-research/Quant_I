# Preparing Datasets 



---------------------------------------

## ENVIRONMENT PREPARATION

![](img/headers/library.png)


### The `library()` Function: Load a Package


You will need TWO packages:

* `tidyverse` Easily Install and Load the 'Tidy universe' of packages
* `readxl` Read Excel Files
* `furniture` Nice Tables and Row-wise functions (by Tyson)

> Make sure the packages are **installed** *(Package tab)*

The function `library()` checks the package out, or makes it active.


```r
library(tidyverse)
library(readxl)
library(furniture)
```



### The `readxl::read_excel()` Function: Read in Excel Data Files

> Make sure the **dataset** is saved in the same *folder* as this file

> Make sure the that *folder* is the **working directory**

* Now we are ready to open the data with the `read_excel()` function from the `readxl` package
    + `readxl::read_excel()` the double colon specifies the `package::function()`
    + the only thing required inside the `()` is the quoted name of the Excel file 
      - Make sure it is stored in the .Rmd's folder
      - Make sure to include the file's extension *(.xls)*
      
> NOTE: a `tibble` is basically just a "table" of data, the way the tidy-verse represents data sets.
      

```r
read_excel("Ihno_dataset.xls")
```

```
# A tibble: 100 x 18
   Sub_num Gender Major Reason Exp_cond Coffee Num_cups Phobia Prevmath
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00     0      1.00     3.00
 2    2.00   1.00  1.00   2.00     1.00   0        0      1.00     4.00
 3    3.00   1.00  1.00   1.00     1.00   0        0      4.00     1.00
 4    4.00   1.00  1.00   1.00     1.00   0        0      4.00     0   
 5    5.00   1.00  1.00   1.00     1.00   0        1.00  10.0      1.00
 6    6.00   1.00  1.00   1.00     2.00   1.00     1.00   4.00     1.00
 7    7.00   1.00  1.00   1.00     2.00   0        0      4.00     2.00
 8    8.00   1.00  1.00   3.00     2.00   1.00     2.00   4.00     1.00
 9    9.00   1.00  1.00   1.00     2.00   0        0      4.00     1.00
10   10.0    1.00  1.00   1.00     2.00   1.00     2.00   5.00     0   
# ... with 90 more rows, and 9 more variables: Mathquiz <dbl>, Statquiz
#   <dbl>, Exp_sqz <dbl>, Hr_base <dbl>, Hr_pre <dbl>, Hr_post <dbl>,
#   Anx_base <dbl>, Anx_pre <dbl>, Anx_post <dbl>
```


------------------------------------

## OPPERATORS and HELPFUL FUNCTIONS

### The `<-` Assignment Opperator: Save as a Name

* the `<-` combination of symbols makes **assignments**
   + tells **R** to store the dataset as the name it points to
   + this lets us use the dataset later on in another step

> NOTE: no output is produced when you make an assignment.


```r
data <- read_excel("Ihno_dataset.xls") 
```


* Print out the dataset by just typing and running the name you assigned it


```r
data
```

```
# A tibble: 100 x 18
   Sub_num Gender Major Reason Exp_cond Coffee Num_cups Phobia Prevmath
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00     0      1.00     3.00
 2    2.00   1.00  1.00   2.00     1.00   0        0      1.00     4.00
 3    3.00   1.00  1.00   1.00     1.00   0        0      4.00     1.00
 4    4.00   1.00  1.00   1.00     1.00   0        0      4.00     0   
 5    5.00   1.00  1.00   1.00     1.00   0        1.00  10.0      1.00
 6    6.00   1.00  1.00   1.00     2.00   1.00     1.00   4.00     1.00
 7    7.00   1.00  1.00   1.00     2.00   0        0      4.00     2.00
 8    8.00   1.00  1.00   3.00     2.00   1.00     2.00   4.00     1.00
 9    9.00   1.00  1.00   1.00     2.00   0        0      4.00     1.00
10   10.0    1.00  1.00   1.00     2.00   1.00     2.00   5.00     0   
# ... with 90 more rows, and 9 more variables: Mathquiz <dbl>, Statquiz
#   <dbl>, Exp_sqz <dbl>, Hr_base <dbl>, Hr_pre <dbl>, Hr_post <dbl>,
#   Anx_base <dbl>, Anx_pre <dbl>, Anx_post <dbl>
```

> NOTE: The pound or hashtag symbol at the front of a line within an R code chunk designates what follows as a comment and does not try to run the code.


```r
#data
```


### The Pipe `%>%` Opperator: Link Steps Togehter

This special set of symbols *(no spaces included)* signals R to feed what precedes it **into** what follows it.  Its a simple idea that makes code writing in R much easier. 


```r
data <- read_excel("Ihno_dataset.xls") %>% 
  dplyr::rename_all(tolower)              # convert variable names to lower case

data
```

```
# A tibble: 100 x 18
   sub_num gender major reason exp_cond coffee num_cups phobia prevmath
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00     0      1.00     3.00
 2    2.00   1.00  1.00   2.00     1.00   0        0      1.00     4.00
 3    3.00   1.00  1.00   1.00     1.00   0        0      4.00     1.00
 4    4.00   1.00  1.00   1.00     1.00   0        0      4.00     0   
 5    5.00   1.00  1.00   1.00     1.00   0        1.00  10.0      1.00
 6    6.00   1.00  1.00   1.00     2.00   1.00     1.00   4.00     1.00
 7    7.00   1.00  1.00   1.00     2.00   0        0      4.00     2.00
 8    8.00   1.00  1.00   3.00     2.00   1.00     2.00   4.00     1.00
 9    9.00   1.00  1.00   1.00     2.00   0        0      4.00     1.00
10   10.0    1.00  1.00   1.00     2.00   1.00     2.00   5.00     0   
# ... with 90 more rows, and 9 more variables: mathquiz <dbl>, statquiz
#   <dbl>, exp_sqz <dbl>, hr_base <dbl>, hr_pre <dbl>, hr_post <dbl>,
#   anx_base <dbl>, anx_pre <dbl>, anx_post <dbl>
```



### The `head()` Function: Print the First Few Rows

See the first few rows of a dataset by using the `head()` function.  Since it is part for **base R**, I never include the package, but if we did, it would be `utils::head()`.  The default is to print the first SIX rows.


```r
head(data)
```

```
# A tibble: 6 x 18
  sub_num gender major reason exp_cond coffee num_cups phobia prevmath
    <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
1    1.00   1.00  1.00   3.00     1.00   1.00     0      1.00     3.00
2    2.00   1.00  1.00   2.00     1.00   0        0      1.00     4.00
3    3.00   1.00  1.00   1.00     1.00   0        0      4.00     1.00
4    4.00   1.00  1.00   1.00     1.00   0        0      4.00     0   
5    5.00   1.00  1.00   1.00     1.00   0        1.00  10.0      1.00
6    6.00   1.00  1.00   1.00     2.00   1.00     1.00   4.00     1.00
# ... with 9 more variables: mathquiz <dbl>, statquiz <dbl>, exp_sqz
#   <dbl>, hr_base <dbl>, hr_pre <dbl>, hr_post <dbl>, anx_base <dbl>,
#   anx_pre <dbl>, anx_post <dbl>
```


Inside the `head()` function, you can change the default of `n = 6` rows.  You can learn about this and other options in the **Help** tab *search for 'head'*.


```r
utils::head(data, n = 3)
```

```
# A tibble: 3 x 18
  sub_num gender major reason exp_cond coffee num_cups phobia prevmath
    <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
1    1.00   1.00  1.00   3.00     1.00   1.00        0   1.00     3.00
2    2.00   1.00  1.00   2.00     1.00   0           0   1.00     4.00
3    3.00   1.00  1.00   1.00     1.00   0           0   4.00     1.00
# ... with 9 more variables: mathquiz <dbl>, statquiz <dbl>, exp_sqz
#   <dbl>, hr_base <dbl>, hr_pre <dbl>, hr_post <dbl>, anx_base <dbl>,
#   anx_pre <dbl>, anx_post <dbl>
```


```r
head(data, n = 11)
```

```
# A tibble: 11 x 18
   sub_num gender major reason exp_cond coffee num_cups phobia prevmath
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00     0      1.00     3.00
 2    2.00   1.00  1.00   2.00     1.00   0        0      1.00     4.00
 3    3.00   1.00  1.00   1.00     1.00   0        0      4.00     1.00
 4    4.00   1.00  1.00   1.00     1.00   0        0      4.00     0   
 5    5.00   1.00  1.00   1.00     1.00   0        1.00  10.0      1.00
 6    6.00   1.00  1.00   1.00     2.00   1.00     1.00   4.00     1.00
 7    7.00   1.00  1.00   1.00     2.00   0        0      4.00     2.00
 8    8.00   1.00  1.00   3.00     2.00   1.00     2.00   4.00     1.00
 9    9.00   1.00  1.00   1.00     2.00   0        0      4.00     1.00
10   10.0    1.00  1.00   1.00     2.00   1.00     2.00   5.00     0   
11   11.0    1.00  1.00   1.00     2.00   0        1.00   5.00     1.00
# ... with 9 more variables: mathquiz <dbl>, statquiz <dbl>, exp_sqz
#   <dbl>, hr_base <dbl>, hr_pre <dbl>, hr_post <dbl>, anx_base <dbl>,
#   anx_pre <dbl>, anx_post <dbl>
```


### The `names()` Function: List the Variable Names

Another helpful function is `names()` which lists out the names of the **variables**.  This is nice to use to copy-paste later on, since...in R code chunks:

* Spelling matters
* Capitalization matters
* Spacing does NOT matter: one space is the same as 100 spaces
* Line enters are ignored


```r
names(data)
```

```
 [1] "sub_num"  "gender"   "major"    "reason"   "exp_cond" "coffee"  
 [7] "num_cups" "phobia"   "prevmath" "mathquiz" "statquiz" "exp_sqz" 
[13] "hr_base"  "hr_pre"   "hr_post"  "anx_base" "anx_pre"  "anx_post"
```



### The `dim()` Function: List the Dimentions

See how many rows *(observation)* and columns *(variables)*


```r
dim(data)
```

```
[1] 100  18
```


### The `tibble::glimpse()` Function: Gives an Overview of Variables

This is a handy function that gives:

* Dimensions (observations and variables)
* Names of variables
* Each variables type, which could be...
  + `dbl` = numeric: double precision floating point numbers
  + `fct` = factor: categorical, either nominal or ordinal
  + `chr` = character: text
* Lists the first few entries


```r
tibble::glimpse(data)
```

```
Observations: 100
Variables: 18
$ sub_num  <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16...
$ gender   <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
$ major    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
$ reason   <dbl> 3, 2, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1,...
$ exp_cond <dbl> 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 3, 4, 4, 4, 4,...
$ coffee   <dbl> 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1,...
$ num_cups <dbl> 0, 0, 0, 0, 1, 1, 0, 2, 0, 2, 1, 0, 1, 2, 3, 0, 0, 3,...
$ phobia   <dbl> 1, 1, 4, 4, 10, 4, 4, 4, 4, 5, 5, 4, 7, 4, 3, 8, 4, 5...
$ prevmath <dbl> 3, 4, 1, 0, 1, 1, 2, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1, 1,...
$ mathquiz <dbl> 43, 49, 26, 29, 31, 20, 13, 23, 38, NA, 29, 32, 18, N...
$ statquiz <dbl> 6, 9, 8, 7, 6, 7, 3, 7, 8, 7, 8, 8, 1, 5, 8, 3, 8, 7,...
$ exp_sqz  <dbl> 7, 11, 8, 8, 6, 6, 4, 7, 7, 6, 10, 7, 3, 4, 6, 1, 7, ...
$ hr_base  <dbl> 71, 73, 69, 72, 71, 70, 71, 77, 73, 78, 74, 73, 73, 7...
$ hr_pre   <dbl> 68, 75, 76, 73, 83, 71, 70, 87, 72, 76, 72, 74, 76, 8...
$ hr_post  <dbl> 65, 68, 72, 78, 74, 76, 66, 84, 67, 74, 73, 74, 78, 7...
$ anx_base <dbl> 17, 17, 19, 19, 26, 12, 12, 17, 20, 20, 21, 32, 19, 1...
$ anx_pre  <dbl> 22, 19, 14, 13, 30, 15, 16, 19, 14, 24, 25, 35, 23, 2...
$ anx_post <dbl> 20, 16, 15, 16, 25, 19, 17, 22, 17, 19, 22, 33, 20, 2...
```



### The `dplyr::select()` Function: Specify VARIABLES to include/keep

This function chooses which **variables** to include, excluding all others not given between the `()`.


```r
data %>% 
  dplyr::select(sub_num, gender, major, reason, exp_cond, coffee)
```

```
# A tibble: 100 x 6
   sub_num gender major reason exp_cond coffee
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00
 2    2.00   1.00  1.00   2.00     1.00   0   
 3    3.00   1.00  1.00   1.00     1.00   0   
 4    4.00   1.00  1.00   1.00     1.00   0   
 5    5.00   1.00  1.00   1.00     1.00   0   
 6    6.00   1.00  1.00   1.00     2.00   1.00
 7    7.00   1.00  1.00   1.00     2.00   0   
 8    8.00   1.00  1.00   3.00     2.00   1.00
 9    9.00   1.00  1.00   1.00     2.00   0   
10   10.0    1.00  1.00   1.00     2.00   1.00
# ... with 90 more rows
```



### The `dplyr::filter()` Function: Specify OBSERVATIONS to include/keep

This function chooses which **observations** to include, excluding all others not given between the `()`.


```r
data %>% 
  dplyr::filter(gender == 1)
```

```
# A tibble: 57 x 18
   sub_num gender major reason exp_cond coffee num_cups phobia prevmath
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00     0      1.00     3.00
 2    2.00   1.00  1.00   2.00     1.00   0        0      1.00     4.00
 3    3.00   1.00  1.00   1.00     1.00   0        0      4.00     1.00
 4    4.00   1.00  1.00   1.00     1.00   0        0      4.00     0   
 5    5.00   1.00  1.00   1.00     1.00   0        1.00  10.0      1.00
 6    6.00   1.00  1.00   1.00     2.00   1.00     1.00   4.00     1.00
 7    7.00   1.00  1.00   1.00     2.00   0        0      4.00     2.00
 8    8.00   1.00  1.00   3.00     2.00   1.00     2.00   4.00     1.00
 9    9.00   1.00  1.00   1.00     2.00   0        0      4.00     1.00
10   10.0    1.00  1.00   1.00     2.00   1.00     2.00   5.00     0   
# ... with 47 more rows, and 9 more variables: mathquiz <dbl>, statquiz
#   <dbl>, exp_sqz <dbl>, hr_base <dbl>, hr_pre <dbl>, hr_post <dbl>,
#   anx_base <dbl>, anx_pre <dbl>, anx_post <dbl>
```

You can combine steps to multiple things.  The steps are completed in the order we read: top to bottom, left to right.


```r
data %>% 
  dplyr::select(sub_num, gender, major, reason, exp_cond, coffee) %>% 
  dplyr::filter(gender == 1)
```

```
# A tibble: 57 x 6
   sub_num gender major reason exp_cond coffee
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00
 2    2.00   1.00  1.00   2.00     1.00   0   
 3    3.00   1.00  1.00   1.00     1.00   0   
 4    4.00   1.00  1.00   1.00     1.00   0   
 5    5.00   1.00  1.00   1.00     1.00   0   
 6    6.00   1.00  1.00   1.00     2.00   1.00
 7    7.00   1.00  1.00   1.00     2.00   0   
 8    8.00   1.00  1.00   3.00     2.00   1.00
 9    9.00   1.00  1.00   1.00     2.00   0   
10   10.0    1.00  1.00   1.00     2.00   1.00
# ... with 47 more rows
```


-----------------------------------------

## DATA WRANGLING


### The `dplyr::mutate()` Function: Create a New Variable

Just like radiation may cause a fish to grow an additional eye (a mutation), the `mutate()` function grows a new variable.


```r
data %>% 
  dplyr::mutate(test = 1) %>% 
  dplyr::select(sub_num, gender, mathquiz, statquiz, test) %>% 
  head()
```

```
# A tibble: 6 x 5
  sub_num gender mathquiz statquiz  test
    <dbl>  <dbl>    <dbl>    <dbl> <dbl>
1    1.00   1.00     43.0     6.00  1.00
2    2.00   1.00     49.0     9.00  1.00
3    3.00   1.00     26.0     8.00  1.00
4    4.00   1.00     29.0     7.00  1.00
5    5.00   1.00     31.0     6.00  1.00
6    6.00   1.00     20.0     7.00  1.00
```




### The `factor()` Function: Define Categorical Variables

We will be providing this function with three pieces of information:

(@) The name of an existing variable
(@) A *concatinated* set of numerical `levels`
(@) A *concatinated* set of textual `labels`

> You must include the SAME number of levels and labels.  The ORDER in the sets designates how the labels will be applied to the levels.

Here is how it looks to create ONE new factor.  Notice I added the letter `F` to designate that this new variable is a factor.  


```r
data %>% 
  dplyr::mutate(genderF = factor(gender,
                                 levels = c(1, 2),
                                 labels = c("Female", "Male"))) 
```

```
# A tibble: 100 x 19
   sub_num gender major reason exp_cond coffee num_cups phobia prevmath
     <dbl>  <dbl> <dbl>  <dbl>    <dbl>  <dbl>    <dbl>  <dbl>    <dbl>
 1    1.00   1.00  1.00   3.00     1.00   1.00     0      1.00     3.00
 2    2.00   1.00  1.00   2.00     1.00   0        0      1.00     4.00
 3    3.00   1.00  1.00   1.00     1.00   0        0      4.00     1.00
 4    4.00   1.00  1.00   1.00     1.00   0        0      4.00     0   
 5    5.00   1.00  1.00   1.00     1.00   0        1.00  10.0      1.00
 6    6.00   1.00  1.00   1.00     2.00   1.00     1.00   4.00     1.00
 7    7.00   1.00  1.00   1.00     2.00   0        0      4.00     2.00
 8    8.00   1.00  1.00   3.00     2.00   1.00     2.00   4.00     1.00
 9    9.00   1.00  1.00   1.00     2.00   0        0      4.00     1.00
10   10.0    1.00  1.00   1.00     2.00   1.00     2.00   5.00     0   
# ... with 90 more rows, and 10 more variables: mathquiz <dbl>, statquiz
#   <dbl>, exp_sqz <dbl>, hr_base <dbl>, hr_pre <dbl>, hr_post <dbl>,
#   anx_base <dbl>, anx_pre <dbl>, anx_post <dbl>, genderF <fct>
```

Notice that the dataset the is printed includes our new variable at the **END**.

You can use the `pipe` to chain several mutate steps together.  I have also assigned the resulting dataset with the five new factor variables at the end to a new name, `dataF`.  Since this code chunk includes a single assignment, there is no output created.

> Remember to include a PIPE between all your steps, but not at the end!


```r
dataF <- data %>% 
  dplyr::mutate(genderF = factor(gender, 
                                 levels = c(1, 2),
                                 labels = c("Female", 
                                            "Male"))) %>% 
  dplyr::mutate(majorF = factor(major, 
                                levels = c(1, 2, 3, 4,5),
                                labels = c("Psychology",
                                           "Premed",
                                           "Biology",
                                           "Sociology",
                                           "Economics"))) %>% 
  dplyr::mutate(reasonF = factor(reason,
                                 levels = c(1, 2, 3),
                                 labels = c("Program requirement",
                                            "Personal interest",
                                            "Advisor recommendation"))) %>% 
  dplyr::mutate(exp_condF = factor(exp_cond,
                                   levels = c(1, 2, 3, 4),
                                   labels = c("Easy",
                                              "Moderate",
                                              "Difficult",
                                              "Impossible"))) %>% 
  dplyr::mutate(coffeeF = factor(coffee,
                                 levels = c(0, 1),
                                 labels = c("Not a regular coffee drinker",
                                            "Regularly drinks coffee"))) 
```

See how the new variables are added at the end.


```r
glimpse(data)
```

```
Observations: 100
Variables: 18
$ sub_num  <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16...
$ gender   <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
$ major    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
$ reason   <dbl> 3, 2, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1,...
$ exp_cond <dbl> 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 3, 4, 4, 4, 4,...
$ coffee   <dbl> 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1,...
$ num_cups <dbl> 0, 0, 0, 0, 1, 1, 0, 2, 0, 2, 1, 0, 1, 2, 3, 0, 0, 3,...
$ phobia   <dbl> 1, 1, 4, 4, 10, 4, 4, 4, 4, 5, 5, 4, 7, 4, 3, 8, 4, 5...
$ prevmath <dbl> 3, 4, 1, 0, 1, 1, 2, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1, 1,...
$ mathquiz <dbl> 43, 49, 26, 29, 31, 20, 13, 23, 38, NA, 29, 32, 18, N...
$ statquiz <dbl> 6, 9, 8, 7, 6, 7, 3, 7, 8, 7, 8, 8, 1, 5, 8, 3, 8, 7,...
$ exp_sqz  <dbl> 7, 11, 8, 8, 6, 6, 4, 7, 7, 6, 10, 7, 3, 4, 6, 1, 7, ...
$ hr_base  <dbl> 71, 73, 69, 72, 71, 70, 71, 77, 73, 78, 74, 73, 73, 7...
$ hr_pre   <dbl> 68, 75, 76, 73, 83, 71, 70, 87, 72, 76, 72, 74, 76, 8...
$ hr_post  <dbl> 65, 68, 72, 78, 74, 76, 66, 84, 67, 74, 73, 74, 78, 7...
$ anx_base <dbl> 17, 17, 19, 19, 26, 12, 12, 17, 20, 20, 21, 32, 19, 1...
$ anx_pre  <dbl> 22, 19, 14, 13, 30, 15, 16, 19, 14, 24, 25, 35, 23, 2...
$ anx_post <dbl> 20, 16, 15, 16, 25, 19, 17, 22, 17, 19, 22, 33, 20, 2...
```

```r
glimpse(dataF)
```

```
Observations: 100
Variables: 23
$ sub_num   <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 1...
$ gender    <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
$ major     <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
$ reason    <dbl> 3, 2, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1...
$ exp_cond  <dbl> 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 3, 4, 4, 4, 4...
$ coffee    <dbl> 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 1...
$ num_cups  <dbl> 0, 0, 0, 0, 1, 1, 0, 2, 0, 2, 1, 0, 1, 2, 3, 0, 0, 3...
$ phobia    <dbl> 1, 1, 4, 4, 10, 4, 4, 4, 4, 5, 5, 4, 7, 4, 3, 8, 4, ...
$ prevmath  <dbl> 3, 4, 1, 0, 1, 1, 2, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1, 1...
$ mathquiz  <dbl> 43, 49, 26, 29, 31, 20, 13, 23, 38, NA, 29, 32, 18, ...
$ statquiz  <dbl> 6, 9, 8, 7, 6, 7, 3, 7, 8, 7, 8, 8, 1, 5, 8, 3, 8, 7...
$ exp_sqz   <dbl> 7, 11, 8, 8, 6, 6, 4, 7, 7, 6, 10, 7, 3, 4, 6, 1, 7,...
$ hr_base   <dbl> 71, 73, 69, 72, 71, 70, 71, 77, 73, 78, 74, 73, 73, ...
$ hr_pre    <dbl> 68, 75, 76, 73, 83, 71, 70, 87, 72, 76, 72, 74, 76, ...
$ hr_post   <dbl> 65, 68, 72, 78, 74, 76, 66, 84, 67, 74, 73, 74, 78, ...
$ anx_base  <dbl> 17, 17, 19, 19, 26, 12, 12, 17, 20, 20, 21, 32, 19, ...
$ anx_pre   <dbl> 22, 19, 14, 13, 30, 15, 16, 19, 14, 24, 25, 35, 23, ...
$ anx_post  <dbl> 20, 16, 15, 16, 25, 19, 17, 22, 17, 19, 22, 33, 20, ...
$ genderF   <fct> Female, Female, Female, Female, Female, Female, Fema...
$ majorF    <fct> Psychology, Psychology, Psychology, Psychology, Psyc...
$ reasonF   <fct> Advisor recommendation, Personal interest, Program r...
$ exp_condF <fct> Easy, Easy, Easy, Easy, Easy, Moderate, Moderate, Mo...
$ coffeeF   <fct> Regularly drinks coffee, Not a regular coffee drinke...
```




--------------------------------


## CREATING NEW VARIABLES: Assignment 0

### Question 2: Create a new variable = `mathquiz` + 50



```r
data2 <- dataF %>% 
  dplyr::mutate(mathquiz_p50 = mathquiz + 50) 
```



```r
data2 %>% 
  dplyr::select(sub_num, mathquiz, mathquiz_p50)
```

```
# A tibble: 100 x 3
   sub_num mathquiz mathquiz_p50
     <dbl>    <dbl>        <dbl>
 1    1.00     43.0         93.0
 2    2.00     49.0         99.0
 3    3.00     26.0         76.0
 4    4.00     29.0         79.0
 5    5.00     31.0         81.0
 6    6.00     20.0         70.0
 7    7.00     13.0         63.0
 8    8.00     23.0         73.0
 9    9.00     38.0         88.0
10   10.0      NA           NA  
# ... with 90 more rows
```



### Question 3: Create a new variable = `Hr_base` / 60


```r
data3 <- data2 %>% 
  dplyr::mutate(hr_base_bps = hr_base / 60) 
```



```r
data3 %>% 
  dplyr::select(sub_num, hr_base, hr_base_bps) 
```

```
# A tibble: 100 x 3
   sub_num hr_base hr_base_bps
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
# ... with 90 more rows
```


### Question 4a: Create a new variable  = `Statquiz` + 2, then * 10



```r
data4a <- data3 %>% 
  dplyr::mutate(statquiz_4a = (statquiz + 2) * 10 )
```


### Question 4b: Create a new variable  = `Statquiz` * 10, then + 2


```r
data4b <- data4a %>% 
  dplyr::mutate(statquiz_4b = (statquiz * 10) + 2 )
```


```r
data4b %>% 
  dplyr::select(sub_num, statquiz, statquiz_4a, statquiz_4b) 
```

```
# A tibble: 100 x 4
   sub_num statquiz statquiz_4a statquiz_4b
     <dbl>    <dbl>       <dbl>       <dbl>
 1    1.00     6.00        80.0        62.0
 2    2.00     9.00       110          92.0
 3    3.00     8.00       100          82.0
 4    4.00     7.00        90.0        72.0
 5    5.00     6.00        80.0        62.0
 6    6.00     7.00        90.0        72.0
 7    7.00     3.00        50.0        32.0
 8    8.00     7.00        90.0        72.0
 9    9.00     8.00       100          82.0
10   10.0      7.00        90.0        72.0
# ... with 90 more rows
```



### Question 5a: Create a new variable = `sum` of the 3 anxiety measures 

Here are three ways you may try to find the sum.  The middle way does not perform the action we want.  The first way works fine, unless there is some missing data.


```r
data5a <- data4b %>% 
  dplyr::mutate(anx_plus    =         anx_base + anx_pre + anx_post)  %>%  # works, missing??
  dplyr::mutate(anx_sum     =     sum(anx_base,  anx_pre,  anx_post)) %>%  # does NOT work
  dplyr::mutate(anx_rowsums = rowsums(anx_base,  anx_pre,  anx_post))      # best way
```




```r
data5a %>% 
  dplyr::select(sub_num, 
                anx_base, anx_pre, anx_post, 
                anx_plus, anx_sum, anx_rowsums) 
```

```
# A tibble: 100 x 7
   sub_num anx_base anx_pre anx_post anx_plus anx_sum anx_rowsums
     <dbl>    <dbl>   <dbl>    <dbl>    <dbl>   <dbl>       <dbl>
 1    1.00     17.0    22.0     20.0     59.0    5741        59.0
 2    2.00     17.0    19.0     16.0     52.0    5741        52.0
 3    3.00     19.0    14.0     15.0     48.0    5741        48.0
 4    4.00     19.0    13.0     16.0     48.0    5741        48.0
 5    5.00     26.0    30.0     25.0     81.0    5741        81.0
 6    6.00     12.0    15.0     19.0     46.0    5741        46.0
 7    7.00     12.0    16.0     17.0     45.0    5741        45.0
 8    8.00     17.0    19.0     22.0     58.0    5741        58.0
 9    9.00     20.0    14.0     17.0     51.0    5741        51.0
10   10.0      20.0    24.0     19.0     63.0    5741        63.0
# ... with 90 more rows
```

\clearpage

### Question 5b: Create a new variable = `average` of the 3 heart rates 



```r
data5b <- data5a %>% 
  dplyr::mutate(hr_avg      =         (hr_base + hr_pre + hr_post)/3) %>%  # works,no missings
  dplyr::mutate(hr_rowmeans = rowmeans(hr_base,  hr_pre,  hr_post)) # always works
```



```r
data5b %>% 
  dplyr::select(sub_num, 
                hr_base, hr_pre, hr_post, 
                hr_avg,  hr_rowmeans) 
```

```
# A tibble: 100 x 6
   sub_num hr_base hr_pre hr_post hr_avg hr_rowmeans
     <dbl>   <dbl>  <dbl>   <dbl>  <dbl>       <dbl>
 1    1.00    71.0   68.0    65.0   68.0        68.0
 2    2.00    73.0   75.0    68.0   72.0        72.0
 3    3.00    69.0   76.0    72.0   72.3        72.3
 4    4.00    72.0   73.0    78.0   74.3        74.3
 5    5.00    71.0   83.0    74.0   76.0        76.0
 6    6.00    70.0   71.0    76.0   72.3        72.3
 7    7.00    71.0   70.0    66.0   69.0        69.0
 8    8.00    77.0   87.0    84.0   82.7        82.7
 9    9.00    73.0   72.0    67.0   70.7        70.7
10   10.0     78.0   76.0    74.0   76.0        76.0
# ... with 90 more rows
```

\clearpage

### Question 6: Create a new variable = `Statquiz` minus `Exp_sqz`


```r
data6 <- data5b %>% 
  dplyr::mutate(statDiff = statquiz - exp_sqz)
```


```r
data6 %>% 
  dplyr::select(sub_num, exp_cond, exp_condF,
                statquiz, exp_sqz, statDiff) 
```

```
# A tibble: 100 x 6
   sub_num exp_cond exp_condF statquiz exp_sqz statDiff
     <dbl>    <dbl> <fct>        <dbl>   <dbl>    <dbl>
 1    1.00     1.00 Easy          6.00    7.00    -1.00
 2    2.00     1.00 Easy          9.00   11.0     -2.00
 3    3.00     1.00 Easy          8.00    8.00     0   
 4    4.00     1.00 Easy          7.00    8.00    -1.00
 5    5.00     1.00 Easy          6.00    6.00     0   
 6    6.00     2.00 Moderate      7.00    6.00     1.00
 7    7.00     2.00 Moderate      3.00    4.00    -1.00
 8    8.00     2.00 Moderate      7.00    7.00     0   
 9    9.00     2.00 Moderate      8.00    7.00     1.00
10   10.0      2.00 Moderate      7.00    6.00     1.00
# ... with 90 more rows
```

\clearpage

### Putting it all together


```r
data_clean <- read_excel("Ihno_dataset.xls") %>% 
  dplyr::rename_all(tolower) %>% 
  dplyr::mutate(genderF = factor(gender, 
                                 levels = c(1, 2),
                                 labels = c("Female", 
                                            "Male"))) %>% 
  dplyr::mutate(majorF = factor(major, 
                                levels = c(1, 2, 3, 4,5),
                                labels = c("Psychology",
                                           "Premed",
                                           "Biology",
                                           "Sociology",
                                           "Economics"))) %>% 
  dplyr::mutate(reasonF = factor(reason,
                                 levels = c(1, 2, 3),
                                 labels = c("Program requirement",
                                            "Personal interest",
                                            "Advisor recommendation"))) %>% 
  dplyr::mutate(exp_condF = factor(exp_cond,
                                   levels = c(1, 2, 3, 4),
                                   labels = c("Easy",
                                              "Moderate",
                                              "Difficult",
                                              "Impossible"))) %>% 
  dplyr::mutate(coffeeF = factor(coffee,
                                 levels = c(0, 1),
                                 labels = c("Not a regular coffee drinker",
                                            "Regularly drinks coffee")))  %>% 
  dplyr::mutate(mathquiz_p50 = mathquiz + 50) %>% 
  dplyr::mutate(hr_base_bps  = hr_base / 60) %>% 
  dplyr::mutate(statquiz_4a  = (statquiz + 2) * 10 ) %>% 
  dplyr::mutate(statquiz_4b  = (statquiz * 10) + 2 ) %>% 
  dplyr::mutate(anx_sum     = rowsums(anx_base, anx_pre, anx_post)) %>% 
  dplyr::mutate(hr_mean       = rowmeans(hr_base + hr_pre + hr_post)) %>% 
  dplyr::mutate(statDiff     = statquiz - exp_sqz)

glimpse(data_clean)
```

```
Observations: 100
Variables: 30
$ sub_num      <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15...
$ gender       <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
$ major        <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1...
$ reason       <dbl> 3, 2, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 3, 1, 1, 1...
$ exp_cond     <dbl> 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 3, 4, 4, 4...
$ coffee       <dbl> 1, 0, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0...
$ num_cups     <dbl> 0, 0, 0, 0, 1, 1, 0, 2, 0, 2, 1, 0, 1, 2, 3, 0, 0...
$ phobia       <dbl> 1, 1, 4, 4, 10, 4, 4, 4, 4, 5, 5, 4, 7, 4, 3, 8, ...
$ prevmath     <dbl> 3, 4, 1, 0, 1, 1, 2, 1, 1, 0, 1, 0, 0, 1, 1, 0, 1...
$ mathquiz     <dbl> 43, 49, 26, 29, 31, 20, 13, 23, 38, NA, 29, 32, 1...
$ statquiz     <dbl> 6, 9, 8, 7, 6, 7, 3, 7, 8, 7, 8, 8, 1, 5, 8, 3, 8...
$ exp_sqz      <dbl> 7, 11, 8, 8, 6, 6, 4, 7, 7, 6, 10, 7, 3, 4, 6, 1,...
$ hr_base      <dbl> 71, 73, 69, 72, 71, 70, 71, 77, 73, 78, 74, 73, 7...
$ hr_pre       <dbl> 68, 75, 76, 73, 83, 71, 70, 87, 72, 76, 72, 74, 7...
$ hr_post      <dbl> 65, 68, 72, 78, 74, 76, 66, 84, 67, 74, 73, 74, 7...
$ anx_base     <dbl> 17, 17, 19, 19, 26, 12, 12, 17, 20, 20, 21, 32, 1...
$ anx_pre      <dbl> 22, 19, 14, 13, 30, 15, 16, 19, 14, 24, 25, 35, 2...
$ anx_post     <dbl> 20, 16, 15, 16, 25, 19, 17, 22, 17, 19, 22, 33, 2...
$ genderF      <fct> Female, Female, Female, Female, Female, Female, F...
$ majorF       <fct> Psychology, Psychology, Psychology, Psychology, P...
$ reasonF      <fct> Advisor recommendation, Personal interest, Progra...
$ exp_condF    <fct> Easy, Easy, Easy, Easy, Easy, Moderate, Moderate,...
$ coffeeF      <fct> Regularly drinks coffee, Not a regular coffee dri...
$ mathquiz_p50 <dbl> 93, 99, 76, 79, 81, 70, 63, 73, 88, NA, 79, 82, 6...
$ hr_base_bps  <dbl> 1.183333, 1.216667, 1.150000, 1.200000, 1.183333,...
$ statquiz_4a  <dbl> 80, 110, 100, 90, 80, 90, 50, 90, 100, 90, 100, 1...
$ statquiz_4b  <dbl> 62, 92, 82, 72, 62, 72, 32, 72, 82, 72, 82, 82, 1...
$ anx_sum      <dbl> 59, 52, 48, 48, 81, 46, 45, 58, 51, 63, 68, 100, ...
$ hr_mean      <dbl> 204, 216, 217, 223, 228, 217, 207, 248, 212, 228,...
$ statDiff     <dbl> -1, -2, 0, -1, 0, 1, -1, 0, 1, 1, -2, 1, -2, 1, 2...
```




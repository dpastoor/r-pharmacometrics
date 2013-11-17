Core R
========================================================

The objectives of this section is to take a number of concepts that you use frequently but may have not questioned the 'why' that R behaves that way. 

The overarching theme in this documentation is to "concisely" present the concept in a way to help you to think "in terms of R" rather than trying to memorize patterns. This will be supplemented by examples to help reinforce the concepts and help you on your journey to become an R-ninja.

To set the stage, a brief history of R can put into context many of the decisions to how R behaves.



## Data Structures

R has a number of ways of storing information. The quick way to visualize the possibilities is as such:

|    | Homogeneous    | Heterogeneous |
|----|---------------|--------------|
| 1d | Atomic vector | List         |
| 2d | Matrix        | Data frame   |
| nd | Array         |              |

**Homogenous** - all elements must be of the same type (mode)
**Heterogeneous** - elements can be of different type (mode)

A **Type/Mode** indicates how R stores the information in memory
* numeric
* double
* integer
* logical
* character
* list of pointers
* function

###table of examples### (ie page 96 R cookbook)

The term **Mode** and **Type** are virtually interchangeable - from here out we will use the term **Type** as it is more commonly discussed. ('mode' was inhereted mostly from S/S-plus nomenclalature/defintion)

## Vectors

Data structures in R can be boiled down to a Vector. The most basic vector is an atomic vector.

Vectors have 4 key components:
* *contents* - the information
* *type* - what type of information it stores
* *length* - how long it is
* *attributes* - additional metadata

These components can be easily accessed as such:


```r
# example vector
numeric_vector <- c(1, 2, 3)

# access contents by calling the vector by name
numeric_vector
```

```
## [1] 1 2 3
```

```r

# see vector type
typeof(numeric_vector)
```

```
## [1] "double"
```

```r

# check length
length(numeric_vector)
```

```
## [1] 3
```

```r

# see additional attributes
attributes(numeric_vector)
```

```
## NULL
```



There are two useful functions for handling vectors: `is.*` and `as.*`

* `is.*` is a testing function that returns TRUE or FALSE
* `as.*` is a coercion function - it attempts to convert the input to the requested data structure


```r
numeric_vector <- c(1, 2, 3)
typeof(numeric_vector)
```

```
## [1] "double"
```

```r
is.numeric(numeric_vector)  # note is.numeric will return TRUE for both doubles and integers
```

```
## [1] TRUE
```

```r
is.list(numeric_vector)
```

```
## [1] FALSE
```

```r

# coerce to list
numeric_vector <- as.list(numeric_vector)
typeof(numeric_vector)
```

```
## [1] "list"
```


*tidbit* - `is.null` determines whether an Object is empty (has no content). `NULL` is often used to represent objects of zero length and is returned by expressions and functions whose value is undefined.

## Coercion
For homogenous vectors, if you attempt to combine elements of different types, it will pick the class of the first element and coerce all others to that type


```r
c("hello", 1, FALSE)
```

```
## [1] "hello" "1"     "FALSE"
```


Note: If a logical vector is coerced into a numeric TRUE becomes 1 and FALSE becomes 0 - this can be used to 'count' the number of TRUE/FALSES easily using sum()

* vectors can be indexed by position: v[1] refers to the first element of the vector
* vectors can be indexed by multiple positions using c() - v[c(1,2)] will return a subvector the first and second element of 'v'

## Attributes
Attributes are additional metadata about an object. The most common 3 attributes are:
* `names()` - character vector of element names
* `dim()` - the structure of the object 
* `class()` - used to implement an object system (described later)

You can give a vector names in three ways:

* During creation: `x <- c(a = 1, b = 2, c = 3)`
* By modifying a vector in place: `x <- 1:3; names(x) <- c("a", "b", "c")`
* By creating a modifed vector: `x <- setNames(1:3, c("a", "b", "c"))`

`dim()` passes additional structural information to the vector. Higher level data structures are simply atomic vectors with the addition of the dim() attribute.

This is an important characteristic to remember as it can help conceptualize the implications of what will happen if you are trying to coerce a data structure into a different type. 

As vectors are coerced into higher order structures (eg. matrices and arrays) R handles this by default in a column-wise manner.


```r
a <- matrix(1:6)
a
```

```
##      [,1]
## [1,]    1
## [2,]    2
## [3,]    3
## [4,]    4
## [5,]    5
## [6,]    6
```


An element in a matrix can be indexed exactly like an atomic vector 


```r
a <- matrix(1:6)
a[2]
```

```
## [1] 2
```

```r
a[4]
```

```
## [1] 4
```


In addition, R can refer to the dimensionality via: 

**DS[row, column]**


```r
a <- matrix(1:6)
# give first row
a[1, ]
```

```
## [1] 1
```

```r
# give first column
a[, 1]
```

```
## [1] 1 2 3 4 5 6
```


Beyond the 3 common attributes, additional attributes can be assigned; however it is important to note that when a vector is modified most attributes beyond the 3 listed above are lost


```r
conc <- c(9.62, 3.1, 2, 0.3)
attr(conc, "units") <- "ug/mL"
conc
```

```
## [1] 9.62 3.10 2.00 0.30
## attr(,"units")
## [1] "ug/mL"
```

```r
attributes(conc)
```

```
## $units
## [1] "ug/mL"
```

```r
conc <- as.data.frame(conc)
conc
```

```
##   conc
## 1 9.62
## 2 3.10
## 3 2.00
## 4 0.30
```

```r
attributes(conc)
```

```
## $names
## [1] "conc"
## 
## $row.names
## [1] 1 2 3 4
## 
## $class
## [1] "data.frame"
```



## Lists
Lists offer the ability to combine objects of different types. They also separate themselves from atomic vectors as they have the capability of **recursion** - Lists can contain nested lists.


```r
list(list(1:3), list("hello", "there"), TRUE)
```

```
## [[1]]
## [[1]][[1]]
## [1] 1 2 3
## 
## 
## [[2]]
## [[2]][[1]]
## [1] "hello"
## 
## [[2]][[2]]
## [1] "there"
## 
## 
## [[3]]
## [1] TRUE
```


To combine multiple lists into one large list, c() will coerce all lists to vectors and vectors to individual elements then combine them.


```r
str(list(list(1:3), list("hello", "there"), TRUE, 1:3))
```

```
## List of 4
##  $ :List of 1
##   ..$ : int [1:3] 1 2 3
##  $ :List of 2
##   ..$ : chr "hello"
##   ..$ : chr "there"
##  $ : logi TRUE
##  $ : int [1:3] 1 2 3
```

```r
str(c(list(1:3), list("hello", "there"), TRUE, 1:3))
```

```
## List of 7
##  $ : int [1:3] 1 2 3
##  $ : chr "hello"
##  $ : chr "there"
##  $ : logi TRUE
##  $ : int 1
##  $ : int 2
##  $ : int 3
```


Note: As shown in the examples, the structure of an object can be shown with `str`

## Data Frames
The most commonly used method for storing data is the data frame. At its core, a dataframe is a list of equal-length vectors. You can think of it as having the same properties as both a matrix and a list. (This means you can use the properties of both for things like indexing and subsetting)

A couple useful commands for dataframe attributes:
- `names()`
- `colnames()`
- `rownames()`
- `length()`
- `nrow()`
- `ncol()`

You can easily see how the properties of both 1-dimensional structures (list) and 2-dimensional structures (matrix) come into play.


```r
# can initialize with named vectors
df <- data.frame(time = 1:6, conc = c(9.1, 8.5, 7.3, 4.2, 3.8, 2.5), race = "male")
## list-like length
length(df)
```

```
## [1] 3
```

```r
# subset for individual element by index or name like a vector
df[1]
```

```
##   time
## 1    1
## 2    2
## 3    3
## 4    4
## 5    5
## 6    6
```

```r
df["time"]
```

```
##   time
## 1    1
## 2    2
## 3    3
## 4    4
## 5    5
## 6    6
```

```r

## array-like subset by dimension (remember - ds[row, column])
df[1, ]
```

```
##   time conc race
## 1    1  9.1 male
```

```r
colnames(df)
```

```
## [1] "time" "conc" "race"
```

```r
nrow(df)
```

```
## [1] 6
```


## Creation vs Coercion

You can create new data structure with `datastructure()` - ie `data.frame()`
As mentioned previously, you can coerce an object to a different data structure with `as.*` - ie: `as.data.frame()`

An additional note when coercing to data frames:
* a vector will yield a one-column data frame
* a list will yield one column for each element; it's an error if they're not all the same length
* a matrix will yield a data frame with the same number of columns


## Combining Data Structures/Objects
There are a number of ways to combine multiple objects. The simplest are `c()`, `cbind()`, and `rbind()`



```r
time <- 1:6
conc <- c(9.1, 8.5, 7.3, 4.2, 3.8, 2.5)
c(time, conc)
```

```
##  [1] 1.0 2.0 3.0 4.0 5.0 6.0 9.1 8.5 7.3 4.2 3.8 2.5
```

```r
rbind(time, conc)
```

```
##      [,1] [,2] [,3] [,4] [,5] [,6]
## time  1.0  2.0  3.0  4.0  5.0  6.0
## conc  9.1  8.5  7.3  4.2  3.8  2.5
```

```r
cbind(time, conc)
```

```
##      time conc
## [1,]    1  9.1
## [2,]    2  8.5
## [3,]    3  7.3
## [4,]    4  4.2
## [5,]    5  3.8
## [6,]    6  2.5
```


While `cbind()` may seem like an easy option to quickly create df's be careful of coercion:


```r
class(cbind(time, conc))
```

```
## [1] "matrix"
```


This is very important when dealing with coercion


```r
time <- 1:6
conc <- c("9.1", 8.5, 7.3, 4.2, 3.8, 2.5)
cbind(time, conc)
```

```
##      time conc 
## [1,] "1"  "9.1"
## [2,] "2"  "8.5"
## [3,] "3"  "7.3"
## [4,] "4"  "4.2"
## [5,] "5"  "3.8"
## [6,] "6"  "2.5"
```

That seems easy to catch, but what about something like this:


```r
as.data.frame(cbind(time, conc))
```

```
##   time conc
## 1    1  9.1
## 2    2  8.5
## 3    3  7.3
## 4    4  4.2
## 5    5  3.8
## 6    6  2.5
```

It prints out to the console looking like numbers but...


```r
str(as.data.frame(cbind(time, conc)))
```

```
## 'data.frame':	6 obs. of  2 variables:
##  $ time: Factor w/ 6 levels "1","2","3","4",..: 1 2 3 4 5 6
##  $ conc: Factor w/ 6 levels "2.5","3.8","4.2",..: 6 5 4 3 2 1
```

They are actually coerced to a matrix of character factors

This is because cbind will create a matrix unless one of the objects is already a data frame.

The best way to avoid this is to be careful when deciding if you want to *coerce* (as.*) or initialize a new data frame. 

A good habit is to just to use data.frame() directly unless you have good reason for the coercion.


```r
# coerce objects together into a data frame
str(as.data.frame(cbind(time, conc)))
```

```
## 'data.frame':	6 obs. of  2 variables:
##  $ time: Factor w/ 6 levels "1","2","3","4",..: 1 2 3 4 5 6
##  $ conc: Factor w/ 6 levels "2.5","3.8","4.2",..: 6 5 4 3 2 1
```

```r
# instead create new data frame
str(data.frame(time, conc))
```

```
## 'data.frame':	6 obs. of  2 variables:
##  $ time: int  1 2 3 4 5 6
##  $ conc: Factor w/ 6 levels "2.5","3.8","4.2",..: 6 5 4 3 2 1
```

Likewise, the safest way to use cbind() is to ensure all objects are of the same type.

## One last combining catch

That is, what happens if vectors being combined to are of *unequal length*? 

R handles this through something called a *Recycling Rule*.

When R performs operations, it does so element-by-element. When combining multiple vecotrs it does so in pairs. When R reaches the end of the shorter vector it starts over from the first element and keeps filling to the length of the longer vector.

This can be convenient when you want to add a new column with a single value:


```r
id <- 1:6
race <- "caucasian"
data.frame(id, race)
```

```
##   id      race
## 1  1 caucasian
## 2  2 caucasian
## 3  3 caucasian
## 4  4 caucasian
## 5  5 caucasian
## 6  6 caucasian
```


But can be dangerous and lead to unintended behavior:


```r
id <- 1:6
race <- c("caucasian", "black")
data.frame(id, race)
```

```
##   id      race
## 1  1 caucasian
## 2  2     black
## 3  3 caucasian
## 4  4     black
## 5  5 caucasian
## 6  6     black
```



# Factors
Factors in R are a tricky beast and I haven't spent as much time as I'd like writing up this section so I will give the cliffnotes.

* unordered factors cannot be sorted
* to convert a numeric factor back to a numeric use the command `as.numeric(as.character(factor))`
* factors have a couple key arguments when dealing with them
    `levels` - are the values the factor takes
    `labels` - are an optional value of labels that can be used to name the factors

This will be hopefully a good example for us to examine. 


```r
Theoph3 <- Theoph[with(Theoph, as.numeric(as.character(Subject)) < 4),]
within(Theoph3, {id <- factor(Subject, 
                                levels = c(1, 2, 3), 
                                labels = c("John", "Mary", "Joe")
                                )
                id2 <- factor(subnum, 
                                levels = c(1, 2, 3), 
                                labels = c("John", "Mary", "Joe")
                                )
                id3 <- factor(subnum, 
                                levels = c(11, 6, 5), 
                                labels = c("John", "Mary", "Joe")
                                )
                subnum <- as.numeric(Subject)
                subcharnum <- as.numeric(as.character(Subject))
            }

)
```

```
## Error: object 'subnum' not found
```




```r
## generate data
x = factor(sample(letters[1:5], 100, replace = TRUE))

print(levels(x))  ## This will show the levels of x are 'Levels: a b c d e'
```

```
## [1] "a" "b" "c" "d" "e"
```

```r

## To reorder the levels: note, if x is not a factor use levels(factor(x))
x = factor(x, levels(x)[c(4, 5, 1:3)])

print(levels(x))  ## Now 'Levels: d e a b c'
```

```
## [1] "d" "e" "a" "b" "c"
```





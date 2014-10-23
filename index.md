---
title       : "Crash Course Into R"
subtitle    : "A Gentle Introduction"
author      : "Peter von Rohr"
job         : "Charlotte Team"
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## How To Get R

### Download from CRAN
- CRAN - The Comprehensive R Archive Network
http://cran.r-project.org/
- local mirror @ ETH: http://stat.ethz.ch/CRAN/
- precompiled binaries for Linux, Mac OS X and Windows

![screenshot cran website](cran.png)

---

## How To Install R

### Installation

- Run the downloaded binaries
- Get an IDE (Integrated Development Environment) like RStudio http://www.rstudio.com/

![screenshot RStudio website](rstudio.png)

---

## First R Session - Calculator Mode

### Question - Answer - Game with R Interpreter

- simple computations


```r
2 + 3
```

```
## [1] 5
```

- complex numbers


```r
7*(2-3i)
```

```
## [1] 14-21i
```

---

### Assignment of objects (aka variables)


```r
x <- 7;
y <- 5*x;
```
- in general the R interpreter is silent. Output is shown either by entering the object name or by the print() function


```r
x
```

```
## [1] 7
```

```r
print(y)
```

```
## [1] 35
```

---

## First R Session - Functions

- Object creation, e.g. function `vector()` creates vector objects

```r
vn <- vector(mode="numeric",length=2);print(vn)
```

```
## [1] 0 0
```
- modification of an object, e.g. extension

```r
vn <- c(vn,2,-1,3);print(vn)
```

```
## [1]  0  0  2 -1  3
```
__NB__ `c` is better not used as object (variable) name

---

### Help System in R

- getting help with the `help()` function
```
help("vector")
```

- Use function `apropos()`, if not sure about function name

```r
apropos("ecto")
```

```
## [1] ".__C__vector"         "as.data.frame.vector" "as.vector"           
## [4] "as.vector.factor"     "getSrcDirectory"      "is.vector"           
## [7] "vector"               "Vectorize"
```

- Documentation section on http://r-project.org
- Go to http://r-seek.org or http://Rdocumentation.org

---

## Extending Functionality of R
Add-on packages extend the functionality of R

- Function `install.packages()` downloads and installs a package, e.g., the command
```
install.packages("VLMC")
```
would download and install a package called `VLMC` from CRAN 

- list of all packages that are installed is obtained by 
```
installed.packages()
```

---

## Basic Datatypes
Six Basic Datatypes

1. `numeric`: real numbers, default for numbers in R
2. `integer`: ...
3. `complex`: negative square roots
4. `logical`: boolean TRUE and FALSE
5. `character`: ...
6. `factor`: special case for fixed effect levels in modelling

---

### Please note the following points on datatypes

- R is very liberal about datatypes
- no strong typing, that means objects are not declared what datatypes they are
- R does a lot of conversion between datatypes (called coersion in R) behind the scence. 
- Coersion comes clearly as a curse and as a blessing - on the one side it is very convenient for the user, but on the other side it can also be the source of bugs which are very difficult to find
- Function `class()` returns the datatype of an object
- Functions `is.<data.type>` can be used to check whether an object is of a given datatype, e.g., `is.integer()`
- Functions `as.<datatype>` can be used to explicitly convert to a datatype, e.g., `as.character()`

---

### Special note on integer
- Unlike other languages, for R the numbers `5` and `5.0` are the same
- By default all numbers are `numeric` which correspond to floating point numbers. Hence

```r
is.integer(5)
```

```
## [1] FALSE
```
- This has consequences for equality testing between numbers. Because most floating point numbers cannot be
 represented exactly, the following result is obtained

```r
a <- sqrt(2);a * a == 2
```

```
## [1] FALSE
```
(See FAQ 7.31 http://cran.r-project.org/doc/FAQ/R-FAQ.html on equality of numbers)

- Function `as.integer()` creates an integer

---

## Composed Datatypes - Vector
Vectors - Definition and Creation
- a `vector` is a sequence of data elements of the same basic type
- data elements in a vector are called `components` or members
- vectors are created by the function `vector()` which takes as argument the mode corresponding to the basic type of the members and the length of the vector.

```r
ve <- vector(mode="logical",length=0) # empty vector of logicals
print(ve)
```

```
## logical(0)
```

```r
vn <- vector(mode="numeric",length=2) # numeric
print(vn)
```

```
## [1] 0 0
```

---

### Vector Operations
- vectors are extended by the concatenate function `c()`

```r
vn <- c(2,3,5);print(vn)
```

```
## [1] 2 3 5
```

```r
vn <- c(vn,10,15,19);print(vn)
```

```
## [1]  2  3  5 10 15 19
```

```r
vc <- c("aa","bb","ba")
vc <- c(vn,vc);print(vc)
```

```
## [1] "2"  "3"  "5"  "10" "15" "19" "aa" "bb" "ba"
```

---

### Properties of a Vector
- the number of members in a vector is determined by

```r
length(vn)
```

```
## [1] 6
```
NB: testing whether a vector is empty can be done with 

```r
length(vn) == 0;length(ve) == 0
```

```
## [1] FALSE
```

```
## [1] TRUE
```

---

### Please note 
- When combining vectors with members of different basic types, R does `type coersion` in most cases without further notice. 
- Combining vectors `vn` and `vc`

```r
vn <- c(2,3,5)
vc <- c("aa","bb","ba")
vc <- c(vn,vc);print(vc)
```

```
## [1] "2"  "3"  "5"  "aa" "bb" "ba"
```
makes R coerce all members of the result into characters

---

### Vector Logical Operations
- Logical or Boolean operations on vectors are done element-wise
- Results of logical operations on vectors are vectors of logicals of the same length as the original vector


```r
a <- c(33,5,7,13,-1)
a > 5
```

```
## [1]  TRUE FALSE  TRUE  TRUE FALSE
```

---

### Vector Arithmetics
Arithmetic operations on vectors are performed element-wise

```r
a <- c(3,5,7,13);b <- c(2,6,4,1)
a+b;a-b
```

```
## [1]  5 11 11 14
```

```
## [1]  1 -1  3 12
```

```r
7*a;a*b;a/b
```

```
## [1] 21 35 49 91
```

```
## [1]  6 30 28 13
```

```
## [1]  1.5000  0.8333  1.7500 13.0000
```

---

### Crossproduct between two vectors
- In R multiplication between two vectors is done element-wise, unlike other systems like Matlab

- The crossproduct between two vectors is obtained by

```r
crossprod(a,b)
```

```
##      [,1]
## [1,]   77
```

---

### Please note
When doing arithmetic computations on vectors of different lengths, R `recycles` the shorter vector, that means the shorter vector is concatenated as many times until its length fits the length of the longer vector

```r
bShort <- b[1:2]
a + bShort
```

```
## [1]  5 11  9 19
```
In case the length of the longer vector is not a multiple of the length of the shorter vector, R still recycles the shorter vector and it produces a `warning` on the console

---

### Vector Member Access
Members or components of a vector can be accessed in three different ways

1. numeric index
2. index vector of logicals
3. names

---

### Vector Member Access Via Numeric Index
- vector elements are accessed by specifying the index in square brackets

```r
vs <- c("a","vector","of","strings")
vs[3]
```

```
## [1] "of"
```
- a negative index of `-i` removes the `i-th` element

```r
vs[-2]
```

```
## [1] "a"       "of"      "strings"
```

---

### Vector Member Access Via Logical Index
- Vector elements are accessed by specifying a vector of logicals with the same length as the original vector in square brackets

```r
vs <- c("a","vector","of","strings")
vl <- c(TRUE,FALSE,TRUE,TRUE)
vs[vl]
```

```
## [1] "a"       "of"      "strings"
```

- combined with logical operations

```r
vs[nchar(vs) > 2]
```

```
## [1] "vector"  "strings"
```
returns all words longer than two characters

---

### Vector Member Access Via Names
Vector elements are accessed by specifying names, provided the vector was assigned names before

```r
vaddress <- c("Mary","Poppins",
              "Wonderstreet","Wondertown")
names(vaddress) <- c("First","Last",
                     "Street","Town")
vaddress["Last"]
```

```
##      Last 
## "Poppins"
```

```r
vaddress[c("First","Town")]
```

```
##        First         Town 
##       "Mary" "Wondertown"
```

---

## Composed Datatypes - Matrix
- Matrices are two-dimensional objects with components organized in rows and columns
- In R a matrix is constructed using function `matrix()`

```r
mA <- matrix(c(3,2,55,23,4,511),nrow=2,ncol=3,
             byrow=TRUE)
mA
```

```
##      [,1] [,2] [,3]
## [1,]    3    2   55
## [2,]   23    4  511
```
where `nrow` and `ncol` specify the number of rows and the number of columns. 
- Setting `byrow=TRUE` fills the matrix row-wise

---

### Matrix Element Access
Matrix elements are accessed analougously to vectors for index numbers and names

```r
mA[2,2]
```

```
## [1] 4
```

```r
dimnames(mA) <- list(c("row1","row2"),
                     c("col1","col2","col3"))
mA;mA["row1","col2"]
```

```
##      col1 col2 col3
## row1    3    2   55
## row2   23    4  511
```

```
## [1] 2
```

---

### Matrix Row or Column Access
- row access

```r
mA[2,]
```

```
## col1 col2 col3 
##   23    4  511
```
- column access

```r
mA[,1]
```

```
## row1 row2 
##    3   23
```

---

### Matrix Modifications
- row-wise extension

```r
mB <- matrix(c(3,5,-43), nrow=1);rbind(mA,mB) # extension by 1 row
```

```
##      col1 col2 col3
## row1    3    2   55
## row2   23    4  511
##         3    5  -43
```
- column-wise extension

```r
mC <- matrix(c(6,2), ncol=1);cbind(mA,mC) # extension by 1 column
```

```
##      col1 col2 col3  
## row1    3    2   55 6
## row2   23    4  511 2
```

---

### Matrix deconstruction
conversion of matrix into a vector

```r
c(mA)
```

```
## [1]   3  23   2   4  55 511
```

---

### Matrix Operations
- transpose

```r
t(mA)
```

```
##      row1 row2
## col1    3   23
## col2    2    4
## col3   55  511
```
- cholesky

```r
mMat <- matrix(c(5,1,1,3),2,2);chol(mMat)
```

```
##       [,1]   [,2]
## [1,] 2.236 0.4472
## [2,] 0.000 1.6733
```

---

## Composed Datatpes - List
- A `list`is an object containing an ordered collection of objects which are called the `components` of the list
- Components need not be of the same type

```r
lst <- list(n = c(5,-7,1), s = c("Fred","Mary"), l = c(TRUE,TRUE,FALSE))
```
- slicing a list using single brackets `[]`

```r
lst[2]
```

```
## $s
## [1] "Fred" "Mary"
```
returns a new list with the second component of `lst`

---

### Accessing Components of a List
- double brackets `[[]]` are used to access components of a list

```r
lst[[2]]
```

```
## [1] "Fred" "Mary"
```

- modification of a list component

```r
lst[[1]][2] <- 43;lst[1]
```

```
## $n
## [1]  5 43  1
```

---

### Access of list components by name
- slicing a list by name

```r
lst["s"]
```

```
## $s
## [1] "Fred" "Mary"
```

- component access

```r
lst$s
```

```
## [1] "Fred" "Mary"
```

---

## Special List - Data Frame
- A `data frame` is a list of vectors all of the same length
- Construction using function `data.frame()`

```r
daFr <- data.frame(nums = c(2,-12), strs = c("Alice","Bob"), bools = c(TRUE,FALSE)) 
```
- access can be via indices or via names

```r
daFr[2,1]; daFr$bools
```

```
## [1] -12
```

```
## [1]  TRUE FALSE
```

---

### R has built-in data frames

```r
head(mtcars, n = 3)
```

```
##                mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4     21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag 21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710    22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
```
- Top line is denoted `header`, it is obtained via function `colnames()`

```r
colnames(mtcars)
```

```
##  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
## [11] "carb"
```
- Each line after the header is called a data row

---

- left most column contains row names

```r
head(rownames(mtcars), n = 3)
```

```
## [1] "Mazda RX4"     "Mazda RX4 Wag" "Datsun 710"
```
- number of rows and columns are obtained by `nrow()` and `ncol()` or by the `dim()` 

```r
nrow(mtcars);ncol(mtcars)
```

```
## [1] 32
```

```
## [1] 11
```

```r
dim(mtcars)
```

```
## [1] 32 11
```

---

### Data Frame Column Vector
- Since a data frame is a special list, access can be done as in lists, e.g., by column names

```r
head(mtcars$mpg, n = 3)
```

```
## [1] 21.0 21.0 22.8
```
- data frames also have properties of matrices and therefore access can also be done via index names

```r
mtcars["Valiant","gear"]
```

```
## [1] 3
```


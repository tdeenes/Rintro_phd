# Az R alapobjektumai

- alapobjektum: vektor
    - alaposztályok: numeric, logical, integer, complex, character, list, expression, raw (az utolsó nagyon ritkán kell)
    - a vektor csak azonos alaposztályú elemeket tartalmazhat, kivéve a list
- alap nyelvi objektum: függvény (function)
    - standard használat: function_name(argument1, argument2)
- az objektumoknak lehetnek attribútumai (`?attributes`):
    - név (`names`, `dimnames`)  
    - dimenzió (`dim`)   
    - osztály (`class`)    
    - egyedi (user-defined) attribútum

### Vektor létrehozása

```r
vec <- c(1, 3, 6, 10)
vec
```

```
## [1]  1  3  6 10
```

```r
# ha integer-t szeretnél, írj a szám után egy L betűt
int <- 1L
str(int) # a str() nagyon hasznos, lasd később
```

```
##  int 1
```

```r
num <- 1
str(num)
```

```
##  num 1
```

- sorozat

```r
upvec <- 10:16 # ez integer, hiába nincsen utána L
upvec
```

```
## [1] 10 11 12 13 14 15 16
```

```r
downvec <- 16:10
downvec
```

```
## [1] 16 15 14 13 12 11 10
```

- vektor nevekkel

```r
vec <- c(first = 1, second = 3, third = 6, fourth = 10)
vec
```

```
##  first second  third fourth 
##      1      3      6     10
```

### Függvény létrehozása

- hozzunk létre egy függvényt, amelyik elemenként összead két numerikus vektort

```r
simpleAdd <- function(x, y) x + y
```

- bonyolultabbakhoz használj kapcsos zárójelet

```r
# ha az 'y' argumentum hiányzik, adja össze 
# az 'x' vektor elemeit
advAdd <- function(x, y) {
    if (missing(y)) {
        out <- sum(x)
    } else {
        out <- x + y
    }
    return(out)
}
```

- a korábbi példában a `return` csak az érthetőség miatt szerepelt; az R az utoljára kiértékelt kifejezés eredményét automatikusan visszaadja

```r
advAdd2 <- function(x, y) {
    if (missing(y)) {
        sum(x)
    } else {
        x + y
    }
}
```

#### Hogyan hívhatók meg a függvények?
- már eddig is ezt csináltuk (az R-ben bármit csinálunk, azt valójában függvény(ek) meghívásával tesszük), de most nézzük a sajátunkra:

```r
# ha nem adunk meg argumentumnevet, akkor a függvény 
# argumentumainak eredeti sorrendje számít
simpleAdd(2, 4)
```

```
## [1] 6
```

```r
# ha megadjuk az argumentum nevét, a sorrend lényegtelen
simpleAdd(y = 4, x = 2)
```

```
## [1] 6
```

```r
# az argumentumként megadott objektumot nem muszáj a 
# függvényhívás előtt létrehozni
advAdd(1:3)
```

```
## [1] 6
```

#### Hogyan lehet tárolni a függvény visszatérési értékét?
- rendeld hozzá egy objektumhoz

```r
mysum <- advAdd(1:5)
mysum
```

```
## [1] 15
```
- többnyire a függvény-ek outputja sokkal komplexebb

```r
# példa: lineáris regresszió egy beépített adatbázison (?mtcars)
?mtcars
fit <- lm(mpg ~ wt, data=mtcars)
fit_summary <- summary(fit)
str(fit_summary)
```

```
## List of 11
##  $ call         : language lm(formula = mpg ~ wt, data = mtcars)
##  $ terms        :Classes 'terms', 'formula' length 3 mpg ~ wt
##   .. ..- attr(*, "variables")= language list(mpg, wt)
##   .. ..- attr(*, "factors")= int [1:2, 1] 0 1
##   .. .. ..- attr(*, "dimnames")=List of 2
##   .. .. .. ..$ : chr [1:2] "mpg" "wt"
##   .. .. .. ..$ : chr "wt"
##   .. ..- attr(*, "term.labels")= chr "wt"
##   .. ..- attr(*, "order")= int 1
##   .. ..- attr(*, "intercept")= int 1
##   .. ..- attr(*, "response")= int 1
##   .. ..- attr(*, ".Environment")=<environment: 0x6425c18> 
##   .. ..- attr(*, "predvars")= language list(mpg, wt)
##   .. ..- attr(*, "dataClasses")= Named chr [1:2] "numeric" "numeric"
##   .. .. ..- attr(*, "names")= chr [1:2] "mpg" "wt"
##  $ residuals    : Named num [1:32] -2.28 -0.92 -2.09 1.3 -0.2 ...
##   ..- attr(*, "names")= chr [1:32] "Mazda RX4" "Mazda RX4 Wag" "Datsun 710" "Hornet 4 Drive" ...
##  $ coefficients : num [1:2, 1:4] 37.285 -5.344 1.878 0.559 19.858 ...
##   ..- attr(*, "dimnames")=List of 2
##   .. ..$ : chr [1:2] "(Intercept)" "wt"
##   .. ..$ : chr [1:4] "Estimate" "Std. Error" "t value" "Pr(>|t|)"
##  $ aliased      : Named logi [1:2] FALSE FALSE
##   ..- attr(*, "names")= chr [1:2] "(Intercept)" "wt"
##  $ sigma        : num 3.05
##  $ df           : int [1:3] 2 30 2
##  $ r.squared    : num 0.753
##  $ adj.r.squared: num 0.745
##  $ fstatistic   : Named num [1:3] 91.4 1 30
##   ..- attr(*, "names")= chr [1:3] "value" "numdf" "dendf"
##  $ cov.unscaled : num [1:2, 1:2] 0.38 -0.1084 -0.1084 0.0337
##   ..- attr(*, "dimnames")=List of 2
##   .. ..$ : chr [1:2] "(Intercept)" "wt"
##   .. ..$ : chr [1:2] "(Intercept)" "wt"
##  - attr(*, "class")= chr "summary.lm"
```

### Hogyan lehet megnézni egy függvény forráskódját?
- az R nyílt forráskódú: csak gépeld be a függvény nevét, zárójel nélkül

```r
var
```

```
## function (x, y = NULL, na.rm = FALSE, use) 
## {
##     if (missing(use)) 
##         use <- if (na.rm) 
##             "na.or.complete"
##         else "everything"
##     na.method <- pmatch(use, c("all.obs", "complete.obs", "pairwise.complete.obs", 
##         "everything", "na.or.complete"))
##     if (is.na(na.method)) 
##         stop("invalid 'use' argument")
##     if (is.data.frame(x)) 
##         x <- as.matrix(x)
##     else stopifnot(is.atomic(x))
##     if (is.data.frame(y)) 
##         y <- as.matrix(y)
##     else stopifnot(is.atomic(y))
##     .Call(C_cov, x, y, na.method, FALSE)
## }
## <bytecode: 0x681a9e8>
## <environment: namespace:stats>
```

- vagy nézd meg a teljes forráskódot mondjuk itt: https://github.com/wch/r-source

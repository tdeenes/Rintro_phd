# Objektumok elemeinek módosítása

Egy objektum elemeinek módosítása tulajdonképpen nem más, mint az indexálás és a hozzárendelés kombinációja. 

- példa egy mátrix oszlopának "felülírására"

```r
mat <- matrix(1:4, 2, 2)
mat
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

```r
mat[, 2] <- c(9, 10)
mat
```

```
##      [,1] [,2]
## [1,]    1    9
## [2,]    2   10
```

- figyeljünk arra, hogy az R a módosításnál is reciklikál

```r
(vec <- sample(10))
```

```
##  [1]  4  7 10  8  3  6  9  1  5  2
```

```r
vec[1:4] <- c(100, 200)
vec
```

```
##  [1] 100 200 100 200   3   6   9   1   5   2
```

- arra is figyeljünk, hogy az R-ben egy elemi vektor (ide sorolandó a mátrix és
a tömb is) csak egyféle típusú (pl. csak integer vagy csak karakter) elemeket tartalmazhat -> az R ezt "észrevétlenül" kikényszeríti!

```r
(vec <- 21:30)
```

```
##  [1] 21 22 23 24 25 26 27 28 29 30
```

```r
typeof(vec)
```

```
## [1] "integer"
```

```r
vec[1:4] <- 1
typeof(vec)
```

```
## [1] "double"
```

```r
vec[10] <- "30"
typeof(vec)
```

```
## [1] "character"
```

- ha egy objektum tulajdonságait meg akarjuk tartani, viszont az összes elemét
ki akarjuk cserélni, érdemes lehet a következő "fogást" alkalmazni:

```r
x <- array(1:9, c(3, 3), 
           dimnames = list(dimA = letters[1:3], dimB = LETTERS[1:3]))
x
```

```
##     dimB
## dimA A B C
##    a 1 4 7
##    b 2 5 8
##    c 3 6 9
```

```r
x[] <- rnorm(9)
x
```

```
##     dimB
## dimA         A          B           C
##    a  1.081249  0.6823887 -0.09632429
##    b -1.251254  0.4101662  0.27467170
##    c  1.493776 -0.6730497 -1.87429927
```

```r
# vesd ossze ezzel a megoldassal:
y <- rnorm(9)
y
```

```
## [1] -0.3065144 -0.8623442 -1.1901602 -0.7367186  0.4221241  0.1928385
## [7]  2.0713363 -0.2601257 -0.4304319
```

```r
dim(y) <- dim(x)
dimnames(y) <- dimnames(x)
y
```

```
##     dimB
## dimA          A          B          C
##    a -0.3065144 -0.7367186  2.0713363
##    b -0.8623442  0.4221241 -0.2601257
##    c -1.1901602  0.1928385 -0.4304319
```

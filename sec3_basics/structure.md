# Objektumok megtekintése

Fontos tudatosítani, hogy a `print` eredménye többnyire nem felel meg az adott
objektum pontos tartalmának:


```r
options(digits = 2) # hany tizedesjegyet jelenitsen meg
vec <- rnorm(4)
print(vec)
```

```
## [1]  0.08  0.39 -0.82 -0.54
```

```r
# demonstracio 1
options(digits = 10)
vec
```

```
## [1]  0.0800438840  0.3901089625 -0.8171218957 -0.5354405228
```

```r
# demonstracio 2
class(vec) <- "specialVector"
print.specialVector <- function(x, ...) print.default("hello")
print(vec)
```

```
## [1] "hello"
```

```r
# allitsuk vissza az alapbeallitasra
options(digits = 7)
```



Egy objektum struktúrájáról többet megtudhatsz az RStudio "Environment" ablakában
a megfelelő objektumra pillantva, amely valójában a `str` függvény eredményét 
jeleníti meg.

- `str` -> roppant hasznos

```r
# az elobbi peldat folytatva:
str(vec)
```

```
## Class 'specialVector'  num [1:4] 0.08 0.39 -0.817 -0.535
```

```r
# uj pelda:
mydat <- matrix(rnorm(10), 2, 5, 
                dimnames=list(c("lower", "upper"),
                              paste("col", 1:5, sep=".")))
mydat
```

```
##            col.1      col.2     col.3      col.4      col.5
## lower -0.2705768 -2.0773748 0.7699770 -0.5320156 -0.2103310
## upper -0.3741381 -0.1975552 0.8402219 -0.5132661  0.9809526
```

```r
str(mydat)
```

```
##  num [1:2, 1:5] -0.271 -0.374 -2.077 -0.198 0.77 ...
##  - attr(*, "dimnames")=List of 2
##   ..$ : chr [1:2] "lower" "upper"
##   ..$ : chr [1:5] "col.1" "col.2" "col.3" "col.4" ...
```

- `head` és `tail` -> főként data.frame esetén jön jól

```r
datfr <- data.frame(characters = letters[1:20], numbers = 1:20)
```
- első 10 elem kiírása

```r
head(datfr, 10)
```

```
##    characters numbers
## 1           a       1
## 2           b       2
## 3           c       3
## 4           d       4
## 5           e       5
## 6           f       6
## 7           g       7
## 8           h       8
## 9           i       9
## 10          j      10
```

- utolsó 10 elem kiírása

```r
tail(datfr, 10)
```

```
##    characters numbers
## 11          k      11
## 12          l      12
## 13          m      13
## 14          n      14
## 15          o      15
## 16          p      16
## 17          q      17
## 18          r      18
## 19          s      19
## 20          t      20
```


# Az R objektum-osztályai

Vektorokra visszavezethető objektumok a következők:
- `matrix`
- `array`
- `list`
- `data.frame`
- hiányzó értékek

### Mátrixok (`matrix`)
- matrix = vector két dimenzióval (column-order)

```r
mat <- matrix(1:8, nrow = 2, ncol = 4)
mat
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6    8
```

```r
dim(mat)
```

```
## [1] 2 4
```
- vektorból is létrehozható

```r
newmat <- 3:6
dim(newmat) <- c(2, 2)
newmat
```

```
##      [,1] [,2]
## [1,]    3    5
## [2,]    4    6
```

### Többdimenziós mátrix a.k.a tömb (`array`)
- array = többdimenziós vektor

```r
arr <- array(1:12, c(3, 2, 2)) # array-nel vektorral adjuk meg a dimenziokat
arr
```

```
## , , 1
## 
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
## 
## , , 2
## 
##      [,1] [,2]
## [1,]    7   10
## [2,]    8   11
## [3,]    9   12
```

- mátrixból is létrehozható

```r
mat <- matrix(1:8, 2, 4)
mat
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6    8
```

```r
arr <- mat
dim(arr) <- c(2, 2, 2)
arr
```

```
## , , 1
## 
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
## 
## , , 2
## 
##      [,1] [,2]
## [1,]    5    7
## [2,]    6    8
```

### Faktorok (`factor`)
- factor = integer vektor címkékkel, amelyet az R speciálisan kezel
- kiemelten hasznos kategoriális változók tárolására

```r
fac <- factor(c(1, 1, 1, 2, 2, 1, 2), labels = c("male", "female"))
fac
```

```
## [1] male   male   male   female female male   female
## Levels: male female
```

```r
newfac <- factor(c("male", "male", "male", "female", "female", "male", "female"))
newfac
```

```
## [1] male   male   male   female female male   female
## Levels: female male
```

### Listák (`list`)
- list = speciális vektor amelyik bármilyen más elemet tartalmazhat (vektort, array-t, listát, stb.)

```r
mylist <- vector("list", 2) # "ures"" lista letrehozasa
mylist
```

```
## [[1]]
## NULL
## 
## [[2]]
## NULL
```

```r
newlist <- list(a = 1, b = FALSE, letters[1:5]) # kozvetlen megadas
newlist
```

```
## $a
## [1] 1
## 
## $b
## [1] FALSE
## 
## [[3]]
## [1] "a" "b" "c" "d" "e"
```

### Data frame (`data.frame`)
- data frame = speciális lista, amely azonos hosszúságú vektorokból áll, és 
mátrix-os elrendezésű

```r
datfr <- data.frame(digits = 10:6, characters = letters[1:5])
datfr
```

```
##   digits characters
## 1     10          a
## 2      9          b
## 3      8          c
## 4      7          d
## 5      6          e
```
- v.ö. egy mátrix-szal

```r
as.matrix(datfr)
```

```
##      digits characters
## [1,] "10"   "a"       
## [2,] " 9"   "b"       
## [3,] " 8"   "c"       
## [4,] " 7"   "d"       
## [5,] " 6"   "e"
```

### Hiányzó értékek
- hiányzó értékek: NA (not available) vagy NaN (not a number)
- minden NaN NA, de nem minden NA NaN

```r
x <- c(1, 3, 4, NaN, 5, NA)
is.na(x)
```

```
## [1] FALSE FALSE FALSE  TRUE FALSE  TRUE
```

```r
is.nan(x)
```

```
## [1] FALSE FALSE FALSE  TRUE FALSE FALSE
```

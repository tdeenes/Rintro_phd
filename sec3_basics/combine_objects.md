# Objektumok kombinálása

- c() -> element by element (listáknál figyelni!)

```r
# ez igy egy harom-elemu listat eredmenyez:
c(list(x = 1:3, y = rnorm(2)), list(z = c("hi", "hello")))
```

```
## $x
## [1] 1 2 3
## 
## $y
## [1] -0.3854566  0.5128661
## 
## $z
## [1] "hi"    "hello"
```

```r
# az viszont nem:
z <- c("hi", "hello")
c(list(x = 1:3, y = rnorm(2)), z)
```

```
## $x
## [1] 1 2 3
## 
## $y
## [1]  0.2515962 -0.3001704
## 
## [[3]]
## [1] "hi"
## 
## [[4]]
## [1] "hello"
```

- cbind() -> oszlopok mentén

```r
# ket vektor osszeillesztese egy-egy oszlopba
cbind(x = 1:3, y = 4:6)
```

```
##      x y
## [1,] 1 4
## [2,] 2 5
## [3,] 3 6
```

```r
# ha az egyik rovidebb, az R reciklikalja
cbind(x = 1:2, y = 1:4)
```

```
##      x y
## [1,] 1 1
## [2,] 2 2
## [3,] 1 3
## [4,] 2 4
```

- mátrixok abban az esetben `cbind`-olhatók, ha azonos számú sorból állnak

```r
( mat1 <- matrix(1:2, 1, 2) )  # ( ) csak az auto-print miatt
```

```
##      [,1] [,2]
## [1,]    1    2
```

```r
( mat2 <- matrix(1:4, 2, 2) )
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

```r
( mat3 <- matrix(5:8, 2, 2) )
```

```
##      [,1] [,2]
## [1,]    5    7
## [2,]    6    8
```


```r
#cbind(mat1, mat2) # ez hibat eredmenyezne
cbind(mat2, mat3)
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    3    5    7
## [2,]    2    4    6    8
```

- rbind() -> kombinálás sorok mentén

```r
rbind(x = 1:3, y = 4:6)
```

```
##   [,1] [,2] [,3]
## x    1    2    3
## y    4    5    6
```

- data.frame() -> hasonló a cbind()-hoz, de data.frame-et eredményez

```r
data.frame(x = 1:3, y = 4:6)
```

```
##   x y
## 1 1 4
## 2 2 5
## 3 3 6
```

- abind() -> array-ek kombinálására (kell hozzá az `abind` csomagot)

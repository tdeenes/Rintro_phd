# Objektumok elemeinek elérése (indexálása)

- `[` -> megőrzi az objektum alaposztályát, több elem is elérhető
- `[[` -> főként `list` és `data.frame` objektumokra, csak egy elem elérésére
- `$` -> csak `list` és `data.frame` objektumokra, csak névvel
- `@` -> S4 objektumokra (kezdőként nem kell)
- az R-ben az elemeket elérhetjük a pozíciójuk és a nevük alapján is (már 
persze ha van nekik), illetve használhatunk logikai vektort is az elemek 
megtartására vagy kizárására


### Elemek elérése vektorból


```r
# hozzunk letre egy vektort, amelynek az elemeknek van neve
( vec <- c(1:2, 4) )
```

```
## [1] 1 2 4
```

```r
names(vec) <- c("a", "b", "d")
vec
```

```
## a b d 
## 1 2 4
```

```r
# numerikus index-szel
vec[2:3]
```

```
## b d 
## 2 4
```

```r
# negativ szam azt jelenti, hogy 'minden, kiveve az adott sorszamu elem'
vec[-1]
```

```
## b d 
## 2 4
```

```r
# eleres nevvel
vec["b"]
```

```
## b 
## 2
```

```r
# logikai vektorral is indexelhetunk: 
# a TRUE elemek maradnak, a FALSE elemek kiesnek
# -> logikai index hossza azonos kell legyen a vektor hosszaval
vec[c(FALSE, TRUE, FALSE, FALSE)]
```

```
## b 
## 2
```

### Elemek elérése többdimenziós vektorból

```r
( mat <- matrix((1:8)^2, 2, 4) )
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    9   25   49
## [2,]    4   16   36   64
```

```r
# elso sor elerese
mat[1, ]
```

```
## [1]  1  9 25 49
```

```r
# masodik oszlop elerese
mat[, 2]
```

```
## [1]  9 16
```

```r
# vegyithetjuk is az index-tipusokat:
# pl. elso sor igen, masodik sor nem, illetve minden oszlop a 3. kivetelevel:
mat[c(TRUE, FALSE), -3]
```

```
## [1]  1  9 49
```

- ha meg akarod őrizni a dimenziókat (programozáskor nagyon hasznos)

```r
mat[, 2, drop = FALSE]
```

```
##      [,1]
## [1,]    9
## [2,]   16
```
- első 5 elem elérése (ügyelj arra, hogy az R oszlop-orientált)

```r
mat[1:5]
```

```
## [1]  1  4  9 16 25
```

### Lista és data.frame elemeinek elérése

```r
( mylist <- list(x=1, y=1:2, z=1:4) )
```

```
## $x
## [1] 1
## 
## $y
## [1] 1 2
## 
## $z
## [1] 1 2 3 4
```

- névvel

```r
mylist$y
```

```
## [1] 1 2
```

```r
mylist[["y"]]
```

```
## [1] 1 2
```

- több elem együttes elérése névvel

```r
mylist[c("x", "z")]
```

```
## $x
## [1] 1
## 
## $z
## [1] 1 2 3 4
```
- és numerikus indexekkel

```r
mylist[c(1, 3)]
```

```
## $x
## [1] 1
## 
## $z
## [1] 1 2 3 4
```

- lista transzformációja data.frame-mé

```r
( datfr <- as.data.frame(mylist) )
```

```
##   x y z
## 1 1 1 1
## 2 1 2 2
## 3 1 1 3
## 4 1 2 4
```

- emlékezz, hogy a data.frame a lista és a mátrix kombinációjának tekinthető
- a 'z' változó elérése

```r
datfr[["z"]] 
```

```
## [1] 1 2 3 4
```

```r
datfr$z
```

```
## [1] 1 2 3 4
```

```r
datfr[, "z"]
```

```
## [1] 1 2 3 4
```


### Bizonyos sorok kiválasztása `data.frame`-ből

- lássuk a korábban létrehozott data.frame-et:

```r
datfr
```

```
##   x y z
## 1 1 1 1
## 2 1 2 2
## 3 1 1 3
## 4 1 2 4
```

- érjük el a második sorát (emlékezz, a data.frame mátrixként is indexelhető):

```r
datfr[2, ]
```

```
##   x y z
## 2 1 2 2
```

- érjük el azt a sort, amelynél a 'z' változó értéke nagyobb 2-nél:

```r
# hozzunk létre egy vektort, amelyiknek az elemei TRUE vagy FALSE
# attól függően, hogy a 'datfr' objektum 'z' változója nagyobb-e 2-nél
index <- datfr$z > 2

# használjuk ezt az index vektort a megfelelő sorok kinyerésére
datfr[index, ]
```

```
##   x y z
## 3 1 1 3
## 4 1 2 4
```

```r
# az 'index' vektort nem muszáj expliciten létrehozni
datfr[datfr$z > 2, ]
```

```
##   x y z
## 3 1 1 3
## 4 1 2 4
```

- egy kényelmesen használható függvény data.frame indexelésére a `subset()`

```r
subset(datfr, z > 2)
```

```
##   x y z
## 3 1 1 3
## 4 1 2 4
```



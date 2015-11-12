# R objektumok (de)szerializációja

A szerializáció, illetve deszerializáció a memóriában tárolt objektumok külső
tárolóra történő mentését, illetve az onnan történő visszaállítást jelenti.
Közérthetőbben most arról lesz szó, hogyan lehet a legegyszerűbben elmentened,
illetve betöltened R-objektumokat.

### Mentés

- hozzunk létre két példa-adatot:

```r
x <- c(1, 3, 5, 7)
y <- data.frame(id = c("001", "002", "003"), IQ = c(92, 128, 101))
```

- egy objektum mentése:

```r
saveRDS(y, file = "iq.rds")
```

- több objektum mentése:

```r
save(x, y, file = "iq.RData")
```

- (majdnem) minden objektum mentése

```r
save(list = ls(), file = "all.RData")
```

### Visszaállítás

- a `saveRDS`-sel elmentett objektum nem tartalmazza az objektum nevét, tehát
a beolvasott adatot hozzá kell rendelnünk egy új változóhoz:

```r
y_import <- readRDS("iq.rds")

# ellenorzes
identical(y, y_import)
```

```
## [1] TRUE
```

- a `save` parancs az objektumot és az objektum nevét is elmenti, így
betöltéskor azok is betöltődnek -> NAGYON ÓVATOS legyél, mert észrevétlenül
felülírhatsz egy memóriában tárolt változót

```r
# létrehozok egy új x változót
x <- "proba"

# betoltom az "all.RData" fajlt
load("all.RData")

# mivel az "all.RData" fajl tartalmaz egy `x` objektumot, a betoltesevel 
# felulirtuk a memoriaban tarolt `x`-et
x
```

```
## [1] 1 3 5 7
```

- a `load` fentebbi kellemetlen mellékhatása kiküszöbölhető, ha egy külön
környezetbe töltjük be az adatokat, vagy ha csak beillesztjük a keresési útba

```r
# uj kornyezet
e <- new.env(parent = emptyenv())
load("all.RData", e)
ls(e)
```

```
##  [1] "advAdd"              "advAdd2"             "arr"                
##  [4] "bib"                 "datfr"               "downvec"            
##  [7] "fac"                 "fit"                 "fit_summary"        
## [10] "i"                   "index"               "int"                
## [13] "mat"                 "mat1"                "mat2"               
## [16] "mat3"                "mydat"               "mylist"             
## [19] "mysum"               "newfac"              "newlist"            
## [22] "newmat"              "num"                 "packs"              
## [25] "print.specialVector" "simpleAdd"           "upvec"              
## [28] "vec"                 "vec.reference"       "vec.target"         
## [31] "x"                   "y"                   "z"
```

```r
# keresesi ut modositasa
attach("all.RData")
x
```

```
## [1] 1 3 5 7
```

```r
get("x", pos = 2)
```

```
## [1] 1 3 5 7
```



### Példaadatok betöltése

Számos R csomag tartalmaz "beépített" példaadatokat. Ezen adatok valójában 
.RData vagy .rda kiterjesztésű fájlok, amelyek akár egy egyszerű `load()`
paranccsal is betölthetők. Ehhez azonban tudunk kell a fájl elérési útját, ami
helyett sokkal kényelmesebb a `data()` függvényt alkalmazni. A `data()` 
először a betöltött csomagokban keresi az adott nevű adatot, majd a 
munkakönyvtár "data" nevű mappájában (már ha létezik ilyen nevű könyvtár).
A későbbiekben a `data()` parancsot gyakran fogjuk használni a példákban,
például így:


```r
# a diszlexia-vizsgálati adatok betoltese
data(dyslex)
```


# Átstrukturálás

Az adatbevitelnél gyakran "wide" formátumban rögzítik az adatokat,
a modellezésnél viszont a "long" formátum a kedvezőbb. 

- példa wide formátumra

```r
# adatok betoltese
data(dyslex)

# folso nehany sor
head(dyslex)
```

```
##   id nem  csoport oszt kor figyzavar szokincs olv_helyes1 olv_helyes2
## 1 s1 fiu kontroll    3 117        50       32          28          17
## 2 s2 fiu kontroll    3 115        63       49          41          29
## 3 s3 fiu kontroll    2 108        51       20          34          35
## 4 s4 fiu kontroll    3 117        69       35          26          18
## 5 s5 fiu kontroll    3 123        53       31          28          21
## 6 s6 fiu kontroll    3 115        60       30          40          38
##   olv_helyes3 sp_helyes1 sp_helyes2 sp_helyes3 sp_helyes4 sp_helyes5
## 1          18         28         20         19         17         19
## 2          23         29         17         18         17         19
## 3          26         19         14         12         12          9
## 4          19         20         14         11         12         12
## 5          21         16          5         17         14         13
## 6          36         26         14         20         18         13
##   figy_csop olvasas helyesiras
## 1  kontroll      63        103
## 2  kontroll      93        100
## 3  kontroll      95         66
## 4      adhd      63         69
## 5  kontroll      70         65
## 6  kontroll     114         91
```

- elemezzük csak az olvasást

```r
dyslex_read <- subset(dyslex, 
                      select = -(sp_helyes1:sp_helyes5))
head(dyslex_read)
```

```
##   id nem  csoport oszt kor figyzavar szokincs olv_helyes1 olv_helyes2
## 1 s1 fiu kontroll    3 117        50       32          28          17
## 2 s2 fiu kontroll    3 115        63       49          41          29
## 3 s3 fiu kontroll    2 108        51       20          34          35
## 4 s4 fiu kontroll    3 117        69       35          26          18
## 5 s5 fiu kontroll    3 123        53       31          28          21
## 6 s6 fiu kontroll    3 115        60       30          40          38
##   olv_helyes3 figy_csop olvasas helyesiras
## 1          18  kontroll      63        103
## 2          23  kontroll      93        100
## 3          26  kontroll      95         66
## 4          19      adhd      63         69
## 5          21  kontroll      70         65
## 6          36  kontroll     114         91
```

- alakítsuk át long formátumba (legyen egy 'blokk' és egy 'olv_helyes' valtozonk)

```r
dyslex_read_long <- reshape(dyslex_read, 
                            varying = c("olv_helyes1", "olv_helyes2", "olv_helyes3"),
                            timevar = "blokk",
                            v.names = "olv_helyes",
                            direction = "long")
head(dyslex_read_long)
```

```
##      id nem  csoport oszt kor figyzavar szokincs figy_csop olvasas
## s1.1 s1 fiu kontroll    3 117        50       32  kontroll      63
## s2.1 s2 fiu kontroll    3 115        63       49  kontroll      93
## s3.1 s3 fiu kontroll    2 108        51       20  kontroll      95
## s4.1 s4 fiu kontroll    3 117        69       35      adhd      63
## s5.1 s5 fiu kontroll    3 123        53       31  kontroll      70
## s6.1 s6 fiu kontroll    3 115        60       30  kontroll     114
##      helyesiras blokk olv_helyes
## s1.1        103     1         28
## s2.1        100     1         41
## s3.1         66     1         34
## s4.1         69     1         26
## s5.1         65     1         28
## s6.1         91     1         40
```

- a *reshape2* csomaggal egyszerűbb

```r
library(reshape2)
```

```
## 
## Attaching package: 'reshape2'
## 
## The following objects are masked from 'package:data.table':
## 
##     dcast, melt
```

```r
dyslex_read_long2 <- melt(
    dyslex_read, 
    measure.vars = c("olv_helyes1", "olv_helyes2", "olv_helyes3"),
    variable.name = "mutato",
    value.name = "ertek")
```


- talán még egyszerűbb a *tidyr* csomaggal

```r
library(tidyr)
dyslex_read_long3 <- gather(dyslex_read, mutato, ertek, 
                            olv_helyes1:olv_helyes3)
```

- és szintén kellemes (es nagyon gyors) a *data.table* megoldása



```r
library(data.table)
dyslex_read_long4 <- melt(data.table(dyslex_read), 
     measure.vars = c("olv_helyes1", "olv_helyes2", "olv_helyes3"),
     variable.name = "mutato",
     value.name = "ertek")
```

- long-ból wide formátumba:
    - base: `reshape(..., direction = "wide")`
    - reshape2, data.table: `?dcast`
    - tidyr: `spread`

```r
# tidyr
dyslex_orig <- spread(dyslex_read_long3, mutato, ertek)
str(dyslex_orig)
```

```
## 'data.frame':	101 obs. of  13 variables:
##  $ id         : Factor w/ 101 levels "s1","s10","s100",..: 1 14 25 36 47 58 69 80 91 2 ...
##  $ nem        : Factor w/ 2 levels "lany","fiu": 2 2 2 2 2 2 2 1 2 1 ...
##  $ csoport    : Factor w/ 2 levels "kontroll","sni": 1 1 1 1 1 1 1 1 1 1 ...
##  $ oszt       : num  3 3 2 3 3 3 3 3 2 3 ...
##  $ kor        : num  117 115 108 117 123 115 119 109 102 107 ...
##  $ figyzavar  : num  50 63 51 69 53 60 57 54 50 50 ...
##  $ szokincs   : num  32 49 20 35 31 30 40 36 47 32 ...
##  $ figy_csop  : Ord.factor w/ 2 levels "kontroll"<"adhd": 1 1 1 2 1 1 1 1 1 1 ...
##  $ olvasas    : num  63 93 95 63 70 114 120 100 101 49 ...
##  $ helyesiras : num  103 100 66 69 65 91 79 79 54 66 ...
##  $ olv_helyes1: num  28 41 34 26 28 40 44 36 39 17 ...
##  $ olv_helyes2: num  17 29 35 18 21 38 40 36 30 16 ...
##  $ olv_helyes3: num  18 23 26 19 21 36 36 28 32 16 ...
```


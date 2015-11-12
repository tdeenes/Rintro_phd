# Szövegfájlok beolvasása és kiírása



### Beolvasás
Szövegfájlok (pl. .txt, .csv) importálását lehetőleg kezdd azzal, hogy 
egy szerkesztővel (ne Excel-lel!) megnézed a fájl tartalmát. Ebből megtudhatod,
hogy milyen karakter választja el az értékeket (pl. tab vagy pontosvessző),
milyen karakter jelzi a tizedesvesszőt (pont vagy vessző) stb.

Alapesetben a `read.table` függvényt érdemes használni.(Ha kíváncsi vagy a 
részletekre és a mélyebb szintű függvényekre, nézd meg a [hivatalos leírást](http://cran.rapporter.net/doc/manuals/r-release/R-data.html)).

```r
# egy peldafajl, amely kulonbozo uzemek dolgozoinak alkalmassagvizsgalati
# eredmenyeit tartalmazza (a "data" konyvtarban talalhato, ezert kell a
# file.path() fuggvenyt hasznalni)
dat_txt <- read.table(file.path("data", "AlkVizsg.txt"), 
                      sep = "\t", dec = ",", header = TRUE)
str(dat_txt)
```

```
## 'data.frame':	623 obs. of  8 variables:
##  $ uzem             : Factor w/ 4 levels "EBM","Papst",..: 4 4 4 4 4 4 4 4 4 4 ...
##  $ id               : Factor w/ 623 levels "e1","e10","e100",..: 512 536 547 558 569 580 591 602 613 513 ...
##  $ d_proba_N        : int  441 370 370 348 521 445 557 400 618 543 ...
##  $ d_proba_hibaN    : int  77 174 69 34 53 29 88 50 114 121 ...
##  $ abrasor          : int  5 5 5 8 7 7 10 9 5 6 ...
##  $ abraanalogia     : int  7 4 5 6 10 9 7 8 9 8 ...
##  $ kezugyesseg_vonal: num  0.92 0.855 0.714 0.967 1 0.972 0.949 0.947 0.952 0.929 ...
##  $ kezugyesseg_pont : num  0.948 0.844 0.54 0.982 0.96 0.971 0.883 0.953 0.957 0.988 ...
```

```r
# egyszerubben
dat_txt_short <- read.delim2(file.path("data", "AlkVizsg.txt"))

# a ket objektum megegyezik (nem csoda, lasd a read.delim2 forraskodjat)
identical(dat_txt, dat_txt_short)
```

```
## [1] TRUE
```

```r
# ugyanez a .csv formatumu fajl eseteben
dat_csv <- read.table(file.path("data", "AlkVizsg.csv"), 
                      sep = ";", dec = ",", header = TRUE)
str(dat_csv)
```

```
## 'data.frame':	623 obs. of  8 variables:
##  $ uzem             : Factor w/ 4 levels "EBM","Papst",..: 4 4 4 4 4 4 4 4 4 4 ...
##  $ id               : Factor w/ 623 levels "e1","e10","e100",..: 512 536 547 558 569 580 591 602 613 513 ...
##  $ d_proba_N        : int  441 370 370 348 521 445 557 400 618 543 ...
##  $ d_proba_hibaN    : int  77 174 69 34 53 29 88 50 114 121 ...
##  $ abrasor          : int  5 5 5 8 7 7 10 9 5 6 ...
##  $ abraanalogia     : int  7 4 5 6 10 9 7 8 9 8 ...
##  $ kezugyesseg_vonal: num  0.92 0.855 0.714 0.967 1 0.972 0.949 0.947 0.952 0.929 ...
##  $ kezugyesseg_pont : num  0.948 0.844 0.54 0.982 0.96 0.971 0.883 0.953 0.957 0.988 ...
```

```r
# a ket objektum megegyezik
identical(dat_txt, dat_csv)
```

```
## [1] TRUE
```

```r
# egy meg kenyelmesebb megoldas
dat_csv_short <- read.csv2(file.path("data", "AlkVizsg.csv"))

# az eredmeny ujra ugyanaz
identical(dat_csv, dat_csv_short)
```

```
## [1] TRUE
```

Ha nagyobb fájlról van szó, érdemes áttanulmányozni a `read.table`
dokumentációját. Az argumentumok megfelelő megválasztásával jelentősen
felgyorsíthatjuk a beolvasási folyamatot.

```r
# ennel a meretnel mindegy, de az argumentumok illusztraciojara oke
temp <- read.table(file.path("data", "AlkVizsg.txt"),
                   sep = "\t", dec = ",", header = TRUE,
                   colClasses = c("character", "character",
                                  rep("integer", 4),
                                  rep("numeric", 2)),
                   comment.char = "",
                   fileEncoding = "UTF-8",
                   nrows = 623)
```

Ha igazán nagy szövegfájlt próbálsz beolvasni, használd az `fread` függvényt
a *data.table* csomagból.

### Kiírás

A szövegfájlba történő kiírás jellemzően a `write.table` függvénnyel történik.

```r
# kiiras
write.table(dat_csv, file = "temp.csv", 
            sep = ";", quote = FALSE, 
            row.names = FALSE)

# csak pelda volt, toroljuk is fajlt
unlink("temp.csv")
```


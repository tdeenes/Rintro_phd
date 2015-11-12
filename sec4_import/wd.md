# Munkakönyvtár, fájlműveletek

Mielőtt rátérünk az adatbeolvasásra és -kiírásra, néhány praktikus infó:

1) Ne felejtkezz el a munkakönyvtár beállításáról:

```r
# aktualis munkakonyvtar (=working directory)
( wd <- getwd() )
```

```
## [1] "/home/tdenes/Documents/Eloadasok/2015/PHD_Rkurzus/Rintro_phd/sec4_import"
```

```r
# munkakonyvtar modositasa
setwd("..")

# visszalepes az eredeti munkakonyvtarba
setwd(wd)
```

2) Az R képes egyszerű fájlműveletekre, mint például:

- egy könyvtár tartalmának megjelenítése

```r
# a (rejtett fajlok nelkuli) teljes lista
dir()
```

```
##  [1] "data"          "README.md"     "serialize.md"  "serialize.Rmd"
##  [5] "spss.md"       "spss.Rmd"      "text.md"       "text.Rmd"     
##  [9] "wd.md"         "wd.Rmd"
```

```r
# bizonyos mintazatu fajlnevek
dir(pattern = "Rmd")
```

```
## [1] "serialize.Rmd" "spss.Rmd"      "text.Rmd"      "wd.Rmd"
```

```r
# a dir() es a list.files() ugyanaz
?dir
```

- fájlok másolása, törlése stb.

```r
?file.copy
```

- fájlok alapinformációinak elérése (pl. méret)

```r
?file.info
```


# R objektumok létrehozása

Egy példa: számítsuk ki, hogy mennyi 3 + 4.

```r
3 + 4
```

```
## [1] 7
```

Valójában az SPSS és számos kommerciális statisztikai program a felhasználó
szempontjából nem több egy nagyon bonyolult számológépnél: megadod az inputokat,
az inputok közötti műveleteket, majd a program kiprinteli az eredményt. Az R ennél 
jóval több: itt minden input és művelet valójában egy objektum, és a műveletek eredménye szintén egy objektum. Ez azért nagyon klassz, mert ezáltal egy eredményt
felhasználhatsz egy másik művelet inputjaként. Ha egy művelet eredményét meg akarod
"őrizni" későbbi felhasználásra, azt jelezned kell az R-nek. 

Az R-ben számos módon létrehozhatunk objektumokat, ezek közül a legalapvetőbb
a `<-` jel (amely valójában egy függvény, lásd később).

- `<-` a hozzárendelés jele

```r
x <- 3 + 4
x     # ha konzolban vagy, ez automatikusan meghivja a print parancsot
```

```
## [1] 7
```

```r
print(x) # fuggvenyen belul ki kell irni
```

```
## [1] 7
```

```r
(x <- 3 + 4) # sima zarojel (fuggveny nelkul) szinten a print-et hivja meg
```

```
## [1] 7
```

- az `=` szintén használható hozzárendelésre, de inkább korlátozzuk függvényargumentumok megadására (lásd később)

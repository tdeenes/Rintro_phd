# Operátorok

## Általános operátorok
- azonosan egyenlő (DE ld. `?all.equal`): `==`
- nagyobb/kisebb: `>` `<`
- nagyobb/kisebb vagy egyenlő: `>=` `<=`
- negáció: `!` (pl. nem egyenlő: `!=`)
- és: `&` (lásd még: `&&`)
- vagy: `|` (ld még: `||`)
- kizárólagos vagy: `xor(cond1, cond2)`
- feltétel: `if (cond==TRUE) { do this } else { do that }`

## Speciális operátorok
- `%*%` = mátrix-szorzás
- `%in%` = illeszkedő elemek (ld még: `?match`):

```r
# az `%in%` nem különbözteti meg a numeric és integer típust 
( vec.target <- c(6, 2, 10) )
```

```
## [1]  6  2 10
```

```r
( vec.reference <- 1:10 )
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
vec.target %in% vec.reference
```

```
## [1] TRUE TRUE TRUE
```

- `%o%` = outer product (see `?outer`)
- `%%` = modulo, `%/%` = egészrész
- `:` = sorozat létrehozása, lásd ?seq 
- `::` = egy csomag fv-ének meghívása a csomag betöltése nélkül
- `:::` = egy csomag nem exportált fv-ének elérése

```r
print.anova  # ez hibát eredményez, mivel a függvény "rejtett" (nem exportált)
```

```
## Error in eval(expr, envir, enclos): object 'print.anova' not found
```

```r
#getAnywhere(print.anova) ## -> a print.anova fv-t a stats csomag tartalmazza
stats:::print.anova # így már elérhetjük
```

```
## function (x, digits = max(getOption("digits") - 2L, 3L), signif.stars = getOption("show.signif.stars"), 
##     ...) 
## {
##     if (!is.null(heading <- attr(x, "heading"))) 
##         cat(heading, sep = "\n")
##     nc <- dim(x)[2L]
##     if (is.null(cn <- colnames(x))) 
##         stop("'anova' object must have colnames")
##     has.P <- grepl("^(P|Pr)\\(", cn[nc])
##     zap.i <- 1L:(if (has.P) 
##         nc - 1
##     else nc)
##     i <- which(substr(cn, 2, 7) == " value")
##     i <- c(i, which(!is.na(match(cn, c("F", "Cp", "Chisq")))))
##     if (length(i)) 
##         zap.i <- zap.i[!(zap.i %in% i)]
##     tst.i <- i
##     if (length(i <- grep("Df$", cn))) 
##         zap.i <- zap.i[!(zap.i %in% i)]
##     printCoefmat(x, digits = digits, signif.stars = signif.stars, 
##         has.Pvalue = has.P, P.values = has.P, cs.ind = NULL, 
##         zap.ind = zap.i, tst.ind = tst.i, na.print = "", ...)
##     invisible(x)
## }
## <bytecode: 0x690d940>
## <environment: namespace:stats>
```

# Az R szintaxisának jellegzetességei

- a komment jele: # (csak az adott sorra érvényes)
- lehet törni sorokat, nem kell lezárni a sort `;`-vel
- háromféle zárójel:
- `()` fv meghívására, `[]` vektor elemeinek elérésére (spec. formája a `[]`), és `{}` parancsok csoportosítására
- a zárójel-blokkok tetszőlegesen beágyazhatók

```r
# pelda a zarojelek hasznalatara
system.time(   
    {   # a sorok innentol...
    x <- 3L
    y <- 4L   
    for (i in 1:100) {
        # egymasba agyazott zarojelek
        mean(matrix(rnorm(100000, x, y), 1000, 100)[, i])  
        }
    }    # ... idaig egy blokkba tartoznak
)
```

```
##    user  system elapsed 
##   0.836   0.000   0.836
```

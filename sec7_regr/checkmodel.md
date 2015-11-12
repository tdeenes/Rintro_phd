# Ellenőrzés

A modell futtatása után ildomos ellenőrizni, hogy a reziduálisok normál 
eloszlásúak és homoszkedasztikusak-e, illetve hogy nincsenek-e túlzottan
befolyásos megfigyelési egységek a mintában.




- egy egyszerű módszer:

```r
plot(model)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png) ![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-2.png) ![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-3.png) ![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-4.png) 

_Tipp_: regressziós modellekhez és ANOVA-hoz erősen ajánlott telepíteni John Fox 
[*car*](https://cran.r-project.org/web/packages/car/index.html) nevű csomagját. Rengeteg hasznos függvényt tartalmaz, többek között reziduálisok diagnosztikájához kapcsolódóakat is.

# Az lme4 csomag szintaxisa 



Az lme4 csomag az R hagyományos `formula`-jat egészíti ki azzal, hogy a 
random hatásokat `()`-ben kell megadnunk, `|` jellel elválasztva a random
hatás struktúráját magától a random faktortól.


- konstans + random konstans:

```r
library(lme4)
```

```
## Loading required package: Matrix
```

```r
mod0 <- lmer(scRT ~ 1 + (1 | Subject), data = lexdec_corr)
summary(mod0)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ 1 + (1 | Subject)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 3947.4
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.5443 -0.6751 -0.0900  0.5266  5.6587 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  Subject  (Intercept) 0.3635   0.6029  
##  Residual             0.6625   0.8140  
## Number of obs: 1594, groups:  Subject, 21
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept) 0.002605   0.133131    0.02
```

- "valódi" fix hatás + random konstans + random slope:

```r
mod_trial <- lmer(scRT ~ scTrial + (1 + scTrial | Subject), 
                  data = lexdec_corr)
summary(mod_trial)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 + scTrial | Subject)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 3932.5
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.6980 -0.6648 -0.0766  0.5195  5.7253 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev. Corr 
##  Subject  (Intercept) 0.36429  0.6036        
##           scTrial     0.01695  0.1302   -0.33
##  Residual             0.64584  0.8036        
## Number of obs: 1594, groups:  Subject, 21
## 
## Fixed effects:
##              Estimate Std. Error t value
## (Intercept)  0.002846   0.133246   0.021
## scTrial     -0.034086   0.034885  -0.977
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial -0.267
```

- keresztezett random hatások:

```r
mod_crossed <- lmer(scRT ~ scTrial + (1 + scTrial | Subject) + (1 | Word), 
                    data = lexdec_corr)
summary(mod_crossed)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 + scTrial | Subject) + (1 | Word)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 3599.9
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.3768 -0.6269 -0.1168  0.4464  6.0555 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev. Corr 
##  Word     (Intercept) 0.18275  0.4275        
##  Subject  (Intercept) 0.37168  0.6097        
##           scTrial     0.01655  0.1286   -0.29
##  Residual             0.46785  0.6840        
## Number of obs: 1594, groups:  Word, 79; Subject, 21
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.01718    0.14251   0.121
## scTrial     -0.03851    0.03310  -1.164
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial -0.227
```

- beágyazott random hatások (többféle megadási mód lehetséges):

```r
mod_nested1 <- lmer(scRT ~ scTrial + (1 | Page) + (1 | Word), 
                    data = lexdec_corr)
mod_nested2 <- lmer(scRT ~ scTrial + (1 | Page) + (1 | Word:Page), 
                    data = lexdec_corr)
mod_nested3 <- lmer(scRT ~ scTrial + (1 | Page/Word), 
                    data = lexdec_corr)
summary(mod_nested1)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 | Page) + (1 | Word)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 4363.8
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2557 -0.6725 -0.1447  0.4817  4.4651 
## 
## Random effects:
##  Groups   Name        Variance Std.Dev.
##  Word     (Intercept) 0.07730  0.2780  
##  Page     (Intercept) 0.08711  0.2951  
##  Residual             0.84531  0.9194  
## Number of obs: 1594, groups:  Word, 79; Page, 10
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.01154    0.10111   0.114
## scTrial     -0.04445    0.02333  -1.905
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial 0.000
```

```r
summary(mod_nested2)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 | Page) + (1 | Word:Page)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 4363.8
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2557 -0.6725 -0.1447  0.4817  4.4651 
## 
## Random effects:
##  Groups    Name        Variance Std.Dev.
##  Word:Page (Intercept) 0.07730  0.2780  
##  Page      (Intercept) 0.08711  0.2951  
##  Residual              0.84531  0.9194  
## Number of obs: 1594, groups:  Word:Page, 79; Page, 10
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.01154    0.10111   0.114
## scTrial     -0.04445    0.02333  -1.905
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial 0.000
```

```r
summary(mod_nested3)
```

```
## Linear mixed model fit by REML ['lmerMod']
## Formula: scRT ~ scTrial + (1 | Page/Word)
##    Data: lexdec_corr
## 
## REML criterion at convergence: 4363.8
## 
## Scaled residuals: 
##     Min      1Q  Median      3Q     Max 
## -2.2557 -0.6725 -0.1447  0.4817  4.4651 
## 
## Random effects:
##  Groups    Name        Variance Std.Dev.
##  Word:Page (Intercept) 0.07730  0.2780  
##  Page      (Intercept) 0.08711  0.2951  
##  Residual              0.84531  0.9194  
## Number of obs: 1594, groups:  Word:Page, 79; Page, 10
## 
## Fixed effects:
##             Estimate Std. Error t value
## (Intercept)  0.01154    0.10111   0.114
## scTrial     -0.04445    0.02333  -1.905
## 
## Correlation of Fixed Effects:
##         (Intr)
## scTrial 0.000
```

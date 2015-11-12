# Darabolás és egyesítés

Gyakran előfordul, hogy bizonyos (faktor)változók mentén fel akarjuk 
darabolni az adattáblánkat, és ugyanazon elemzéseket akarjuk elvégezni minden 
egyes résztáblán.

- pl. a diszlexiás adataink darabolása a csoport változó mentén

```r
data(dyslex)
groups <- split(dyslex, dyslex$csoport)
```

- standardizáljuk az olvasás változókat csoportonként

```r
groups <- lapply(groups, 
                 function(x) {
                     vars <- grep("olv_", colnames(x))
                     x[, vars] <- scale(x[, vars])
                     x}
                 )
```

- egyesítés egy data.frame-mé

```r
all <- Reduce("rbind", groups)
```

- előfordul, hogy van két adattáblánk ugyanazon megfigyelési egységektől
származó adatokkal, amelyeket egyesíteni szeretnénk (angolul *merge*)

```r
# hozzuk megint létre a dyslex_read és dyslex_spell adattáblákat, 
# de most az olvasási adatokat ne szűrjük
dyslex_read <- subset(dyslex, 
                      select = -(sp_helyes1:sp_helyes5))
dyslex_spell <- subset(dyslex, 
                       kor < 145 & oszt <= 4, 
                       select = c(id, sp_helyes1:sp_helyes5))

# egyesítés (csak a közös személyek)
dyslex_merged1 <- merge(dyslex_read, dyslex_spell, by = "id")

# egyesítés (mindenki)
dyslex_merged2 <- merge(dyslex_read, dyslex_spell, by = "id", all = TRUE)
```

### dplyr

- elemzés csoportok mentén

```r
library(dplyr)
groups <- 
    tbl_df(dyslex) %>%
        group_by(csoport) %>%
        mutate(olv_helyes1 = scale(olv_helyes1), 
               olv_helyes2 = scale(olv_helyes2),
               olv_helyes3 = scale(olv_helyes3))
```

- merge

```r
# csak a kozos szemelyekre
inner_merged <- inner_join(dyslex_read, dyslex_spell)

# mindenkire
full_merged <- full_join(dyslex_read, dyslex_spell)
```

### data.table

- elemzés csoportok mentén

```r
library(data.table)

# egy valtozora
groups <- data.table(dyslex)
groups[, olv_helyes1 := scale(olv_helyes1), by = csoport]

# tobbre
vars <- c("olv_helyes1", "olv_helyes2", "olv_helyes3")
groups <- data.table(dyslex)[,
                             (vars) := scale(get(vars)),
                             by = csoport]
```

- merge

```r
# alakitsuk at, hogy data.table legyen
dyslex_read <- setDT(dyslex_read, key = "id")
dyslex_spell <- setDT(dyslex_spell, key = "id")

# a data.table-nek van sajat merge() metodusa, de igy a legtomorebb:
merged1 <- dyslex_read[dyslex_spell]
merged2 <- dyslex_spell[dyslex_read, , nomatch = NA]
```


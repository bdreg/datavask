

```r
## Diabetes ketoacidose (DKA)

## Datakilde
lokalDT <- lok2018dt1
```

```
## Error in eval(expr, envir, enclos): object 'lok2018dt1' not found
```

```r
## Aggrigerer
dkaTab <- groupingsets(lokalDT,
  j = .(N = sum(!is.na(und_ketoacidose)),
       ja = length(which(und_ketoacidose == "Ja"))),
  by = c("agecat", "agekat"),
  sets = list(c("agecat", "agekat"), character(0))
)
```

```
## Error in groupingsets(lokalDT, j = .(N = sum(!is.na(und_ketoacidose)), : could not find function "groupingsets"
```

```r
dkaTab[, pros := as.character(round(ja / N * 100, digits = 1))]
```

```
## Error in eval(expr, envir, enclos): object 'dkaTab' not found
```

```r
dkaTab[ja == 0, pros := "- "]
```

```
## Error in eval(expr, envir, enclos): object 'dkaTab' not found
```

```r
dkaTab[is.na(agecat), agecat := "Totalt"]
```

```
## Error in eval(expr, envir, enclos): object 'dkaTab' not found
```

```r
## lager id til sortering
dkaTab[is.na(agekat), agekat := nrow(dkaTab) * 2] #gir høyeste tall så det ligger altid nedest
```

```
## Error in eval(expr, envir, enclos): object 'dkaTab' not found
```

```r
setorder(dkaTab, agekat) #reorder rows
```

```
## Error in setorder(dkaTab, agekat): could not find function "setorder"
```

```r
## Justeringer
dkaTab[, agekat := NULL]
```

```
## Error in eval(expr, envir, enclos): object 'dkaTab' not found
```

```r
setcolorder(dkaTab, c("agecat", "ja", "pros", "N"))
```

```
## Error in setcolorder(dkaTab, c("agecat", "ja", "pros", "N")): could not find function "setcolorder"
```

```r
setnames(dkaTab, names(dkaTab), c("Alder kategorier", "Antall", "Andel", "N"))
```

```
## Error in setnames(dkaTab, names(dkaTab), c("Alder kategorier", "Antall", : could not find function "setnames"
```

```r
## Tabell
dkaTabell <- tabFun(dkaTab, "Har hatt ketoacidose", total = TRUE)
```

```
## Error in tabFun(dkaTab, "Har hatt ketoacidose", total = TRUE): could not find function "tabFun"
```


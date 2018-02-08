---
title       : Andmestiku sorteerimine
description : Sorteerimine

--- type:NormalExercise lang:r xp:100 skills:1 key:d54982584e
## Sorteerimine

Ühe vektori väärtuste sorteerimiseks saab kasutada käsku `sort`, käsk annab tulemuseks järjestatud väärtused.

Käsk `order` annab väljundiks sorteerimisreegli: kuhu peaksime vastavate indeksitega elemendid vektoris/andmetabelis ümber tõstma, et saada kasvavas(kahanevas) järjestuses tulemus. 

Käsule `order` saab argumendiks anda rohkem kui ühe vektori, oluline on siis vektorite järjekord käsus.  Näiteks `order(x, y, z)` annab sellise indeksite järjekorra
kus elemendid on esmalt järjestatud `x` järgi, kui mingid `x` väärtused langevad kokku, siis nende järjestus määratakse `y` väärtuste põhjal, kui kokkulangevate `x` väärtuste korral esineb ka võrdseid `y` väärtuseid, siis nende järjestus määratakse `z` põhjal.



Töölaual on vektorid `x` ja `y` ning andmestik `xy`.



*** =instructions
- **Ülesanne 1** Sorteeri andmestik `xy` kasvavalt `x` ja `y` järgi, kasuta selleks `order` käsku. Omista sorteeritud andmestik muuutujale `xy1`, prindi ekraanile.
- **Ülesanne 2** Moodusta andmestik `xy2`, selleks anna andmestikule `xy` ridade järjestus ette käsuga `order(x, -y)`. Prindi tulemus ekraanile.
- **Ülesanne 3** Võrdle kahte tulemust, milles seisneb erinevus? 


*** =hint
- Andmestiku sorteerimiseks määra `order` käsu tulemuse abil andmestiku ridade järejstus: `andmestik[order(x, y),]`.

*** =pre_exercise_code
```{r}
x <- c(2:1, 2:1, 2:1, 4)
y <- c(7, 1, 5, 2, 6, 3, 4)
xy <- data.frame(x, y)
```

*** =sample_code
```{r}
# Vaata vektorite x, y ja andmestiku xy sisu
x; y; xy

# Ülesanne 1: andmestiku sorteerimine kasvavalt
xy1 <- xy[_____, ]
xy1


# Ülesanne 2: ridade järjestus order(x, -y) põhjal
xy2 <- xy[_____, ]
xy2


# Ülesanne 3: Milles seisneb erinevus? (vastust kirja ei pea panema)

```

*** =solution
```{r}
# Vaata vektorite x, y ja andmestiku xy sisu
x; y; xy

# Ülesanne 1: andmestiku sorteerimine kasvavalt
xy1 <- xy[order(x, y), ]
xy1


# Ülesanne 2: ridade järjestus order(x, -y) põhjal
xy2 <- xy[order(x, -y), ]
xy2


# Ülesanne 3: Milles seisneb erinevus? (vastust kirja ei pea panema)



```

*** =sct
```{r}
test_predefined_objects("x", 
                        eq_condition = "equivalent",
                        eval = TRUE,
                        undefined_msg = "Oled muutuja `x` kustutanud! Alusta uuesti.", 
                        incorrect_msg = "Oled  `x` väärtuseid muutnud! Alusta uuesti.")


test_predefined_objects("y", 
                        eq_condition = "equivalent",
                        eval = TRUE,
                        undefined_msg = "Oled muutuja `y` kustutanud! Alusta uuesti.", 
                        incorrect_msg = "Oled  `y` väärtuseid muutnud! Alusta uuesti.")


test_predefined_objects("xy", 
                        eq_condition = "equivalent",
                        eval = TRUE,
                        undefined_msg = "Oled andmestiku `xy` kustutanud! Alusta uuesti.", 
                        incorrect_msg = "Oled  andmestiku `xy` väärtuseid muutnud! Alusta uuesti.")




####

test_object("xy1", 
            undefined_msg = "Muutuja  `xy1` on defineerimata.",
            incorrect_msg = "Andmestik  `xy1`  ei ole korrektne. Proovi uuesti." )


test_object("xy2", 
            undefined_msg = "Muutuja  `xy2` on defineerimata.",
            incorrect_msg = "Andmestik  `xy2`   ei ole korrektne. Proovi uuesti." )



test_function(name = "order",
              args = NULL,
              index = 2,
             eq_condition = "equivalent",
             not_called_msg = "Mõlemas ülesandes on vaja kasutada käsku `order`.") 


#
success_msg("Tubli!")

```








--- type:NormalExercise lang:r xp:100 skills:1 key:253fd59b42
##  Andmestiku sorteerimine 1

Töölaual on andmestik `iris`.


*** =instructions

- **Ülesanne 1** Järjesta andmestik `iris` kasvavasse järjestusse tunnuste `Sepal.Width`, `Sepal.Length` ja `Petal.Width` järgi.  Omista tulemus muutujale `iris.sort1`.
- **Ülesanne 2** Mis sorti iiris on eelviimasel kohal? Omista sordi nimi muuutujale `eelviimane`.


*** =hint
- Anna esimeses ülesandes funktsiooni `order` argumentideks tunnused `Sepal.Width`, `Sepal.Length` ja `Petal.Width` (selles järjekorrras).
- Andmestiku lõpu vaatamiseks kasuta  näiteks funktsiooni `tail`.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# vaata andmestikku
head(iris)

# Ülesanne 1: sorteerimine
iris.sort1 <- iris[____, ]

# ülesanne 2: eelviimase lille sort
eelviimane <- "_______"


```

*** =solution
```{r}
# vaata andmestikku
head(iris)

# Ülesanne 1: sorteerimine
iris.sort1 <- iris[order(iris$Sepal.Width, iris$Sepal.Length, iris$Petal.Width), ]

# ülesanne 2: eelviimase lille sort
eelviimane <- "setosa"


```

*** =sct
```{r}
# 1
test_function(name = "order", 
              args = NULL,
              index = 1,
             eq_condition = "equivalent",
             not_called_msg = "Esimeses ülesandes pead kasutama funktsiooni `order`.",
             args_not_specified_msg = NULL,
             incorrect_msg = NULL)


test_object("iris.sort1", 
            undefined_msg = "Andmestik `iris.sort1` on defineerimata.",
            incorrect_msg = "Andmestiku `iris.sort1` sisu ei ole korrektne. Proovi uuesti." )


# 2
test_object("eelviimane", 
            undefined_msg = "Muutuja  `eelviimane` on defineerimata.",
            incorrect_msg = "Muutuja  `eelviimane` väärtus ei ole korrektne. Proovi uuesti." )




#
success_msg("Hästi!")



```





--- type:NormalExercise lang:r xp:100 skills:1 key:90c0772430
##  Andmestiku sorteerimine 2

Töölaual on andmestik `iris`.



*** =instructions
- **Ülesanne 1** Järjesta andmestik `iris`  nii, et vaatlused oleks tunnuse `Sepal.Width` järgi järjestatud ksavavalt ning need vaatlused, mil on kroonlehe laius sama, oleksid tunnuse `Sepal.Length` järgi järjestatud kahanevasse järjestusse. Omista sorteeritud andmestik muutujale `iris.sort2`. 
- **Ülesanne 3** Mis sorti iiris on sorteeritud andmestikus 30 kohal? Omista selle sordi nimi muutujale `kolmekymnes`.

*** =hint
- Kui andmestikku on vaja sorteerida ühe tunnuse järgi kasvavalt ja teise järgi kahanevalt, siis saad `order` käsus lisada miinusmärgi selle tunnuse nime ette, mille järgi tuleb sorteerida kahanevalt (tingimusel, et `decreasing = FALSE`). See abinõu sobib aga ainult siis kui tegu on arvtunnustega!
- Kolmekymnenda vaatluse nägemiseks: `iris.sort2[30,]`


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# vaata andmestikku
head(iris)

# Ülesanne 1: sorteerimine
iris.sort2 <- iris[____, ]

# ülesanne 2: kolmekümnenda lille sort
kolmekymnes <- "_______"

```

*** =solution
```{r}
# vaata andmestikku
head(iris)

# Ülesanne 1: sorteerimine
iris.sort2 <- iris[order(iris$Sepal.Width, -iris$Sepal.Length ), ]

# ülesanne 2: kolmekümnenda lille sort
kolmekymnes <- "virginica"

```

*** =sct
```{r}
# 1
test_function(name = "order", 
              args = NULL,
              index = 1,
             eq_condition = "equivalent",
             not_called_msg = "Esimeses ülesandes pead kasutama funktsiooni `order`.",
             args_not_specified_msg = NULL,
             incorrect_msg = NULL)


test_object("iris.sort2", 
            undefined_msg = "Andmestik `iris.sort2` on defineerimata.",
            incorrect_msg = "Andmestiku `iris.sort2` sisu ei ole korrektne. Kontrolli, kuidas andsid ette `order` käsu argumendid, ja proovi uuesti." )


# 2
test_object("kolmekymnes", 
            undefined_msg = "Muutuja  `kolmekymnes` on defineerimata.",
            incorrect_msg = "Muutuja  `kolmekymnes` väärtus ei ole korrektne. Proovi uuesti." )




#
success_msg("Hästi! Pane tähele, et sel viisil suuna muutmine sorteerimisel on võimalik arvtunnuste korral.")







```

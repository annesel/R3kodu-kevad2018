---
title       : Faktor-tüüpi tunnus
description : Faktor-tüüpi tunnuse kasutamine
--- type:NormalExercise lang:r xp:100 skills:1 key:35f7f6fc0f
## Faktori tasemete järjestamine 

Töölaual on andmestik `iris`. Andmed on kolme sort iiriste(lilled mitte kommid!) õie mõõtmete kohta. Mõõdetud on õielehtede (kroonlehed - ik *petal*, tupplehed - ik *sepal*) pikkus ja laius sentimeetrites.


Vaata kõigepealt käsuga `summary(iris)` andmestiku ülevaadet. Tunnus `Species` näitab iirise sorti.


*** =instructions
- **Ülesanne 1** Käsu `by` abil leia kõigi kolme iirisesordi kroonlehe keskmine pikkus (kroonlehe pikkus `Petal.Length`), omista saadud vastus muutujale `keskmised`, prindi selle väärtus ekraanile.
- **Ülesanne 2** Millise sordi kroonlehed on keskmiselt kõige lühemad? Omista selle sordi nimi muuutjale `kroonlehed1`.
- **Ülesanne 3** Kasutades `factor` käsku lisa andmestikku tunnus nimega `sordinimi`, mis oleks sama sisuga kui `Species`, kuid mille väärtuste järjekord oleks: `versicolor`, `setosa`, `virginica`.
- **Ülesanne 4** Kasutades `tapply` käsku leia maksimaalsed kroonlehe pikkused igal sordil, tulemuste järjestus muutujas `maksimumid` olgu järgmine: `versicolor`, `setosa`, `virginica`. Prindi muutuja väärtus ekraanile. Käsu `tapply` kirjapilt `tapply(uuritavtunnus, grupitunnus, funktsioon)`.


*** =hint
- `by` käsu kirjapilt on järgmine: `by(uuritavtunnus, grupitunnus, funktsioon)`.
- Faktori tasemete ümberjärjestamiseks kasuta `factor` käsku, andes argumendile `levels` väärtuseks sordinimede vektori nõutud järjestuses.


*** =pre_exercise_code
```{r}
#
```

*** =sample_code
```{r}
# Vaata esmalt andmestikust ülevaadet
summary(iris)


# Ülesanne 1: Leia keskmised kroonlehepikkused käsu by abil
keskmised <- by(_______________)
keskmised


# Ülesanne 2: Mis sordil keskmiselt kõige lühemad kroonlehed
kroonlehed1 <- "_________"


# Ülesanne 3: Muuda sordinimede järjestust, tekita selleks uus tunnus
iris$sordinimi <- ____________________________


# Ülesanne 4: Leia maksimaalne kroonlehe pikkus sortide kaupa, sordid olgu uues järjestuses
maksimumid <- tapply(____________)
maksimumid
```




*** =solution
```{r}
# Vaata esmalt andmestikust ülevaadet
summary(iris)


# Ülesanne 1: Leia keskmised kroonlehepikkused käsu by abil
keskmised <- by(iris$Petal.Length, iris$Species, mean)
keskmised


# Ülesanne 2: Mis sordil keskmiselt kõige lühemad kroonlehed
kroonlehed1 <- "setosa"


# Ülesanne 3: Muuda sordinimede järjestust, tekita selleks uus tunnus
iris$sordinimi <- factor(iris$Species, levels = c("versicolor", "setosa", "virginica"))


# Ülesanne 4: Leia maksimaalne kroonlehe pikkus sortide kaupa, sordid olgu uues järjestuses
maksimumid <- tapply(iris$Petal.Length, iris$sordinimi, max)
maksimumid
```

*** =sct
```{r}
# 1
test_function(name = "by",
              args = c("data", "INDICES", "FUN"),
              index = 1,
             eq_condition = "equivalent",
             not_called_msg = "Esimeses ülesandes pead kasutama funktsiooni `by`.",
             args_not_specified_msg = paste("Käsus `by` on vaja ", 
             c("esimeseks argumendiks panna uuritav tunnus", 
             "teiseks argumendiks vaja määrata grupeeriv tunnus", 
             "kolmandaks argumendiks panna selle funktsiooni nimi, mida tahame uuritavale tunnusele rakendada")),
             incorrect_msg = paste("Käsus `by` on praegu ", 
             c("esimene argument  vale.",
             "teine argument vale.", 
             "kolmas argument vale, kirjuta kolmandale kohale funktsiooni nimi `mean`."))) 


test_object("keskmised", 
            undefined_msg = "Muutuja  `keskmised` on defineerimata.",
            incorrect_msg = "Muutuja  `keskmised` väärtus ei ole korrektne. Proovi uuesti." )


# 2
test_object("kroonlehed1", 
            undefined_msg = "Muutuja  `kroonlehed1` on defineerimata.",
            incorrect_msg = "Muutuja  `kroonlehed1` väärtus ei ole korrektne. Proovi uuesti." )


# 3
test_function(name = "factor",
              args = c("levels"),
              index = 1,
             eq_condition = "equivalent",
             not_called_msg = "Kolmandas ülesandes pead kasutama funktsiooni `factor`.",
             args_not_specified_msg = "Käsus `factor` pead määrama argumendi `levels` väärtuse.",
             incorrect_msg = "Käsus `factor` on argumendi `levels` väärtus vale, see peaks olema vektor nõutud järjekorras sordinimedega.") 


test_data_frame("iris", columns = c("sordinimi"),
                undefined_msg = "Ära kustuta andmstikku `iris`!",
                undefined_cols_msg = "Kas oled andmestikku `iris` lisanud veeru `sordinimi`?",
                incorrect_msg = "Kas oled uue faktori `sordinimi` õigesti väärtustanud ?")



# 4
test_function(name = "tapply",
              args = c("X", "INDEX", "FUN"),
              index = 1,
             eq_condition = "equal",
             not_called_msg = "Viimases ülesandes pead kasutama funktsiooni `tapply`.",
             args_not_specified_msg = paste("Käsus `tapply` on vaja ", 
             c("esimeseks argumendiks panna uuritav tunnus", 
             "teiseks argumendiks vaja määrata grupeeriv tunnus",
             "kolmandaks argumendiks panna selle funktsiooni nimi, mida tahame uuritavale tunnusele rakendada")),
             incorrect_msg = paste("Käsus `tapply` on praegu ", 
             c("esimene argument  vale.",
             "teine argument vale, pane selleks eelmises punktis loodud tunnus.", 
             "kolmas argument vale, kirjuta kolmandale kohale funktsiooni nimi `max`."))) 


test_object("maksimumid", 
            undefined_msg = "Muutuja  `maksimumid` on defineerimata.",
            incorrect_msg = "Muutuja  `maksimumid` väärtus ei ole korrektne. Proovi uuesti." )

 



#
success_msg("Tubli! Esimesed ülesanded on tehtud.")


```






















--- type:NormalExercise lang:r xp:100 skills:1 key:4229ba4b81
## Faktor-tunnuse loomine arvtunnusest


Töölaual on andmestik `iris`. Andmed on kolme sort iiriste(lilled mitte kommid!) õie mõõtmete kohta. Mõõdetud on õielehtede (kroonlehed - ik *petal*, tupplehed - ik *sepal*) pikkus ja laius sentimeetrites.


Kui arvtunnuse väärtused on vaja jagada intervallidesse, siis saab kasutada käsku `cut`. Loodav tunnus on faktor-tüüpi. 

 


*** =instructions
- **Ülesanne 1** Jaga kroonlehtede pikkuse tunnus `Petal.Length` intervallidesse, selleks tekita uus tunnus `intervallid`. Intervallid olgu pikkusega 0.5 sentimeetrit ja kujul: `[1, 1.5)`, `[1.5, 2)` jne kuni `[6.7, 7)`. Ära tekkivate faktoritasemete silte muuda.
- **Ülesanne 2** Kontrolli, kas uus tunnus `intervallid` on ikka faktor-tüüpi. Pane kirja, mis funktsiooniga saab faktor-tüübile vastavust kontrollida.
- **Ülesanne 3** Leia uue tunnuse sagedustabel. Omista see muutujale `sagedustabel` ja prindi ekraanile.
- **Ülesanne 4** Vaata sagedustebelist mitu intervalli jäi tühjaks? Omista tühjade intervallide arv muutujale `tyhjad`.


*** =hint
- Vaata `cut` käsu abifaili, loe milleks saab kasutada argumenti `right`.
- Ära määra `cut` käsus argumenti `labels`.


*** =pre_exercise_code
```{r}
#pole
```



*** =sample_code
```{r}
# Vaata esmalt andmestikust ülevaadet
summary(iris)


#Ülesanne 1 Jaga kroonlehtede pikkus intervallidesse
intervallid <- cut(______________)


#Ülesanne 2: Kas muutuja intervallid on faktor-tüüpi?
__.______(intervallid)


#Ülesanne 3: Sagedustabel
sagedustabel <- ________(intervallid)
sagedustabel


#Ülesanne 4: Mitu tühja intervalli tekkis?
tyhjad <- __

```



*** =solution
```{r}
# Vaata esmalt andmestikust ülevaadet
summary(iris)


#Ülesanne 1 Jaga kroonlehtede pikkus intervallidesse
intervallid <- cut(iris$Petal.Length, br = seq(1, 7, 0.5),  right = FALSE)


#Ülesanne 2: Kas muutuja intervallid on faktor-tüüpi?
is.factor(intervallid)


#Ülesanne 3: Sagedustabel
sagedustabel <- table(intervallid)
sagedustabel


#Ülesanne 4: Mitu tühja intervalli tekkis?
tyhjad <- 2


```



*** =sct
```{r}
# 1
test_function(name = "cut",
              args = c("x", "breaks", "right"),
              index = 1,
             eq_condition = "equivalent",
             not_called_msg = "Esimeses ülesandes pead kasutama funktsiooni `cut`.",
             args_not_specified_msg = paste("Käsus `cut` on vaja ", 
             c("esimeseks argumendiks panna intervallidesse jagatav tunnus", 
             "teiseks argumendiks  määrata lõikepunktid", 
             "määrata   argumendi `right` väärtus.")),
             incorrect_msg = paste("Käsus `cut` on praegu ", 
             c("esimene argument vale.", 
             "lõikepunktid valed.", 
             "intervallide kuju vale, muuda argumendi `right` väärtus."))) 


test_object("intervallid", 
            undefined_msg = "Muutuja `intervallid` on defineerimata.",
            incorrect_msg = "Muutuja `intervallid` väärtus ei ole korrektne. Proovi uuesti." )


# 2
test_function(name = "is.factor", 
              args = c("x"),
              index = 1,
             eq_condition = "equivalent",
             not_called_msg = "Teises ülesandes pead kasutama funktsiooni `is.factor`.",
             args_not_specified_msg = NULL,
             incorrect_msg = "Funktsioonile `is.factor` on antud vale argument.")

# 3
test_function(name = "table", 
                args = NULL,
              index = 1,
             eq_condition = "equivalent",
             not_called_msg = "Kolmandas ülesandes pead kasutama funktsiooni `table`.",
             args_not_specified_msg = NULL,
             incorrect_msg = "Funktsioonile `table` on antud vale argument.")

test_object("sagedustabel", 
            undefined_msg = "Muutuja  `sagedustabel` on defineerimata.",
            incorrect_msg = "Muutuja  `sagedustabel` väärtus ei ole korrektne. Proovi uuesti." )



#4
test_object("tyhjad", 
            undefined_msg = "Muutuja  `tyhjad` on defineerimata.",
            incorrect_msg = "Muutuja  `tyhjad` väärtus ei ole korrektne. Proovi uuesti." )





success_msg("Hästi!")



```

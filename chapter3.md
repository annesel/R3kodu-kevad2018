---
title       : Andmestiku kuju teisendused
description : Andmestiku kuju teisendused

--- type:NormalExercise lang:r xp:100 skills:1 key:d43bfcf37a
## Andmestiku viimine pikka formaati

Töölaual on olemas andmestik `B`. Andmestikus on 160 inimese kohta mitmete testide (40 testi) tulemused.



*** =instructions
- **Ülesanne 1** Aktiveeri pakett `reshape2`.
- **Ülesanne 2** Kasutades käsku `melt` vii andmestik `B` pikale kujule, nii, et iga uuritava kohta tekib andmestikku 40 rida. Nimeta uus andmestik nimega `testid.pikk`. Andmestikus peab säilima inimese identifiakaator `id` kuid välja jääma testi tüübi tunnus `grupp`.
- **Ülesanne 3** Vaata uue andmestiku struktuuri käsuga `str`.

*** =hint
- Käsus `melt` määra argumentide `measure.vars` ja  `id.vars` väärtus. `id.vars` on need tunnused, mida me andmestiku kuju muutes ümberpaigutada ei taha.  

*** =pre_exercise_code
```{r}
B <-  read.csv2(file = "http://kodu.ut.ee/~annes/R/B.csv",   nrows = 160, stringsAsFactors = T)
B <- B[, substr(names(B), 1, 3) %in% c("id", "gru", "tes") ]
```

*** =sample_code
```{r}
# Vaata andmestiku kirjeldust
str(B)

# Ülesanne 1: aktiveeri lisapakett
______(reshape2)


# ÜLesanne 2: vii andmestik pikale kujule
testid.pikk <- melt(_______________________)
_____(testid.pikk)


```

*** =solution
```{r}
# Vaata andmestiku kirjeldust
str(B)

# Ülesanne 1: aktiveeri lisapakett
library(reshape2)


# ÜLesanne 2: vii andmestik pikale kujule
testid.pikk <- melt(B, measure.vars = 3:42, id.vars = 1)
str(testid.pikk)


```

*** =sct
```{r}
# 1
test_function(name = "library", 
              args = "package",
              index = 1,
              eval = FALSE,
              eq_condition = "equivalent",
              not_called_msg = "Esimeses ülesandes pead kasutama funktsiooni `library`.",
              args_not_specified_msg = "Käsule `library` tuleb argumendiks anda paketi nimi.",
              incorrect_msg =  "Käsu `library` argumendiks anna paketi nimi  `reshape2`")



#2
test_function(name = "melt", 
              args = c("data", "id.vars", "measure.vars"),
              index = 1,
              eq_condition = "equivalent",
              not_called_msg = "Teises ülesandes pead kasutama funktsiooni `melt`.",
              args_not_specified_msg = paste("Käsule `melt` läheb " , 
                                             c("esimeseks argumendiks andmestiku nimi",
                                               " üheks argumendiks  `id.vars`, mille kaudu saab määrata tunnused, mis teisendamisel paika jätta. Tunnusenimed kirjuta siin jutumärkidesse või anna ette sobiva veeruindeksid.", 
                                               " üheks argumendiks  `measure.vars`, mille kaudu saab määrata tunnused, mille väärtused tõstetakse ühte veergu.")),
              incorrect_msg =   paste("Käsus `melt` on  " , 
                                      c("vale andmestik",
                                        "`id.vars` argumendi väärtus vale.", 
                                        "`measure.vars` argumendi väärtus vale.")))


test_object("testid.pikk", 
            undefined_msg = "Andmestik  `testid.pikk` on defineerimata.",
            incorrect_msg = "Andmestik  `testid.pikk` sisu ei ole korrektne. Proovi uuesti." )

# 3
test_function(name = "str", 
              args = "object",
              index = 1,
              eq_condition = "equivalent",
              not_called_msg = "Viimases ülesandes pead kasutama funktsiooni `str`.",
              args_not_specified_msg = "Käsule `str` läheb argumendiks andmestiku nimi.",
              incorrect_msg =  "Oled `str` argumendiks andnud vale andmestiku.")


#
success_msg("Hästi!")


```


--- type:NormalExercise lang:r xp:100 skills:1 key:3844f1cfc1
## Andmestiku viimine laia formaati

Töölaual on andmestik `rotid`. Rotid on jagatud 3 gruppi, iga grupp sai erinevat toitu (`Diet`). Sööda mõju uurimiseks kaaluti rotid korduvalt, mõõtmisajad on kirjas tunnuses `Time` (aeg päevades katse algusest) kaal grammides on toodud veerus `weight`.


*** =instructions
- **Ülesanne 1** Aktiveeri pakett `reshape2`.
- **Ülesanne 2** Kasutades käsku `dcast` vii andmestik `rotid` sellisele kujule, et iga roti kaalumõõtmised oleksid ühes reas, koos roti identifikaatori(`Rat`) ja söödatüübiga (`Diet`). Omista uus andmestik muutujale `rotid.lai`. 
- **Ülesanne 3** Prindi uus andmestik ekraanile.



*** =hint
- Käsus `dcast` on argument `value.var`, mille abil saab ette anda selle tunnuse nime, mille väärtuseid kasutatakse ridade täitmisel.
- Käsus `dcast` on ridade-veergude paigutus määratud: `formula = Rat + Diet ~ Time` kaudu.

*** =pre_exercise_code
```{r}
# nlme paketist
library(nlme)
library(stringr)
rotid <- as.data.frame(BodyWeight)
rotid$Rat <- paste0("no", str_pad(rotid$Rat, width = 2, "left", pad = "0"))
rotid$Time <- paste0("day", str_pad(rotid$Time, width = 2, "left", pad = "0"))
indeks <- c(25:33, 76:77, 160:165)
rotid <- rotid[-indeks,]
rm(indeks)
```

*** =sample_code
```{r}
# vaata andmestikku
summary(rotid)

# Ülesanne 1: aktiveeri lisapakett
______(reshape2)


# Ülesanne 2: vii andmestik laiale kujule
rotid.lai <- dcast(_______________________)

# Ülesanne 3: prindi uus andmestik ekraanile
____________

```

*** =solution
```{r}
# vaata andmestikku
summary(rotid)

# Ülesanne 1: aktiveeri lisapakett
library(reshape2)


# Ülesanne 2: vii andmestik laiale kujule
rotid.lai <- dcast(rotid, Rat + Diet ~ Time, value.var = "weight")


# Ülesanne 3: prindi uus andmestik ekraanile
rotid.lai 

```

*** =sct
```{r}
# 1
test_function(name = "library", 
              args = "package",
              index = 1,
              eval = FALSE,
              eq_condition = "equivalent",
              not_called_msg = "Esimeses ülesandes pead kasutama funktsiooni `library`.",
              args_not_specified_msg = "Käsule `library` tuleb argumendiks anda paketi nimi.",
              incorrect_msg =  "Käsu `library` argumendiks anna paketi nimi  `reshape2`")


#2
test_function(name = "dcast", 
              args = c("data", "formula", "value.var"),
              index = 1,
              eq_condition = "equivalent",
              not_called_msg = "Teises ülesandes pead kasutama funktsiooni `dcast`.",
              args_not_specified_msg = paste("Käsku `dcast` läheb " , 
                                             c("esimeseks argumendiks andmestiku nimi",
                                               " üheks argumendiks  `formula`, mille kaudu saab määrata nö rea ja veertunnused.", 
                                               " üheks argumendiks  `value.var`, mille kaudu saab määrata tunnuse, mille väärtusega laia tabeli read täidetakse.")),
              incorrect_msg =   paste("Käsus `dcast` on  ", 
                                      c("vale andmestik",
                                        "`formula` argumendi väärtus vale.", 
                                        "`value.var` argumendi väärtus vale, pane selleks kaalu tunnus.")))


test_object("rotid.lai", 
            undefined_msg = "Andmestik  `rotid.lai` on defineerimata.",
            incorrect_msg = "Andmestik  `rotid.lai` sisu ei ole korrektne. Proovi uuesti." )

# 3
test_output_contains("rotid.lai", incorrect_msg = "Uus andmestik on ekraanile printimata.")


#
success_msg("Hästi! Viimasest tabelist näed, et kõiki rotte pole kaalutud sama arv kordi.")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:8a253e656c
## Andmestiku agregeerimine 1

Töölaual on sama andmestik `rotid`.  Pakett `reshape2` on juba aktiveeritud


*** =instructions
- **Ülesanne 1** Mitu korda on iga rotti kaalutud? Leia sagedustabel tunnusele `rotid$Rat`, omista tabel muutujale `tabel1`, prindi see ekraanile.
- **Ülesanne 2** Kasutades funktsiooni `dcast` leia samad näitajad andmetabelisse st teisenda andmestikku `rotid` nii, et  tulemuseks olevas andmetabelis oleks ühes veerus rottide indikaatorid ja teises igal rotil tehtud mõõtmiste arv (selle veeru nimi olgu `"mootmisi"`). Omista saadud tulemus muutujale `tabel2`, prindi see ekraanile.
- **Ülesanne 3** Mitu rotti on enne katse lõppu katkestanud, st mitmel pole kõiki 11 mõõtmist? Omista nende rottide arv muutujale `katkestajaid`.


*** =hint
- Käsus `dcast` käsus saad arvutatavale veerule nime panemiseks käsu argumendi `formula` kirja panna nii `reatunus1 + reatunnus2 ~ "uustunnus"`.
- Kui rea- ja veertunnuste valem on selline, et ühte lahtrisse peaks minema mitu väärtust, siis vaikimisi leitakse nende väärtuste arv ja esitatakse tabelis st `fun.aggregate` väärtuseks on vaikimisi vektori pikkuse leidmise funktsioon. Seda siin ülesandes peaksi kasutama.

*** =pre_exercise_code
```{r}
# nlme paketist
library(nlme)
library(stringr)
rotid <- as.data.frame(BodyWeight)
rotid$Rat <- paste0("no", str_pad(rotid$Rat, width = 2, "left", pad = "0"))
rotid$Time <- paste0("day", str_pad(rotid$Time, width = 2, "left", pad = "0"))
indeks <- c(25:33, 76:77, 160:165)
rotid <- rotid[-indeks,]
rm(indeks)

library(reshape2)

```

*** =sample_code
```{r}
# vaata andmestikku
summary(rotid)

# Ülesanne 1: Leia sagedustabel
tabel1 <- ________________
tabel1


# ÜLesanne 2: Leia samad näitajad käsu dcast abil
tabel2 <- dcast(_______________________)
tabel2


# Ülesanne 3: Kui palju on katkestajaid
katkestajaid <- _______

```



*** =solution
```{r}
# vaata andmestikku
summary(rotid)

# Ülesanne 1: Leia sagedustabel
tabel1 <- table(rotid$Rat)
tabel1


# ÜLesanne 2: Leia samad näitajad käsu dcast abil
tabel2 <- dcast(rotid, Rat ~ "mootmisi")
tabel2


# Ülesanne 3: Kui palju on katkestajaid
katkestajaid <- 3
```



*** =sct
```{r}
# 1
test_function(name = "table", 
              args = NULL,
              index = 1,
              eq_condition = "equivalent",
              not_called_msg = "ESiemses ülesandes pead kasutama funktsiooni `table`.",
              args_not_specified_msg = NULL,
              incorrect_msg = "Funktsioonile `table` on antud vale argument.")

test_object("tabel1", 
            undefined_msg = "Sagedustabel `tabel1` on defineerimata.",
            incorrect_msg = "Sagedustabeli `tabel1` väärtus ei ole korrektne. Proovi uuesti." )

test_output_contains("tabel1", incorrect_msg = "Sagedustabel on ekraanile printimata.")



#2
test_function(name = "dcast", 
              args = c("data", "formula"
              #, "fun.aggregate"
              ),
              index = 1,
              eq_condition = "equivalent",
              not_called_msg = "Teises ülesandes pead kasutama funktsiooni `dcast`.",
              args_not_specified_msg = paste("Käsku `dcast` läheb " , 
                                             c("esimeseks argumendiks andmestiku nimi",
                                               " üheks argumendiks  `formula`, valem mille kaudu saab määrata nö rea ja veertunnused."
                                               #," üheks argumendiks  `fun.aggregate`, mille kaudu saab määrata funktsiooni mille tulemus lahtrites esitada."
                                               )),
              incorrect_msg =   paste("Käsus `dcast` on  ", 
                                      c("vale andmestik",
                                        "`formula` argumendi väärtus vale."
                                        #, "`fun.aggregate` argumendi väärtus vale, pane selleks `length`, siis loetakse toimunud mõõtmised kokku."
                                        )))


test_data_frame("tabel2", columns = "mootmisi",
            undefined_msg = "Andmetabel `tabel2` on defineerimata.",
            undefined_cols_msg = "Andmestikus `tabel2` pole veergu nimega `mootmisi`.",
            incorrect_msg = "Andmetabeli `tabel2`  veeru `mootmisi` väärtus ei ole korrektne. Proovi uuesti." )


test_output_contains("tabel2", incorrect_msg = "`dcast` funtksiooni tulemus `tabel2` on ekraanile printimata.")




#3
test_object("katkestajaid", 
            undefined_msg = "Muutuja `katkestajaid` on defineerimata.",
            incorrect_msg = "Muutuja `katkestajaid` väärtus ei ole korrektne. Proovi uuesti." )



success_msg("Hästi! Siin ülesandes võis `dcast` funktsioonis argumentide `fun.aggregate` ja `value.var` väärtused jätta täpsustamata, kuna vaikimisi väärtused olid sobivad.")

```



--- type:NormalExercise lang:r xp:100 skills:1 key:5d55f0973a
## Andmestiku agregeerimine 2

Töölaual on sama andmestik `rotid`.  Pakett `reshape2` on juba aktiveeritud.

 


*** =instructions
- **Ülesanne 1** Kasutades funktsiooni `dcast` leia tabel, kus rotid on grupeeritud vastavalt dieedile ja igale rotile on leitud tema kaalude mediaan. Kaalu mediaani veerule määra nimeks `"kaalu mediaan"`. Omista saadud tabel muutujale `tabel3`, prindi see eraanile.
- **Ülesanne 2** Omista muutujale `rott2mediaan` roti `no.02` kaalu mediaani väärtus. 


*** =hint
- Käsus `dcast` käsus saad arvutatavale veerule nime panemiseks käsu argumendi `formula` kirja panna nii `reatunus1 + reatunnus2 ~ "uustunnus"`.


*** =pre_exercise_code
```{r}
# nlme paketist
library(nlme)
library(stringr)
rotid <- as.data.frame(BodyWeight)
rotid$Rat <- paste0("no", str_pad(rotid$Rat, width = 2, "left", pad = "0"))
rotid$Time <- paste0("day", str_pad(rotid$Time, width = 2, "left", pad = "0"))
indeks <- c(25:33, 76:77, 160:165)
rotid <- rotid[-indeks,]
rm(indeks)

library(reshape2)

```

*** =sample_code
```{r}
# vaata andmestikku
summary(rotid)

# Ülesanne 1: Leia mediaanide tabel dcast käsuga
tabel3 <- ________________
tabel3


# Ülesanne 2: roti nr 2 kaalu mediaan
rott2mediaan <- _______

```



*** =solution
```{r}
# vaata andmestikku
summary(rotid)

# Ülesanne 1: Leia mediaanide tabel dcast käsuga
tabel3 <- dcast(rotid, Diet + Rat ~ "kaalu mediaan", fun.aggregate = median, value.var = "weight")
tabel3


# Ülesanne 2: roti nr 2 kaalu mediaan
rott2mediaan <- 240

```



*** =sct
```{r}

#1
test_function(name = "dcast", 
              args = c("data", "formula", "fun.aggregate", "value.var"),
              index = 1,
              eq_condition = "equal",
              not_called_msg = "Esimeses ülesandes pead kasutama funktsiooni `dcast`.",
              args_not_specified_msg = paste("Käsku `dcast` läheb " , 
                                             c("esimeseks argumendiks andmestiku nimi",
                                               " üheks argumendiks  `formula`, valem, mille kaudu saab määrata rea ja veertunnused.",
                                               " üheks argumendiks  `fun.aggregate`, selle kaudu saab määrata funktsiooni, mille tulemus lahtrites esitada.",
                                               " seekord vaja ka argumenti `value.var`.")),
              incorrect_msg =   paste("Käsus `dcast` on  ", 
                                      c("vale andmestik",
                                        "`formula` argumendi väärtus vale. Tabelis võiks reas esimene väärtus olla dieedi number, teine roti number ja kolmas leitud mediaan veerus `kaalu mediaan`", 
                                        "`fun.aggregate` argumendi väärtus vale.", 
                                        " argumendi `value.var` väärtus vale. Mis tunnuse mediaani on vaja leida?"
                                        )))



test_data_frame("tabel3", columns = "kaalu mediaan",
            undefined_msg = "Andmetabel `tabel3` on defineerimata.",
            undefined_cols_msg = "Andmestikus `tabel3` pole veergu nimega `kaalu mediaan`.",
            incorrect_msg = "Andmetabeli `tabel3  veeru `kaalu mediaan` väärtus ei ole korrektne. Proovi uuesti." )


test_output_contains("tabel3", incorrect_msg = "`dcast` funtksiooni tulemus `tabel3` on ekraanile printimata.")




#3
test_object("rott2mediaan", 
            undefined_msg = "Muutuja `rott2mediaan` on defineerimata.",
            incorrect_msg = "Muutuja `rott2mediaan` väärtus ei ole korrektne. Proovi uuesti." )



success_msg("Hästi! Siin ülesandes pidi `dcast` funktsioonis argumentide `fun.aggregate` ja `value.var` väärtused määrama, sest vaikimisi väärtused ei sobinud.")


```




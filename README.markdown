---
author:
- Abdelhedi Youssef
title: Projet Analyse de Données
---

Pour Commencer, après avoir téléchargé nos données sous format csv
depuis Google Forms, nous devons les charger :

::: snugshade
::: Highlighting
questionnaire [\<-]{style="color: 0.56,0.35,0.01"}
[**read.csv**]{style="color: 0.13,0.29,0.53"}([\"D:/A
garder/maths/M1/Analyse de
données/Formulaire.csv\"]{style="color: 0.31,0.60,0.02"})
:::
:::

$\underline{\textbf{Premier ACP}}$

**Traitement des Données**

Pour cela, nous devons simplement extraire le premier bloc (toutes les
questions qui commencent par "Qu'est-ce qui influence votre envie de
répondre à des questionnaires") :

::: snugshade
::: Highlighting
colonnes [\<-]{style="color: 0.56,0.35,0.01"}
[**grep**]{style="color: 0.13,0.29,0.53"}(
[\"\^Qu]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.est]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.ce]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.qui]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.influence]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.votre]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.envie]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.de]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.répondre]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.à]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.des]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.questionnaires]{style="color: 0.31,0.60,0.02"}[**\\\\**]{style="color: 0.81,0.36,0.00"}[.\"]{style="color: 0.31,0.60,0.02"},
[**colnames**]{style="color: 0.13,0.29,0.53"}(questionnaire), [value
=]{style="color: 0.13,0.29,0.53"} [TRUE]{style="color: 0.56,0.35,0.01"})
:::
:::

Et ensuite changer les valeurs pour qu'elles correspondent à l'échelle
de Likert :

::: snugshade
::: Highlighting
questionnaire [\<-]{style="color: 0.56,0.35,0.01"} questionnaire
[**%\>%**]{style="color: 0.81,0.36,0.00"}
[**mutate**]{style="color: 0.13,0.29,0.53"}([**across**]{style="color: 0.13,0.29,0.53"}([**all_of**]{style="color: 0.13,0.29,0.53"}(colonnes),
[**\~**]{style="color: 0.81,0.36,0.00"}[**replace**]{style="color: 0.13,0.29,0.53"}(.,
. [**==**]{style="color: 0.81,0.36,0.00"} [\"Pas du tout
daccord\"]{style="color: 0.31,0.60,0.02"},
[1]{style="color: 0.00,0.00,0.81"})))
[**%\>%**]{style="color: 0.81,0.36,0.00"}
[**mutate**]{style="color: 0.13,0.29,0.53"}([**across**]{style="color: 0.13,0.29,0.53"}([**all_of**]{style="color: 0.13,0.29,0.53"}(colonnes),
[**\~**]{style="color: 0.81,0.36,0.00"}[**replace**]{style="color: 0.13,0.29,0.53"}(.,
. [**==**]{style="color: 0.81,0.36,0.00"} [\"Pas
daccord\"]{style="color: 0.31,0.60,0.02"},
[2]{style="color: 0.00,0.00,0.81"})))
[**%\>%**]{style="color: 0.81,0.36,0.00"}
[**mutate**]{style="color: 0.13,0.29,0.53"}([**across**]{style="color: 0.13,0.29,0.53"}([**all_of**]{style="color: 0.13,0.29,0.53"}(colonnes),
[**\~**]{style="color: 0.81,0.36,0.00"}[**replace**]{style="color: 0.13,0.29,0.53"}(.,
. [**==**]{style="color: 0.81,0.36,0.00"}
[\"Neutre\"]{style="color: 0.31,0.60,0.02"},
[3]{style="color: 0.00,0.00,0.81"})))
[**%\>%**]{style="color: 0.81,0.36,0.00"}
[**mutate**]{style="color: 0.13,0.29,0.53"}([**across**]{style="color: 0.13,0.29,0.53"}([**all_of**]{style="color: 0.13,0.29,0.53"}(colonnes),
[**\~**]{style="color: 0.81,0.36,0.00"}[**replace**]{style="color: 0.13,0.29,0.53"}(.,
. [**==**]{style="color: 0.81,0.36,0.00"} [\"Plutôt
Daccord\"]{style="color: 0.31,0.60,0.02"},
[4]{style="color: 0.00,0.00,0.81"})))
[**%\>%**]{style="color: 0.81,0.36,0.00"}
[**mutate**]{style="color: 0.13,0.29,0.53"}([**across**]{style="color: 0.13,0.29,0.53"}([**all_of**]{style="color: 0.13,0.29,0.53"}(colonnes),
[**\~**]{style="color: 0.81,0.36,0.00"}[**replace**]{style="color: 0.13,0.29,0.53"}(.,
. [**==**]{style="color: 0.81,0.36,0.00"} [\"Tout à fait
Daccord\"]{style="color: 0.31,0.60,0.02"},
[5]{style="color: 0.00,0.00,0.81"})))
:::
:::

Enfin changer le nom des colonnes pour qu'elles soient plus lisibles :

::: snugshade
::: Highlighting
data_selectionnee [\<-]{style="color: 0.56,0.35,0.01"}
questionnaire\[colonnes\] nouveaux_noms
[\<-]{style="color: 0.56,0.35,0.01"}
[**c**]{style="color: 0.13,0.29,0.53"}( [\"Clarté des
Questions\"]{style="color: 0.31,0.60,0.02"}, [\"La
Longueur\"]{style="color: 0.31,0.60,0.02"}, [\"Le
créateur\"]{style="color: 0.31,0.60,0.02"},
[\"Lheure\"]{style="color: 0.31,0.60,0.02"}, [\"Le
sujet\"]{style="color: 0.31,0.60,0.02"},[\"Lobjectif\"]{style="color: 0.31,0.60,0.02"},[\"Lorganisation\"]{style="color: 0.31,0.60,0.02"},[\"La
langue\"]{style="color: 0.31,0.60,0.02"},[\"La Methode de
Partage\"]{style="color: 0.31,0.60,0.02"}, [\"La
récompense\"]{style="color: 0.31,0.60,0.02"},[\"Qualité des
Qst\"]{style="color: 0.31,0.60,0.02"},[\"Lemetteur\"]{style="color: 0.31,0.60,0.02"},[\"Le
temps\"]{style="color: 0.31,0.60,0.02"},[\"Lhumeur\"]{style="color: 0.31,0.60,0.02"},[\"Reseau
Social\"]{style="color: 0.31,0.60,0.02"})
[**colnames**]{style="color: 0.13,0.29,0.53"}(data_selectionnee)
[\<-]{style="color: 0.56,0.35,0.01"} nouveaux_noms
:::
:::

Commençons par comprendre la data que nous avons maintenant :

::: snugshade
::: Highlighting
[**summary**]{style="color: 0.13,0.29,0.53"}(data_selectionnee)
:::
:::

    ##  Clarté des Questions La Longueur        Le créateur          L'heure         
    ##  Length:40            Length:40          Length:40          Length:40         
    ##  Class :character     Class :character   Class :character   Class :character  
    ##  Mode  :character     Mode  :character   Mode  :character   Mode  :character  
    ##    Le sujet          L'objectif        L'organisation      La langue        
    ##  Length:40          Length:40          Length:40          Length:40         
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##  La Methode de Partage La récompense      Qualité des Qst     L'emetteur       
    ##  Length:40             Length:40          Length:40          Length:40         
    ##  Class :character      Class :character   Class :character   Class :character  
    ##  Mode  :character      Mode  :character   Mode  :character   Mode  :character  
    ##    Le temps           L'humeur         Reseau Social     
    ##  Length:40          Length:40          Length:40         
    ##  Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character

Nous remarquons donc qu'il faut que nous rendions toutes les valeurs
numériques

::: snugshade
::: Highlighting
data_selectionnee [\<-]{style="color: 0.56,0.35,0.01"}
[**apply**]{style="color: 0.13,0.29,0.53"}(data_selectionnee,
[2]{style="color: 0.00,0.00,0.81"},
[**function**]{style="color: 0.13,0.29,0.53"}(x)
[**as.numeric**]{style="color: 0.13,0.29,0.53"}([**as.character**]{style="color: 0.13,0.29,0.53"}(x)))
:::
:::

**Analyse des Données**

Voyons ce que nous propose la matrice de corrélation :

::: snugshade
::: Highlighting
matrice_correlation [\<-]{style="color: 0.56,0.35,0.01"}
[**cor**]{style="color: 0.13,0.29,0.53"}(data_selectionnee)
[**corrplot**]{style="color: 0.13,0.29,0.53"}(matrice_correlation,
[method =]{style="color: 0.13,0.29,0.53"}
[\"circle\"]{style="color: 0.31,0.60,0.02"}, [type
=]{style="color: 0.13,0.29,0.53"}
[\"upper\"]{style="color: 0.31,0.60,0.02"}, [tl.col
=]{style="color: 0.13,0.29,0.53"}
[\"black\"]{style="color: 0.31,0.60,0.02"}, [tl.srt
=]{style="color: 0.13,0.29,0.53"} [45]{style="color: 0.00,0.00,0.81"})
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-8-1){height="0.3\\textheight"}
:::

Nous pouvons voir notamment que la variable "créateur du formulaire" est
très liée à la variable "émetteur" à environ 80% ainsi qu'à la "méthode
de partage" à 55%

Nous pouvons aussi remarquer que les variables "Sujet","Objectif" et
"Organisation" sont corrélées à hauteur d'environ 50% Maintenant
effectuons l'ACP :

::: snugshade
::: Highlighting
acp_result [\<-]{style="color: 0.56,0.35,0.01"}
[**PCA**]{style="color: 0.13,0.29,0.53"}(data_selectionnee, [graph
=]{style="color: 0.13,0.29,0.53"}
[FALSE]{style="color: 0.56,0.35,0.01"})
[**fviz_eig**]{style="color: 0.13,0.29,0.53"}(acp_result, [addlabels
=]{style="color: 0.13,0.29,0.53"} [TRUE]{style="color: 0.56,0.35,0.01"},
[ylim =]{style="color: 0.13,0.29,0.53"}
[**c**]{style="color: 0.13,0.29,0.53"}([0]{style="color: 0.00,0.00,0.81"},
[40]{style="color: 0.00,0.00,0.81"}))
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-9-1){height="0.35\\textheight"}
:::

Ici nous pouvons choisir de garder 2 ou 3 axes. En effet, ils ont tous
des Valeurs Propres supérieures à 1 (critère de Kaiser). Le coude se
trouve au niveau du 3ème axe et l'inertie cumulée est autour des 50%
malgré le fait qu'il y ait 15 variables. Choisissons-en 2.

**Interpretation**

::: snugshade
:::

    ##                             Dim.1       Dim.2
    ## Clarté des Questions   0.56383704 -0.45299770
    ## La Longueur            0.10965769 -0.04924791
    ## Le créateur           -0.17012742  0.84340094
    ## L'heure                0.33224758  0.48130477
    ## Le sujet               0.78898775  0.05010600
    ## L'objectif             0.79027269  0.12698524
    ## L'organisation         0.76468307 -0.22213604
    ## La langue             -0.03800761  0.38723987
    ## La Methode de Partage  0.16475089  0.76464913
    ## La récompense         -0.16745352  0.36824138
    ## Qualité des Qst        0.66854851 -0.13288838
    ## L'emetteur            -0.09317590  0.87535397
    ## Le temps               0.53690219  0.46306713
    ## L'humeur               0.62670619  0.24286429
    ## Reseau Social          0.03506089 -0.16112179

Nous pouvons ici voir que la première dimension est en rapport avec "Le
sujet", "L'objectif", "L'organisation", "La récompense", "Qualité des
Qst" et "L'humeur". Nous pouvons donc l'appeler Fond et Timing. La
seconde est en rapport avec "Le créateur", "La Methode de Partage" et
"L'emetteur". Nous pouvons donc l'appeler La conception. Nous Pouvons
remarquer ces mêmes informations dans le graphique ci-dessous :

::: snugshade
::: Highlighting
[**fviz_pca_var**]{style="color: 0.13,0.29,0.53"}(acp_result,
[col.var=]{style="color: 0.13,0.29,0.53"}[\"cos2\"]{style="color: 0.31,0.60,0.02"})
[**+**]{style="color: 0.81,0.36,0.00"}
[**scale_color_gradient2**]{style="color: 0.13,0.29,0.53"}([low=]{style="color: 0.13,0.29,0.53"}[\"white\"]{style="color: 0.31,0.60,0.02"},
[mid=]{style="color: 0.13,0.29,0.53"}[\"blue\"]{style="color: 0.31,0.60,0.02"},
[high=]{style="color: 0.13,0.29,0.53"}[\"red\"]{style="color: 0.31,0.60,0.02"},
[midpoint=]{style="color: 0.13,0.29,0.53"}[0.6]{style="color: 0.00,0.00,0.81"})
[**+**]{style="color: 0.81,0.36,0.00"}
[**theme_minimal**]{style="color: 0.13,0.29,0.53"}()
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-11-1){height="0.3\\textheight"}
:::

Maintenant, Essayons de comprendre les individus :

::: snugshade
::: Highlighting
[**fviz_pca_ind**]{style="color: 0.13,0.29,0.53"}(acp_result, [col.ind
=]{style="color: 0.13,0.29,0.53"}
[\"cos2\"]{style="color: 0.31,0.60,0.02"}, [gradient.cols
=]{style="color: 0.13,0.29,0.53"}
[**c**]{style="color: 0.13,0.29,0.53"}([\"#00AFBB\"]{style="color: 0.31,0.60,0.02"},
[\"#E7B800\"]{style="color: 0.31,0.60,0.02"},
[\"#FC4E07\"]{style="color: 0.31,0.60,0.02"}), [repel
=]{style="color: 0.13,0.29,0.53"} [TRUE]{style="color: 0.56,0.35,0.01"}
)
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-12-1){height="0.3\\textheight"}
:::

Nous Pouvons remarquer qu'il y a un groupe de personnes qui donne peu
d'importance à la Conception et encore moins au fond et au Timing, Ils
sont donc désintéressés de l'action même de remplir un formulaire. Et
plus on s'éloigne, moins il y a d'individus, leur repartition suit
certainement une loi normale..

$\underline{\textbf{Second ACP}}$

**Traitement des Données**

Pour cela, nous devons simplement extraire le second bloc (de la colonne
21 à 35)

::: snugshade
::: Highlighting
data_selectionnee [\<-]{style="color: 0.56,0.35,0.01"} questionnaire\[,
[21]{style="color: 0.00,0.00,0.81"}[**:**]{style="color: 0.81,0.36,0.00"}[35]{style="color: 0.00,0.00,0.81"}\]
nouveaux_noms [\<-]{style="color: 0.56,0.35,0.01"}
[**c**]{style="color: 0.13,0.29,0.53"}(
[\"Vehicules\"]{style="color: 0.31,0.60,0.02"},
[\"Technologies\"]{style="color: 0.31,0.60,0.02"},
[\"Social\"]{style="color: 0.31,0.60,0.02"},
[\"Sport\"]{style="color: 0.31,0.60,0.02"},[\"Etudes\"]{style="color: 0.31,0.60,0.02"},[\"Clubs\"]{style="color: 0.31,0.60,0.02"},[\"Sciences\"]{style="color: 0.31,0.60,0.02"},
[\"Cosmetiques\"]{style="color: 0.31,0.60,0.02"},[\"Economie\"]{style="color: 0.31,0.60,0.02"},[\"Jeux
Videos\"]{style="color: 0.31,0.60,0.02"},[\"Mode\"]{style="color: 0.31,0.60,0.02"},[\"RnD\"]{style="color: 0.31,0.60,0.02"},[\"Politique\"]{style="color: 0.31,0.60,0.02"},[\"Musique\"]{style="color: 0.31,0.60,0.02"},[\"Orientation\"]{style="color: 0.31,0.60,0.02"})
[**colnames**]{style="color: 0.13,0.29,0.53"}(data_selectionnee)
[\<-]{style="color: 0.56,0.35,0.01"} nouveaux_noms
[**summary**]{style="color: 0.13,0.29,0.53"}(data_selectionnee)
:::
:::

    ##    Vehicules      Technologies      Social          Sport          Etudes    
    ##  Min.   :1.000   Min.   :1.00   Min.   :1.000   Min.   :1.00   Min.   :1.00  
    ##  1st Qu.:1.750   1st Qu.:3.00   1st Qu.:3.750   1st Qu.:3.00   1st Qu.:3.00  
    ##  Median :3.000   Median :4.00   Median :4.500   Median :4.00   Median :4.00  
    ##  Mean   :2.875   Mean   :4.05   Mean   :4.125   Mean   :3.55   Mean   :3.85  
    ##  3rd Qu.:4.000   3rd Qu.:5.00   3rd Qu.:5.000   3rd Qu.:4.00   3rd Qu.:5.00  
    ##  Max.   :5.000   Max.   :5.00   Max.   :5.000   Max.   :5.00   Max.   :5.00  
    ##      Clubs         Sciences      Cosmetiques       Economie      Jeux Videos 
    ##  Min.   :1.00   Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.0  
    ##  1st Qu.:2.00   1st Qu.:4.000   1st Qu.:1.000   1st Qu.:2.000   1st Qu.:2.0  
    ##  Median :3.00   Median :4.000   Median :2.000   Median :3.000   Median :3.0  
    ##  Mean   :3.25   Mean   :4.025   Mean   :2.375   Mean   :3.025   Mean   :2.9  
    ##  3rd Qu.:4.25   3rd Qu.:5.000   3rd Qu.:3.250   3rd Qu.:4.000   3rd Qu.:4.0  
    ##  Max.   :5.00   Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.0  
    ##       Mode            RnD          Politique        Musique       Orientation 
    ##  Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.000   Min.   :1.0  
    ##  1st Qu.:2.000   1st Qu.:3.000   1st Qu.:2.000   1st Qu.:3.000   1st Qu.:2.0  
    ##  Median :3.000   Median :4.000   Median :3.000   Median :4.000   Median :3.0  
    ##  Mean   :3.075   Mean   :3.725   Mean   :2.875   Mean   :3.975   Mean   :3.2  
    ##  3rd Qu.:4.000   3rd Qu.:5.000   3rd Qu.:4.000   3rd Qu.:5.000   3rd Qu.:4.0  
    ##  Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.000   Max.   :5.0

**Analyse des Données**

Voyons ce que nous propose la matrice de corrélation :

::: snugshade
::: Highlighting
matrice_correlation [\<-]{style="color: 0.56,0.35,0.01"}
[**cor**]{style="color: 0.13,0.29,0.53"}(data_selectionnee)
[**corrplot**]{style="color: 0.13,0.29,0.53"}(matrice_correlation,
[method =]{style="color: 0.13,0.29,0.53"}
[\"circle\"]{style="color: 0.31,0.60,0.02"}, [type
=]{style="color: 0.13,0.29,0.53"}
[\"upper\"]{style="color: 0.31,0.60,0.02"}, [tl.col
=]{style="color: 0.13,0.29,0.53"}
[\"black\"]{style="color: 0.31,0.60,0.02"}, [tl.srt
=]{style="color: 0.13,0.29,0.53"} [45]{style="color: 0.00,0.00,0.81"})
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-14-1){height="0.25\\textheight"}
:::

Maintenant effectuons l'ACP :

::: snugshade
::: Highlighting
acp_result [\<-]{style="color: 0.56,0.35,0.01"}
[**PCA**]{style="color: 0.13,0.29,0.53"}(data_selectionnee, [graph
=]{style="color: 0.13,0.29,0.53"}
[FALSE]{style="color: 0.56,0.35,0.01"})
[**fviz_eig**]{style="color: 0.13,0.29,0.53"}(acp_result, [addlabels
=]{style="color: 0.13,0.29,0.53"} [TRUE]{style="color: 0.56,0.35,0.01"},
[ylim =]{style="color: 0.13,0.29,0.53"}
[**c**]{style="color: 0.13,0.29,0.53"}([0]{style="color: 0.00,0.00,0.81"},
[40]{style="color: 0.00,0.00,0.81"}))
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-15-1){height="0.35\\textheight"}
:::

Ici nous pouvons choisir de garder 2. En effet, ils ont tous des Valeurs
Propres supérieures à 1 (critère de Kaiser). Le coude se trouve au
niveau du 2ème axe et l'inertie cumulée est autour des 47% malgré le
fait qu'il y ait 15 variables.

**Interpretation**

::: snugshade
:::

    ##                    Dim.1      Dim.2
    ## Vehicules     0.04670966  0.6034721
    ## Technologies  0.53697435  0.6290448
    ## Social        0.64294174 -0.3004132
    ## Sport         0.47159414  0.1746898
    ## Etudes        0.67138709 -0.0761582
    ## Clubs         0.76274493 -0.2454059
    ## Sciences      0.65615110  0.2766407
    ## Cosmetiques   0.66060207 -0.4093864
    ## Economie      0.56114097 -0.2530836
    ## Jeux Videos  -0.06014481  0.7296112
    ## Mode          0.41773924 -0.2913497
    ## RnD           0.72199663  0.2886653
    ## Politique     0.45871405  0.1118671
    ## Musique       0.50997039  0.4182240
    ## Orientation   0.71555008 -0.1304903

Nous pouvons ici voir que la première dimension est en rapport avec
"Etudes", "Clubs", "Sciences", "Cosmetiques", "Economie", "RnD" et
"Orientation". Nous pouvons donc l'appeler Culture. La seconde est en
rapport avec "Vehicules","Technologies" et "Jeux Videos". Nous pouvons
donc l'appeler "Divertissements Technologiques". Nous Pouvons remarquer
ces mêmes informations dans le graphique ci-dessous :

::: snugshade
::: Highlighting
[**fviz_pca_var**]{style="color: 0.13,0.29,0.53"}(acp_result,
[col.var=]{style="color: 0.13,0.29,0.53"}[\"cos2\"]{style="color: 0.31,0.60,0.02"})
[**+**]{style="color: 0.81,0.36,0.00"}
[**scale_color_gradient2**]{style="color: 0.13,0.29,0.53"}([low=]{style="color: 0.13,0.29,0.53"}[\"white\"]{style="color: 0.31,0.60,0.02"},
[mid=]{style="color: 0.13,0.29,0.53"}[\"blue\"]{style="color: 0.31,0.60,0.02"},
[high=]{style="color: 0.13,0.29,0.53"}[\"red\"]{style="color: 0.31,0.60,0.02"},
[midpoint=]{style="color: 0.13,0.29,0.53"}[0.6]{style="color: 0.00,0.00,0.81"})
[**+**]{style="color: 0.81,0.36,0.00"}
[**theme_minimal**]{style="color: 0.13,0.29,0.53"}()
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-17-1){height="0.3\\textheight"}
:::

Maintenant, Essayons de comprendre les individus :

::: snugshade
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-18-1){height="0.3\\textheight"}
:::

Nous pouvons remarquer qu'il y a un groupe de Personnes qui est plutot
intéressé par la culture et plutot neutre vis-à-vis du divertissement
technologique, tandis qu'un second a tendance à ne pas aimer la culture
mais plutot etre intéressé par le divertissement technologique. Enfin,
il y a ceux qui ne sont interessés par aucun des deux. Nous remarquons
que le premier groupe est essentiellement constitué de femmes, tandis
que le second d'hommes. $\underline{\textbf{ACM}}$

**Traitement des Données**

Commençons par extraire uniquement les colonnes dont nous avons besoin :

::: snugshade
::: Highlighting
colonnes_a\_retirer [\<-]{style="color: 0.56,0.35,0.01"}
[**c**]{style="color: 0.13,0.29,0.53"}(
[\"Combien.de.temps.au.maximum.vous.passez.à.répondre.à.un.questionnaire..\"]{style="color: 0.31,0.60,0.02"},
[\"Comment.choisissez.vous.les.questionnaires.auxquels.vous.décidez.de.répondre.\"]{style="color: 0.31,0.60,0.02"},
[\"Quelles.informations.seriez.vous.réticents.à.fournir.dans.un.questionnaire..même.de.manière.anonyme.\"]{style="color: 0.31,0.60,0.02"}
) questionnaire [\<-]{style="color: 0.56,0.35,0.01"} questionnaire\[,
[**!**]{style="color: 0.81,0.36,0.00"}[**names**]{style="color: 0.13,0.29,0.53"}(questionnaire)
[**%in%**]{style="color: 0.81,0.36,0.00"} colonnes_a\_retirer\] colonnes
[\<-]{style="color: 0.56,0.35,0.01"}
[**cbind**]{style="color: 0.13,0.29,0.53"}(questionnaire\[,
[36]{style="color: 0.00,0.00,0.81"}[**:**]{style="color: 0.81,0.36,0.00"}[**ncol**]{style="color: 0.13,0.29,0.53"}(questionnaire)\],
questionnaire\[,
[**c**]{style="color: 0.13,0.29,0.53"}([2]{style="color: 0.00,0.00,0.81"},
[3]{style="color: 0.00,0.00,0.81"},
[4]{style="color: 0.00,0.00,0.81"})\])
:::
:::

Ensuite, pour que ce soit plus lisible, nous allons changer le nom des
colonnes :

::: snugshade
::: Highlighting
nouveaux_noms[\<-]{style="color: 0.56,0.35,0.01"}[**c**]{style="color: 0.13,0.29,0.53"}(
[\"abandon_longueur\"]{style="color: 0.31,0.60,0.02"},[\"type_questionnaire\"]{style="color: 0.31,0.60,0.02"},[\"fausses_informations\"]{style="color: 0.31,0.60,0.02"},
[\"anonymat\"]{style="color: 0.31,0.60,0.02"},[\"creation\"]{style="color: 0.31,0.60,0.02"},[\"importance_opinion\"]{style="color: 0.31,0.60,0.02"},[\"sondage\"]{style="color: 0.31,0.60,0.02"},[\"reflexion\"]{style="color: 0.31,0.60,0.02"},[\"humeur\"]{style="color: 0.31,0.60,0.02"},
[\"createur\"]{style="color: 0.31,0.60,0.02"},[\"type_question\"]{style="color: 0.31,0.60,0.02"},[\"longueur\"]{style="color: 0.31,0.60,0.02"},[\"sexe\"]{style="color: 0.31,0.60,0.02"},[\"age\"]{style="color: 0.31,0.60,0.02"},[\"SSP\"]{style="color: 0.31,0.60,0.02"}
) [**colnames**]{style="color: 0.13,0.29,0.53"}(colonnes)
[\<-]{style="color: 0.56,0.35,0.01"} nouveaux_noms
:::
:::

**Analyse des Données**

Une fois cela a été éffectué, réalisons une ACM sur les preferences des
individus :

::: snugshade
::: Highlighting
res.MCA [\<-]{style="color: 0.56,0.35,0.01"}
[**MCA**]{style="color: 0.13,0.29,0.53"}(colonnes, [quanti.sup
=]{style="color: 0.13,0.29,0.53"}
[**c**]{style="color: 0.13,0.29,0.53"}([12]{style="color: 0.00,0.00,0.81"}),
[graph =]{style="color: 0.13,0.29,0.53"}
[FALSE]{style="color: 0.56,0.35,0.01"})
[**fviz_eig**]{style="color: 0.13,0.29,0.53"}(res.MCA, [addlabels
=]{style="color: 0.13,0.29,0.53"} [TRUE]{style="color: 0.56,0.35,0.01"},
[ylim =]{style="color: 0.13,0.29,0.53"}
[**c**]{style="color: 0.13,0.29,0.53"}([0]{style="color: 0.00,0.00,0.81"},
[40]{style="color: 0.00,0.00,0.81"}))
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-21-1){height="0.3\\textheight"}
:::

Nous Remarquons donc que le coude est au bout de la 2ème dimension et
que l'inertie cumulée est d'environ 30% malgré la présence de 12
variables (ce qui reste quand même faible) **Interpretation**

Voyons ce que chacune des 2 premières dimensions représente :

::: snugshade
::: Highlighting
[**plot.MCA**]{style="color: 0.13,0.29,0.53"}(res.MCA,
[choix=]{style="color: 0.13,0.29,0.53"}[var]{style="color: 0.31,0.60,0.02"},[invisible=]{style="color: 0.13,0.29,0.53"}[quanti.sup]{style="color: 0.31,0.60,0.02"},[title=]{style="color: 0.13,0.29,0.53"}[\"Graphe
des variables\"]{style="color: 0.31,0.60,0.02"})
:::
:::

::: center
![image](Projet_files/figure-latex/unnamed-chunk-22-1){height="0.45\\textheight"}
:::

Nous pouvons voir que la première dimension est influencée par les
préférences du type de questionnaires (en ligne ou papier) mais aussi
par la préférence de longueur du questionnaire. Quant à la deuxième
dimension elle est influencée par la catégorie d'age et la situation
socio-professionnelle de l'individu

::: snugshade
::: Highlighting
[**plot.MCA**]{style="color: 0.13,0.29,0.53"}(res.MCA,[invisible=]{style="color: 0.13,0.29,0.53"}
[var]{style="color: 0.31,0.60,0.02"},[habillage=]{style="color: 0.13,0.29,0.53"}[cos2]{style="color: 0.31,0.60,0.02"},[title=]{style="color: 0.13,0.29,0.53"}[\"Graphe
de lACM\"]{style="color: 0.31,0.60,0.02"},[label
=]{style="color: 0.13,0.29,0.53"}[**c**]{style="color: 0.13,0.29,0.53"}([ind]{style="color: 0.31,0.60,0.02"}))
:::
:::

    ## Warning: ggrepel: 18 unlabeled data points (too many overlaps). Consider
    ## increasing max.overlaps

::: center
![image](Projet_files/figure-latex/unnamed-chunk-23-1){height="0.3\\textheight"}
:::

Nous Pouvons remarquer que la plupart des individus se concentrent au
centre du graphique avec un faible cos2 (donc la représentation n'est
pas très effective), et que les individus qui sont plus loin du centre
sont mieux représentés

::: snugshade
::: Highlighting
[**plot.MCA**]{style="color: 0.13,0.29,0.53"}(res.MCA,[invisible=]{style="color: 0.13,0.29,0.53"}
[ind]{style="color: 0.31,0.60,0.02"},[habillage=]{style="color: 0.13,0.29,0.53"}[cos2]{style="color: 0.31,0.60,0.02"},[title=]{style="color: 0.13,0.29,0.53"}[\"Graphe
de lACM\"]{style="color: 0.31,0.60,0.02"},[label
=]{style="color: 0.13,0.29,0.53"}[**c**]{style="color: 0.13,0.29,0.53"}([var]{style="color: 0.31,0.60,0.02"}))
:::
:::

    ## Warning: ggrepel: 20 unlabeled data points (too many overlaps). Consider
    ## increasing max.overlaps

::: center
![image](Projet_files/figure-latex/unnamed-chunk-24-1){height="0.3\\textheight"}
:::

Nous Pouvons donc voir que les individus 38 et 39 ont en commun le fait
d'être employés et qu'ils sont dans la tranche d'age 40-60 et que
l'individu 32 préfère les questionnaires papiers et qu'il a en commun
avec l'individu 22 et 21 les réponses courtes et l'abandon des
questionnaires longs

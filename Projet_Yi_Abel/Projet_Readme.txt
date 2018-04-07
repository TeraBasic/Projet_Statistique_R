﻿---
title: "Analyse de la résistance à la compression du béton"
author: "LI Yi, Muwala Abel"
date: "03/04/2018"
output:
  pdf_document:
    toc: yes
    toc_depth: '3'
  md_document:
    toc: yes
    toc_depth: 3
  html_document:
    toc: yes
    toc_depth: 3
---


```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
##1 Introduction
###1.1 Problématiques
Résumé: Le béton est le matériau le plus important en génie civil. la résistance à la compression du béton est une fonction hautement non linéaire de l'âge et de ces composents.Notamment le ciment, le laitier de haut fourneau, les cendres volantes,l'eau, le superplastifiant, l'agrégat grossier et l'agrégat fin.

Question :
 Y'a-t-il une relation entre "Concrete compressive strength" et les autres attributs ? ou simplement y'a t-il une relation entre un attribut (Input variable) et Concrete compressive strength.
  
 Y'a t-il un attribut qui détermine la résistance du béton à la compression?

Sujet : Concrete Compressive Strength (la résistance à la compression du béton)

###1.2 Données

####1.2.1 Contexte
La résistance réelle à la compression du béton (MPa) pour un mélange donné a été déterminé à partir du laboratoire en fonction de son âge spécifique (jours). Les données sont sous forme brute (non échelonnées).

Statistiques récapitulatives:
Nombre de cas (observations): 1030
Nombre d'attributs: 9
Répartition des attributs: 8 variables d'entrée quantitatives et 1 variable de sortie quantitative
Valeurs d'attribut manquantes: Aucune

####1.2.2 Description des  données 
Nombre de cas (observations): 1030
Nombre d'attributs: 9
Répartition des attributs: 8 variables d'entrée quantitatives et 1 variable de sortie quantitative
Valeurs d'attribut manquantes: Aucune

On donne pour chaque variable le nom, le type, l'unité de mesure et une brève description. La résistance à la compression du béton est le problème de la régression. L'ordre des variables correspond à l'ordre des chiffres le long des lignes de la base de données. 

Pour des questions de simplicicté dans notre traitement , nous allons utiliser d'autres variables à la place des attributs :
A1 pour "Cement";
A2 pour "Blast Furnace Slag";
A3 pour "Fly Ash";
A4 pour "Water";
A5 pour "Superplasticizer ";
A6 pour "Coarse Aggregate";
A7 pour "Fine Aggregate";
A8 pour "Age";
A9 pour "Concrete compressive strength".

####1.2.3 Sources: 

  Original Owner and Donor
  Prof. I-Cheng Yeh
  Department of Information Management 
  Chung-Hua University, 
  Hsin Chu, Taiwan 30067, R.O.C.
  e-mail:icyeh@chu.edu.tw
  TEL:886-3-5186511

  Date Donated: August 3, 2007
  
###1.3 Méthodologie

 Méthode d'analyse et les visualisations
	- statistic simple et description des données.
	- visualisation des données en utilisant les graphiques et les diagrammes qu'on a vue dans les cours.
	- regression linéaire : qualité = a x Cement + b x Blast Furnace Slag + c x Fly Ash ...

'library' utiles pour notre analyse: 
  - ggplot2
  - xlsx
  - car

##2 Summary et visualisation des données
###2.1 Les packages que nous utilisons
Nous utilisons le package ggplot2 pour la visulisation des données, le package xlsx pour le lecture des données.
```{r}
# package
library(ggplot2)
library(xlsx)
```

###2.2 Lecture et Summary des donnée
Nous utilisons la fonction read.xlsx() pour lire les données dans le fichier "Concrete_Data.xls".
On affiche les six première lignes.
```{r}
df <- read.xlsx("Concrete_Data.xls",1)
str(df);
head(df);
```


Nous utilisons la fonctions summary pour afficher certains caractéristiques des données, par exemple: Le nombre minimal, le nombre maximaume, Médiane etc.
```{r}
myvars <- c("A1","A2","A3","A4","A5","A6","A7","A8","A9")
summary(df[myvars])
```
###2.3 La visualisation des données
Nous utilisons la boîte à moustaches pour résumer quelques caractéristiques de position du caractère étudié (médiane, quartiles, minimum, maximum ou déciles).
```{r}
attach(df)
opar <- par(no.readonly=TRUE)
par(mfrow=c(2,4))
boxplot(df["A1"])
boxplot(df["A2"])
boxplot(df["A3"])
boxplot(df["A4"])
boxplot(df["A5"])
boxplot(df["A6"])
boxplot(df["A7"])
boxplot(df["A8"])
par(opar)
detach(df)
```
Nous utilisons le nuage de points pour faire la représentation de données dépendant de plusieurs variables. Il nous permet de mettre en évidence le degré de corrélation entre A9 et les autres variables(A1,A2,A3...A8).
```{r}
library(ggplot2)
attach(df)
opar <- par(no.readonly=TRUE)
par(mfrow=c(2,4))

p1 <- ggplot(data=df, aes(x=A9, y=A1)) + geom_point() + labs(title="A1&A9", x="A9", y="A1")
p2 <- ggplot(data=df, aes(x=A9, y=A2)) + geom_point() + labs(title="A2&A9", x="A9", y="A2")
p3 <- ggplot(data=df, aes(x=A9, y=A3)) + geom_point() + labs(title="A3&A9", x="A9", y="A3")
p4 <- ggplot(data=df, aes(x=A9, y=A4)) + geom_point() + labs(title="A4&A9", x="A9", y="A4")
p5 <- ggplot(data=df, aes(x=A9, y=A5)) + geom_point() + labs(title="A5&A9", x="A9", y="A5")
p6 <- ggplot(data=df, aes(x=A9, y=A6)) + geom_point() + labs(title="A6&A9", x="A9", y="A6")
p7 <- ggplot(data=df, aes(x=A9, y=A7)) + geom_point() + labs(title="A7&A9", x="A9", y="A7")
p8 <- ggplot(data=df, aes(x=A9, y=A8)) + geom_point() + labs(title="A8&A9", x="A9", y="A8")
library(gridExtra)
grid.arrange(p1, p2, p3,p4,p5,p6,p7,p8, ncol=4)
detach(df)
```

##3 Les relations entre les variable 
###3.1 les relations
Avant de faire la régression linéaire, nous examinons les relations entre les variable. Nous utilisons la fonction cor() pour calculer les corrélation entre les variable. C'est étudier l'intensité de la liaison qui peut exister entre ces variables.
```{r}
vars <- df[,1:9]
vars <- as.matrix(sapply(vars, as.numeric)) 
cor(vars)
```
###3.2 La visualiation des relations
Nous utilisons la fonctions scatterplotMatrix () pour afficher les schemas qui representent les relations entre les variables. 
```{r}
library(car)
myvars1 <- c("A1","A2","A3","A4","A9")
myvars2 <- c("A5","A6","A7","A8","A9")
#summary(df[myvars])
vars1 <- df[myvars1]
vars2 <- df[myvars2]
scatterplotMatrix(vars1, spread=FALSE, smoother.args=list(lty=2),
main="Scatter Plot Matrix")
scatterplotMatrix(vars2, spread=FALSE, smoother.args=list(lty=2),
main="Scatter Plot Matrix")
```

##4 Régression linéaire multiple
###4.1 Toutes les variables
Nous utilisons toutes les variables pour faire la Régression linéaire
Variable dépendante(variable expliquée): A9
Variables indépendantes(variable explicative):A1,A2,A3,A4,A5,A6,A7,A8
```{r}
vars <- df[,1:9]
fit1 <- lm(A9 ~ A1+A2+A3+A4+A5+A6+A7+A8,data=vars)
summary(fit1)
```
###4.2 Les variables avec des relations fortes
Nous ne utilisons que les variables qui ont une relation relativement fortes avec la variable dépendante.(|cor|>0.2)
Variable dépendante(variable expliquée): A9
Variables indépendantes(variable explicative):A1,A4,A5,A8
```{r}
fit2 <- lm(A9 ~ A1+A4+A5+A8,data=vars)
summary(fit2)
```
###4.3 Les termes du second degré
Nous ajoutons les termes du second degré
```{r}
fit3 <- lm(A9 ~ A1+A4+A5+A8+I(A1^2)+I(A2^2)+I(A3^2)+I(A4^2),data=vars)
 summary(fit3)
```
###4.4 Explication de résultat de régression linéaire
On a réaliser 3 types de régression linéaire , chacun avec différents ensemble de variables.
On compare les résultats de ces analyses , notamment le ' Multiple R-squared' et la première régression linéaire a une plus grande valeur du ' Multiple R-squared'.
La première régression linéaire (avec tous les attibuts ) est donc la meilleure car plus proche de '1'.
Chaque fois que l'attribut A1 augmente de une unité , l'augmentation estimée de A9 est de '0.119785'.
C'est aussi le cas avec les autres attributs à l'exception de A4 ( l'eau).
L'augmentation de A4 de une unité diminue la résistance à la compression de '0.150298'
Ce résultat n'est obtenue quand ne considérant que l'augmentation estimée. 
Le fait de prendre en compte 'standard error' et 't value' et la distribution des échantillons ca donnerait un résultat différent et le processus d'analyse serait compliqué à notre niveau !

###4.5 Affichage dans les graphes
Nous choisissons deux variables indépendantes et les afficher dans les graphes
Avec les deux graphes ci-dessous on voit les tendances entre :
-la résistance à la compression du béton(A9) et le superplastifiant(A5).
-la résistance à la compression du béton(A9) et l'eau(A4).

```{r}
library(car)
scatterplot(A9 ~ A5, data=vars,
spread=FALSE, smoother.args=list(lty=2), pch=19,
main="A9-A5",
xlab="Superplastifiant",
ylab="Résistance à la compression du béton")

scatterplot(A9 ~ A1, data=vars,
spread=FALSE, smoother.args=list(lty=2), pch=19,
main="A9-A1",
xlab="Ciment",
ylab="Résistance à la compression du béton")

scatterplot(A9 ~ A4, data=vars,
spread=FALSE, smoother.args=list(lty=2), pch=19,
main="A9-A4",
xlab="Eau",
ylab="Résistance à la compression du béton")
```

##5 Conclusion
Après l'analyse effetuée on peut déterminer les composants qui influence la résistance à la compression du béton (Augmentation ou diminution).
On observe que le 'Superplastifiant' est le composant qui fait augmenter le plus la résistance à la compression du béton.
On observe aussi que l'augmentation de l'eau diminue sensible la résistance à la compression du béton.
Avec les graphiques 'scatter plot' on peut observer que les courbes des tendances entre la résistance à la compression du béton et d'un coté le superplastifiant et de l'autre l'eau sont contraire .
Ce qui est cohérent étant donné que le superplastifiant pour diminuer la quantité d'eau que contient le béton et ainsi augmenter leur résistance.

Notons que les modèles de régression linéaire que nous avons utilisés ne sont pastrès  rigoureux et qu'on devra les améliorés pour des analyses plus pertinentes.

##6 References
[1] Statistical Tools For High-Throughput Data Analysis.Logicil R.
disponible sur :http://www.sthda.com/french/wiki/logiciel-r

[2] I-Cheng Yeh.Concrete Compressive Strength Data set. 3/08/2007. 
disponible : https://archive.ics.uci.edu/ml/datasets/Concrete+Compressive+Strength

[3] Robert Prue . Boxplots Using the Amasing R and R command.1703/2014
disponible :https://www.youtube.com/watch?v=WmHcl1xLFEU

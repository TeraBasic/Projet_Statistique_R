Concrete Compressive Strength (la résistance à la compression du béton)

---------------------------------

Type de données: multivarié
 
Résumé: Le béton est le matériau le plus important en génie civil. 
la résistance à la compression du béton est une fonction hautement non linéaire de l'âge et de ces composents.
 Notamment le ciment, le laitier de haut fourneau, les cendres volantes,
l'eau, le superplastifiant, l'agrégat grossier et l'agrégat fin.

---------------------------------

Sources: 

  Original Owner and Donor
  Prof. I-Cheng Yeh
  Department of Information Management 
  Chung-Hua University, 
  Hsin Chu, Taiwan 30067, R.O.C.
  e-mail:icyeh@chu.edu.tw
  TEL:886-3-5186511

  Date Donated: August 3, 2007
 
---------------------------------

Caractéristiques de données:
    
La résistance réelle à la compression du béton (MPa) pour un mélange donné
 a été déterminé à partir du laboratoire en fonction de son âge spécifique (jours). 
Les données sont sous forme brute (non échelonnées).

Statistiques récapitulatives:

Nombre de cas (observations): 1030
Nombre d'attributs: 9
Répartition des attributs: 8 variables d'entrée quantitatives et 1 variable de sortie quantitative
Valeurs d'attribut manquantes: Aucune

---------------------------------


Informations sur les variables

On donne pour chaque variable le nom, le type, l'unité de mesure et une brève description.
La résistance à la compression du béton est le problème de la régression. 
L'ordre des variables ci-dessous correspond à l'ordre des chiffres le long des lignes de la base de données. 

Name                                    Data Type           Measurement                 Description

Cement (component 1)                   quantitative       kg in a m3 mixture           Input Variable
Blast Furnace Slag (component 2)       quantitative       kg in a m3 mixture           Input Variable
Fly Ash (component 3)                  quantitative       kg in a m3 mixture           Input Variable
Water (component 4)                    quantitative       kg in a m3 mixture           Input Variable
Superplasticizer (component 5)         quantitative       kg in a m3 mixture           Input Variable
Coarse Aggregate (component 6)         quantitative       kg in a m3 mixture           Input Variable
Fine Aggregate (component 7)           quantitative       kg in a m3 mixture           Input Variable
Age                                    quantitative       Day (1~365)                  Input Variable
Concrete compressive strength          quantitative       MPa                          Output Variable 
---------------------------------
Problématiques :
  Savoir s'il y a une relation entre "Concrete compressive strength" et les autres attributs ?
  ou simplement y'a t-il une relation entre un attribut (Input variable) et Concrete compressive strength.
  Y'a t-il un attribut qui détermine la résistance du béton à la compression?

--------------------------------------
Dans notre traitement , nous allons utiliser d'autres variables à la place des attributs :
A1 pour "Cement";
A2 pour "Blast Furnace Slag";
A3 pour "Fly Ash";
A4 pour "Water";
A5 pour "Superplasticizer ";
A6 pour "Coarse Aggregate";
A7 pour "Fine Aggregate";
A8 pour "Age";
A9 pour "Concrete compressive strength".

---------------------------------

 Méthode d’analyse et les visualisations
	- statistic simple et description des données.
	- visualisation des données en utilisant les graphiques et les diagrammes qu'on a vue dans les cours.
	- regression linéaire : qualité = a*acidity + b*volatile + c*acid + d* residual sugar ...

'library' utiles pour notre analyse: 
  - ggplot2
  - xlsx
  - car


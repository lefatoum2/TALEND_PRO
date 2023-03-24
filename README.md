# TALEND_PRO3

* [1. Cas d'utilisation : déplacement de fichiers pdf puis archivage puis suppression des fichiers d'origine](#depl)
* [2. Cas d'utilisation : job fils , job père](#perefils)
* [3. Cas d'utilisation : Gestion de l’erreur OutOfMemory](#outofmemory)
* [4. Cas d'utilisation : Filtre des colonnes](#colonnes)
* [5. Cas d'utilisation : Filtre des lignes](#lignes)
* [6. Cas d'utilisation: insertion de plusieurs fichiers dans une base de donnée](#insertionfichiers)
* [7. Cas d'utilisation: update d'une table](#update)
* [8. Cas d'utilisation: suppression d'une ou des lignes d'une base de donnée avec un fichier pivot](#suppression)
* [9. Cas d'utilisation: extraction mensuelle ou trimestrielle](#mensuel_trim)
* [10.Cas d'utilisation: sélectionnez plusieurs fichiers csv ou txt pour faire qu'un fichier xls](#csv_xls)
* [11.Routines](#routines)
## 1. Cas : déplacement de fichiers pdf puis archivage puis suppression des fichiers d'origine<a class="anchor" id="dep1"></a>
![depl1](Talend_images/deplacement_archivage_suppression.png)
![depl2](Talend_images/deplacement_archivage_suppression2.png)
![depl3](Talend_images/deplacement_archivage_suppression3.png)
![depl4](Talend_images/deplacement_archivage_suppression4.png)
![depl5](Talend_images/deplacement_archivage_suppression5.png)
![depl6](Talend_images/deplacement_archivage_suppression6.png)

## 2. Cas : Cas d'utilisation : job fils , job père<a class="anchor" id="perefils"></a>

![perefils1](Talend_images/perefils1.png)
![perefils2](Talend_images/perefils2.png)
![perefils3](Talend_images/perefils3.png)

On peut copier le shéma de sortie du job fils
![perefils4](Talend_images/perefils4.png)
![perefils5](Talend_images/perefils5.png)


## 3. Cas d'utilisation : Gestion de l’erreur OutOfMemory<a class="anchor" id="outofmemory"></a>
![OutOfMemory1](Talend_images/OutOfMemory1.png)
Il faut cocher sur la case "Utiliser les arguments JVM spécifiques
![OutOfMemory2](Talend_images/OutOfMemory2.png)
Puis changer la valeur "-Xmx 1024M" 
![OutOfMemory3](Talend_images/OutOfMemory3.png)
![OutOfMemory4](Talend_images/OutOfMemory4.png)
![OutOfMemory5](Talend_images/OutOfMemory5.png)
![OutOfMemory6](Talend_images/OutOfMemory6.png)
![OutOfMemory7](Talend_images/OutOfMemory7.png)



## 4. Cas d'utilisation : Filtre des colonnes<a class="anchor" id="colonnes"></a>
## 5. Cas d'utilisation : Filtre des lignes<a class="anchor" id="lignes"></a>
## 6. Cas d'utilisation: insertion de plusieurs fichiers dans une base de donnée<a class="anchor" id="insertionfichiers"></a>
![integration_plusieurs_fichiers](./Talend_images/integration_plusieurs_fichiers.png)
## 7. Cas d'utilisation: update d'une table<a class="anchor" id="update"></a>
Il y a deux manières de faire un update :

- soit à partir d'un fichier client

![update1](./Talend_images/update1.png)
Vous devez obligatoire choisir une clé pour faire la mise à jour et choisir les valeurs à mettre à jour.
![update2](Talend_images/update2.png)

- soit du composant TDBRow 

![update4](./Talend_images/update4.png)
![update3](./Talend_images/update3.png)

- soit avect tmap en forçant les valeurs :

![update5](./Talend_images/update_tmap1.png)
![update6](./Talend_images/update_tmap2.png)

Dans cet exemple, j'essaie de forcer avec une mise à jour le numéro identifiant(IDClub) du club d'un joueur de football.


Attention : vous devez spécifier au moins une colonne comme clé primaire sur laquelle baser les opérations Update ou alors Delete.

## 8. Cas d'utilisation: suppression d'une ou des lignes d'une base de donnée avec un fichier pivot<a class="anchor" id="suppression"></a>
Dans cet exemple, j'essaie de supprimer la ligne d'un consommateur à l'aide de son identifiant et de son nom mis dans un fichier.

![suppression](./Talend_images/suppression.png)

![suppression_tmap](./Talend_images/suppression_tmap.png)

Attention : comme pour une mise à jour, la suppression demande une clé de suppression. Pour ma part, j'ai choisi l'identifiant du joueur(ID).

![suppression_tdbouput](./Talend_images/suppression_tdbouput.png)

![suppression_tdbfilterrow](./Talend_images/suppression_tfilterrow.png)

## 9. Cas d'utilisation: extraction mensuelle ou trimestrielle <a class="anchor" id="mensuel_trim"></a>

tJava
```java
context.DateLancement =  TalendDate.getCurrentDate();

Date FirstDayMoisPrecedent = TalendDate.getFirstDayOfMonth(TalendDate.addDate(context.DateLancement,-1,"MM"));
 
context.FirstDayMoisPrecedent = TalendDate.formatDate("dd-MM-yyyy", FirstDayMoisPrecedent);

context.LastDayMoisPrecedent = TalendDate.formatDate("dd-MM-yyyy", TalendDate.getLastDayOfMonth(FirstDayMoisPrecedent)) ;

context.AnneeMoisPrecedent = TalendDate.getPartOfDate("YEAR", FirstDayMoisPrecedent);
```

## Cas d'utilisation: sélectionnez plusieurs fichiers csv ou txt pour faire qu'un fichier xls<a class="anchor" id="csv_xls"></a>

Pour le composant tFileOutputExcel, n'oubliez pas de cocher "Ajouter à la feuille existante". 
Pour le composant tInputDelimited_2, sélectionnez "...CURRENT_FILEPATH..." de "tFileList" pour le mettre dans le "Nom de fichier/Flux".

![gestion_fichiers](./Talend_images/gestion_fichiers2.png)

![gestion_fichiers2](./Talend_images/gestion_fichiers3.png)

## Routines<a class="anchor" id="routines"></a>

```java
row1.FirstName+' '+row1.LastName 
StringHandling.DOWNCASE(row1.FirstName+row1.LastName)+"@gmail.fr" 
!Relational.ISNULL(row1.Prenom)&& !Relational.ISNULL(row1.Nom)&&!Relational.ISNULL(row1.SIRET) 
StringHandling.LEN(row1.Prenom)>5 &&StringHandling.LEN(row1.Nom)> 5 
StringHandling.LEN(row1.NSS) == 13 || StringHandling.LEN(row1.NSS) == 15
StringHandling.LEFT("chaîne à vérifier", n premiers caractères d'une chaîne de caractères)
StringHandling.RIGHT("chaîne à vérifier", n derniers caractères d'une chaîne de caractèr)
TalendDate.getDate("CCYY-MM-DD")
```

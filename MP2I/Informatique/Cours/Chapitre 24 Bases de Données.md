# A)<u>Requêtes sur une table</u> :

## I)<u>Relations ou tables</u> :

### 1)<u> Définition</u> :

>[!cours] 
>On appelle <font color = "red"><u>relation</u></font> (ou <font color = "red"><u>table</u></font>) un ensemble d'<font color = "red"><u>enregistrements</u></font>
>Chaque enregistrement d'une table est la description d'une <u>entité</u> du monde réel

>[!example] BD - 1 : les entités sont des pays
>Chaque entité est décrite par la valeur d'un certain nombres d'<u>attributs</u>
>>[!example] BD - 1 : nom, continent, ... , pib du pays 

### 2)<u>Schéma d'une relation</u> :

>[!cours]
>On appelle <font color = "red"><u>schéma</u></font> d'une <font color = "red"><u>relation</u></font> la donnée de  tous mes <font color = "red"><u>attributs</u></font> et de leur <font color = "red"><u>domaine</u></font> c'est-à-dire  de l'ensemble des valeurs que chaque attribut peut prendre.

>[!example] 
>pays ( nom string,
>iso-3611 string,
>population integer,
>superficie integer,
>pid float)
>
>pays  : table
>première colonne : nom des attributs
>deuxième colonne : domaine de chaque attributs (se réduit généralement à un type de valeurs)

>[!remarque] Remarque 
>on donne parfois les types du langage SQL pour spécifier le domaine : par exemple :
>INT 
>BIGINT 
>VARCHAR(10) : chaîne de longueur au plus 10
>etc 

### 3)<u>Clé primaire</u> : <font color = "red">(important)</font>

On appelle clé primaire, un attribut ou un n-uplet d'attributs, qui prend des valeurs distinctes sur des entités distinctes.
Il existe parfois plusieurs choix possibles de clé primaire : on parle alors de clé candidates à être clé primaire, et c'est le concepteur de la base de donnée qui choisit celle qui lui convient.

>[!example] BD - 1
>Deux possibilités de clé primaire : le nom ou le code iso
>

>[!example] un base d'élèves 
>INE ou le triplet (nom, prénom, date de naissance)
>
>*inconvénient (hormis le cas peu probable mais possible d'avoir 2 étudiants avec le même triplet) ce choix rend difficile de corriger la valeur de l'un des 3 attributs*

### 4)<u>Clé étrangère</u> :


Une clé étrangère est un attribut ou n-uplet d'attributs, qui correspond (sans utiliser forcément les mêmes noms d'attributs) à une clé primaire dans une autre table.

La présence d'une clé étrangère (et déclarer comme telle par le concepteur de la base de données) permet de faire respecter des contraintes d'intégrité, à savoir : 

 - un attribut (ou n-uplet d'attributs) déclarer comme clé étrangère ne pourra pas  prendre de valeurs qui ne soit pas présente dans la table où se trouve la clé primaire correspondante.
 
>[!example] on ne peut utiliser dans une table un INE ne correspondant à aucun étudiant dans la base établissement

 - inversement, il ne sera pas possible de supprimer un enregistrement dans la table où l'attribut est la clé primaire, si la valeur de la clé primaire apparaît dans une autre table.
 
>[!example] on ne peut supprimer un élève et son INE dans la base élève si ce élève (via son INE) est présent dans une autre table.

>[!note] 
>L'existence d'une clé étrangère permet, par ailleurs, de construire des jointures (voir après)

# II)<u>Requêtes SQL sur une table</u> :

Le langage SQL est un langage permettant de construire, modifier, interroger des bases de données, constituées de différentes tables.
Il s'agit d'un <font color = "red"><u>langage de description</u></font> et non d'un langage de programmation :
 - Il n'y aura ni variables, ni boucles, mais uniquement des <font color = "red"><u>requêtes</u></font> dans lesquelles on *décrira* les informations, les données que l'on souhaites ajouter, modifier, ou afficher.

>[!question] 
>*Dans le cadre de MPI, on se contente d'interroger les bases de données (pas de créations, ajout ou modification).*

### 1)<u>Syntaxe générale d'une requête</u> :

``` SQL 
SELECT ... FROM <table>
```

>[!summary] Commentaires
> `...` : attributs
> `<table>` : la table à interroger (qui contient les données à explorer) 

>[!important] 
>`SELECT * FROM nom_table` -> affiche tous les enregistrements de la table
>(une ligne d'entêtes où figurent les attributs puis une ligne par enregistrement et une colonne par attribut)

>[!note] À avoir en tête
>Toute requête renvoie une table

### 2)<u>Nombre d'enregistrement</u> :

``` SQL 
SELECT COUNT(*) FROM nom_table
```
>[!summary] Commentaires
>renvoie le nombre d'enregistrements

>[!example] BD - 1
>`SELECT COUNT(*) FROM pays` 
>renvoie 
>
| COUNT (*) |
| --------- |
| 249       |

### 3)<u>Opération de sélection</u> :

>[!warning] Le mot SELECT est un faux-ami

>[!cours]
>L'opération de sélection, s'opère avec la classe `WHERE`, et qui consiste à ne garder que les enregistrements d'une table qui vérifient un certain critères*  portant sur les valeurs des l'attributs de l'enregistrement

>[!example] SELECT * FROM pays WHERE population > 100e6 AND superficie 1e6
>table : pays
>critère : population > 100e6 AND superficie 1e6
>1e6 = $10^6$

>[!cours]
>Les opérateurs à connaître pour écrire les critères : 
>`=, <>, <, <=, >, >=, AND, OR, NOT`
>`IS NULL`
>`IS NOT NULL`
>*NULL* est une valeur spéciale que l'on peut donner à un attribut lorsque la valeur de cet attribut n'est pas connue. (ou n'existe pas) pour un certain enregistrement (<u>ex</u>: numéro de téléphone)
>>[!warning] `attr = NULL` et `attr <> NULL` ne fonctionne pas

>[!warning] Il n'est pas possible de tester des encadrements
>`2 < a < 3` : NON 
>`2 < a AND a < 3` : OUI

>[!cours] Tests (hors programme) :
> - `attr IN ( , , , )` ; 
> - - <u>ex</u> : `nom IN ("toto","titi")` 
> 
>  - `attr LIKE "...%..."` ;
>  -  - <u>ex</u> : `nom LIKE "a%"` : nom qui commencent par `a` 
>  - *% représente une chaîne de caractères quelconque*

### 4)<u>Opération de projection et autres opérations sur les attributs</u> : 

>[!cours]
>Après le `SELECT`, on peut utiliser le caractère `*` pour afficher la valeur de tous les attributs pour les enregistrements sélectionnés.
>Ou n'en choisir que quelques-uns (opération de projection)
> - les réordonner
> - faire des calculs sur leur valeurs (`*,-,/,+`)
> - les renommer (`AS`)

>[!example] BD - 1
>``` SQL 
>SELECT nom AS "Nom pays", continent, population / superficie AS densité 
>FROM pays
>```
>`"Nom pays"` : entre guillemet car espace dans le nouveau nom
>>[!warning] guillemet obligatoires pour les valeurs de type strings

### 5)<u>Tri d'une table (issue d'une requête)</u> :

``` SQL 
SELECT ... FROM ...
WHERE ....
ORDER BY attr1 ASC (ou DESC)
```

>[!summary] Commentaires
>ligne 1-2 : requête
>`ORDER BY` : tri des lignes par rapport à la valeur de attr1 
>`ASC` : croissant
>`DESC` : décroissant
>
>le tri est par défaut croissant donc spécifier `ASC` est facultatif

>[!note] Note (hors programme)
>On pourrait spécifier plusieurs clés de tri :
>`ORDER BY attr1 DESC, attr2`
>tri d'abord selon la val de attr1 (décroissant) puis si égalité selon la valeur de attr2 (croissant)

### 6)<u>LIMIT, OFFSET</u> :

>[!cours] 
>Les classes LIMIT et OFFSET prennent sens et leur intérêt combinés avec un tri préalable (ORDER BY)
> - `LIMIT n` : ne renvoie que les `n` premiers enregistrements
> - `LIMIT n OFFSET p`  : ne renvoie que les `n` premiers enregistrements suivant les `p` premiers, (qui sont eux, retirés du résultat).

# III)<u>Requêtes impliquées ou sous-requêtes</u> :

>[!cours] 
>On peut utiliser le tableau d'une requête (c'est-à-dire la table renvoyée par une requête) dans 3 cas de figures :
> - si la requête renvoie une unique valeur (la sous-requête est utilisée comme une valeur).
>>[!example] 
>>``` SQL 
>>SELECT nom FROM pays 
>>WHERE pib > (SELECT pib FROM pays WHERE nom ="Islande")
>>```
>>
>>`SELECT pib FROM pays WHERE nom ="Islande"` : sous-requête renvoyant le pib de l'Islande
>
> - si la requête renvoie une liste de valeurs (hors programme)
>>[!example] 
>>``` SQL 
>>SELECT nom FROM pays
>>WHERE contient IN (SELECT contient FROM pays ORDER BY population DESC LIMIT 3)
>>```
>>Renvoie la liste des pays qui sont sur le/les *contient(s) auxquels appartiennent les trois pays les plus peuplés*.
>
> - la table issue d'une requête peut être utilisé comme table après le FROM
>>[!example] 
>>``` SQL 
>>SELECT ... 
>>FROM (SELECT nom, contient, population FROM pays WHERE population > 10e6)
>>...
>>```
>>pour les pays ayant plus de 10 millions d'habitants

## IV) Fonctions d'agrégation :
>[!definition] 
>Les fonctions d'agrégations permette de faire des calculs sur les valeurs d'un meme attribut sur tous les enregistrement d'unr table 

### 1/ Listes des fonctions à connaître

>[!formule] Fonction
>```SQL
>COUNT(attr)
>```
>- Compte les enregistrements pour lesquels l'attribut `attr` a une valeur 
>(ne le compte pas si pas de valeur ou si la valeur est `NULL`)
>
>```SQL
>COUNT(*)
>```
>
>- Compte le nombre total d'enregistrements (lignes) de la table.
>
>
>>[!remarque]
>>```SQL
>>COUNT(DISTINCT attr)
>>```
>>- Compte le nombre de valeurs distinctes prises par l'attribut dans la table 


>[!formule] Autre fonctions d'agrégation
>
>```SQL
>SUM
>AVG
>MIN
>MAX
>```
>>[!example] 
>>```SQL
>>SELECT AVG(population) / 1e6 , SUM(pib)/COUNT(pib) FROM pays
>>```
>>- Renvoie une table qui n'a qu'une *seule* ligne qui donne le nombre d'habitant moyen par pays en milliards d'habitants.
>>  le pib moyen des pays du globe

### 2/ Calculs sur des agrégats

On peut calculer les valeurs des fonctions d'agrégation sur des sous-ensembles (agrégat) d'enregistrements définis par la valeur prise par un certain attribut.

On utilise alors la clause `GROUP BY` pour effectuer ces regroupements.

On obtient alors une table ayant autant de lignes qu'il y a de sous ensemble 

>[!example] 
>```SQL
>SELECT continent, SUM(population) FROM pays
>GROUP BY continent
>```
>- La requête renvoie le nom des continents et leur population totale

>[!warning]
>Dans une requête utilisant un regroupement avec `GROUP BY`, hormis les valeurs de fonctions d'agrégation (par gorupe), cela ne fait pas sens de demander la valeurs d'attribut dont la valeur n'est pas constante sur chaque regroupement.


>[!remarque]
>Si on calcule des fonctions d'agrégation sans `GROUP BY` on ne peut demander que l'affichage de valeurs de fonctions d'agrégation car il n'y aura qu'une ligne dans la réponse 

Lorque l'on a utilisé `GROUP BY` on peut retenir, dans la table résultats, que les lignes vérifiant un certain critère portant portant sur les valeurs prises par les fonctions d'agrégations.

On utilise la clause `HAVING`

>[!example] 
>```SQL
>SELECT continent, SUM(population) FROM pays
>GROUP BY continent
>HAVING SUM(population)>1e9
>```
>>[!warning] Ne pas confondre `WHERE` et `HAVING`

## V) Opérations ensemblistes 

On peut combiner les resultats de deux requêtes à l'aide d'opération ensemblistes 
- `UNION` : union $AB$ 
- `INTERSECT` : intersection $AB$
- `EXCEPT` : Différence $AB$

On va dire ce qu'il en est des associations de cardinalité $*-*$

Une association $*-*$ peut se décomposer en deux associations $1-*$ et $*-1$, ce qui permet de passé du modèle E/A au modele relationnel, en créant une table décrivant l'association "joue dans" (table casting dans l'example du cours) et en la <mark style="background: #FFB86CA6;">liant </mark> aux tables représentant les deux ensembles d'entités reliés par l'associations grâce aux liens <mark style="background: #FFB86CA6;">clé primaire - clé étrangère</mark>


De façon générale, on peut passer du modèle E/A au modèle relationnel, en créant une table par ensemble d'identités et une table par ensemble d'associations 

Mais pour les asso







































---
#Informatique 
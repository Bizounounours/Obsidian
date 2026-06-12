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

## 5. Opérations ensemblistes
On peut combiner les résultats de deux requêtes à l'aide d'opérations ensemblistes (`UNION`[^5],`INTERSECT`[^6],`EXCEPT`[^7]) pour vu que les résultats des deux requêtes aient le **même nombre de colonnes** et que **le domaine des colonnes situées à la même position soit le même**.

> [!example] Exemple
> Voir notebook [cd13-10817352](https://capytale2.ac-paris.fr/p/basthon/n/?kernel=sql&mode=assignment&id=10817663)
> 
> ```sql
> SELECT realisateur FROM film -- Renvoie les identifiants des réalisateurs de film
> INTERSECT
> SELECT id_acteur FROM casting -- Renvoie les identifiants des acteurs ayant joué dans un film
> ```
> 
> Chaque requête renvoie une colonne, avec un attribut de type int.
>
> La requête complète renvoie les identifiants des acteurs qui ont aussi réalisé au moins un film.
>
> >[!tip] Note
> > La requête fonctionnerait en remplaçant `id_acteur` par `id_film` (même nombre de colonnes même domaine) mais le résultat n'aurait pas de sens.

# II. Bases de données comportant plusieurs tables
## 1. Modèle entité-association
### A. Description du modèle
On prend comme exemple la base de données `cinema` du notebook [cd13-10817352](https://capytale2.ac-paris.fr/p/basthon/n/?kernel=sql&mode=assignment&id=10817663), qui contient la description d'entités de deux natures distinctes :
- Les **INDIVIDUS** : **acteurs** ou des **réalisateurs**, décrit dans la table `acteur`[^8] par leur *nom* et un identifiant *id*
- Les **FILMS** : décrits dans la table `film` par les attributs *id, titre, annee, ..., realisateur*

> [!danger] L'attribut `realisateur` est un identifiant : 
> C'est une [[clé étrangère]] faisant référence à la [[clé primaire]] **id** de la table `acteur`.

Dans le modèle entité-association, on cherche à mettre en évidence les liens entre les entités de divers ensembles d'entités (ici les **INDIVIDUS** et les **FILMS**) au travers d'**ensembles d'associations**.

Ici on peut distinguer les ensembles d'associations (ou, en abrégé, associations) suivants :
- "*joue_dans*" : permet d'indiquer qu'un individu a joué dans un certain film.
- "*réalise_par*" : indique qu'un individu a réalisé un certain film.

Dans le cadre du programme, on se limitera à des associations binaires, entre les entités de deux ensembles $E_{1} = \lbrace e^{1}_{i} \rbrace_{1 \leq i \leq n}$, $E_{2} = \lbrace e^{2}_{j} \rbrace_{1 \leq j \leq n}$ permettant de spécifier qu'une entité $e^{1}_{i}$ de $E_{1}$ est associée à une entité $e^{2}_{j}$ de $E_{2}$

Pour une association donnée, on précisera sa **[[cardinalité]]**, précisant combien d'élément de l'un des deux ensembles peuvent être associés à un élément de l'autre ensemble.

La **cardinalité** est donnée sous la forme d'un couple du type $1-1$, $1-n$, $*-1$, $1-*$,$*-*$.
- $1-1$ : Dénote que chaque élément de $E_{1}$ est associé à un et un seul élément de $E_{2}$ (l'association définit une bijection entre $E_{1}$ et $E_{2}$)
- $1-*$ : Chaque élément de $E_{1}$ est associé à un nombre quelconque d'éléments de $E_{2}$ (Éventuellement nul) tandis que chaque élément de $E_{2}$ est associé à un unique élément de $E_{1}$. (le lien d'association définit une application de $E_{2}$ vers $E_{1}$)
- $*-1$ : idem dans l'autre sens (échanger $E_{1}$ et $E_{2}$)
- $*-*$ : Chaque élément de $E_{1}$ peut-être associé à un nombre quelconque d'éléments de $E_{2}$ et réciproquement. (Le lien d'association correspond à une relation binaire, sans plus)

> [!tip] Remarque
> Si on écrit $n$ au lieu de $*$, cela signifie que la valeur $0$ n'est pas autorisée.

> [!example] Exemple
> *joue_dans* est de cardinalité $*-*$ 
> - Un individu peut n'avoir joué dans aucun film ou dans un nombre quelconque de films.
> - Un film peut avoir un nombre quelconque d'acteurs éventuellement aucun
> 
> *realise_par* est de cardinalité $*-1$
> - Chaque film est réalisé par un individu dans la BD étudiée

On résume les informations sur les liens d'association entre les ensembles d'entités par un diagramme :
![[Liens d'association.png]]

- Séparation d'une association $*-*$ en deux associations $*-1$ et $1-*$
  
  Pour ce faire, on peut définir un nouvel ensemble d'entités, dont les éléments sont les associations d'un élément de $E_{1}$ avec un élément de $E_{2}$ auquel il est associé.

> [!example] Exemple
> Pour l'association *joue_dans*, on peut définir un ensemble d'entité **ROLES** dans lequel chaque élément traduit qu'un certain individu a joué dans un certain film.
> 
> Cet ensemble d'entités, **ROLES**, est réalisé par la table `casting` dont le schéma relationnel est `casting(id_acteur entier, id_film entier, num entier)` [^9]

On a maintenant :
![[Pasted image 20260519095053.png]]

### B. Traduction en SQL des associations 1-1 ou 1-\*
Si on a une association $1-1$ ou $1-*$ entre deux-ensembles d'entités $E_{1}$ et $E_{2}$, représentés par des tables $t_{1}$ et $t_{2}$, et qu'une clé étrangère existe pour $t_{1}$ renvoyant à une [[clé primaire]] dans $t_{2}$, on peut matérialiser le lien d'association de la façon suivante :
![[Pasted image 20260519100110.png]]

On va dire ce qu'il en est des associations de cardinalité $*-*$.

Une association $*-*$ peut se décomposer en deux associations $1-*$ et $*-1$, ce qui permet de passer du modèle E/A au modèle relationnel, en créant une table décrivant l'association "*joue_dans*" ([[24. Base de donnée#A. Description du modèle|table casting dans l'exemple du cours]]) et en **la reliant** aux tables représentant les deux ensembles d'entité reliés par l'association, grace aux liens **clé primaire-clé étrangère**.

De façon générale, on peut passer du modèle E/A au modèle relationnel, en créant une table par ensemble d'entités et une table par ensemble d'associations.

Mais pour les associations $1-*$ ou $*-1$, le lien clé primaire-clé étrangère peut permettre de faire l'économie d'une table représentant l'association. 

Il est possible que les associations d'un ensemble d'association aient des propriétés (ou attributs), de même que les entités ont des propriétés.

C'est le cas ici, où pour l'association "*joue_dans*" on a ajouté la propriété "*rang_dans_la_distribution*" (attribut *num* dans *casting*).

On peut le signaler ainsi :
![[Pasted image 20260522082755.png]]

## 2. Jointures
### A. Produit cartésien de deux tables
```sql
SELECT * FROM table1,table2
```
Ou de façon équivalente.
```sql
SELECT * FROM table1 JOIN table2
```

Construit une table dont les lignes sont, chacune, la concaténation d'un enregistrement de la table `table1` et d'un enregistrement de la table `table2` sans que nécessairement la juxtaposition des deux enregistrements ait de sens.  

> [!example] Exemple
> ```sql
> SELECT * FROM film,acteur
> ```
> Attributs de la table retenu renvoie :
>
| film    | < | <   | <           | individu | <   |
| --- | ----- | --- | ----------- | -------- | --- |
| id  | titre | ... | realisateur | id       | nom |
>

Si $table_{1} = \{ent_{i}^1\}_{1 \leq i \leq n}$ et $table_{2} = \{ent_{j}^2\}_{1\leq j \leq m}$

Le produit cartésien est l'ensemble $\{ (ent_{i}^1,ent_{j}^2)\}_{\cases{1\leq i\leq n  \\ 1\leq j\leq m}}$ et a pour cardinal $|table_{1}|\times|table_{2}|$.

> [!example] Exemple
> Sur l'exemple $|film| = 1500$ et $|acteur| = 2000$
> 
> La table résultante à $3M$ de lignes
>> [!danger] Affichage

### B. Jointures
On peut imposer que deux enregistrements $ent_{i}^1$, $ent_{j}^2$ ne soient réunis une ligne que si un certain critère portant sur leurs attributs est vérifié de la façon suivante :
```sql
SELECT * FROM table1 

JOIN table 2
ON -- Critère
```
Ou bien
```sql
SELECT * FROM table1,table2

WHERE -- Critère
```

> [!example] Exemple
> ```sql
> SELECT * FROM film 
> 
> JOIN acteur
> ON film.realisateur = acteur.id
> ```

Ici, le critère `film.realisateur = acteur.id` assure que l'individu à droite est le réalisateur du film (et cela permet de connaitre son nom[^10] et pas seulement son identifiant (attribut *realisateur* de la table *film*)).

 - On doit obligatoirement **préfixer** le nom de l'attribut par le nom de la table si le nom le même nom d'attribut est utilisé dans les deux tables.
   
   Donc `film.realisateur` peut être remplacé par `realisateur` alors qu'on ne peut pa remplacer `acteur.id` par `id` car `id` n'est pas unique.
   
   On peut décider que l'on préfixera toujours.
   
 On peut utiliser aussi un renommage
   
 ```sql
 SELECT * FROM film AS F 
 
 JOIN acteur AS I
 ON F.realisateur = I.id
 ```

#### Jointure "naturelle"
Lorsqu'un attribut (ou un n-uplet d'attributs) est une clé étrangère dans une table *t1*, qui fait référence à un clé primaire d'une table *t2*, il découle que la jointure suivante est possible et a du sens :
```sql
SELECT * FROM t1

JOIN t2
ON t1.attr1 = t2.attr2 -- Clé étrangère = Clé primaire correspondante
(AND t1.attr3 = t2.attr4) -- Si les clés sont des n-uplets (attr1,attr3) et (attr2,attr4)
...
```

> [!tip] Remarque
> Tant que l'on reste là (`SELECT *`) la table résultante a pour attributs tous les attributs des 2 tables.
> 
> Et `t1.attr1` et `t2.attr2` sont égaux et donc présents 2 fois

On pourra utiliser des projections pour supprimer les colonnes redondantes ou inutiles.

Dans les cas, il s'agit après avoir fait la jointure, de réaliser sur la table résultante toutes opérations utiles pour obtenir le résultat demandé.

#### Jointures multiples
```sql
SELECT * FROM table1 

JOIN table2
ON -- Critère

JOIN table3
ON -- Critère
-- ad libitum
```
Chaque critère devant porter sur des attributs des tables qui précèdent.

#### Auto-jointure
On peut joindre une table avec elle-même mais il y a nécessité de renommer la table.
```sql
SELECT * FROM casting AS c1

JOIN casting AS c2
ON c1.id_film = c2.id_film
```

On obtient :

| c1        | <       | <   | c2        | <       | <   |
| --------- | ------- | --- | --------- | ------- | --- |
| id_acteur | id_film | num | id_acteur | id_film | num |
| 47        | 23      | 2   | 205       | 23      | 2   |
L'acteur(trice) 47 a joué dans le film 23 avec l'acteur(trice) 205


> [!tip] Remarque
> Utile pour savoir si 47 a joué avec 205 
> 
> Mais on peut le savoir aussi en faisant :
> ```sql
> SELECT id_film FROM casting
> 
> WHERE id_acteur = 47
> INTERSECT
> SELECT id_film FROM casting
> 
> WHERE id_acteur = 205
> ```

---
#Informatique #cours
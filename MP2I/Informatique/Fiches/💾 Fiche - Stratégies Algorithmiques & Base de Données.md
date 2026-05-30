


## PARTIE I : STRATÉGIES ALGORITHMIQUES (CHAPITRE 23)

### 1. Force brute
* **Champ d'application :** Cette démarche (la plus élémentaire) consiste à tester toutes les solutions envisageables du problème (explorer l'ensemble des candidats) et à s'arrêter dès qu'une solution est trouvée.

>[!definition] Force brute
>Démarche algorithmique qui suppose que :
> 1. Il est possible de parcourir l'ensemble des solutions envisageables (candidats).
> 2. Il doit être possible de tester si un candidat est solution.

* **Complexité :** La complexité est souvent **exponentielle** et la résolution par cette méthode irréaliste à grande échelle.
* **Implémentation :** Généralement, on s'arrête à la $1^{\text{ère}}$ solution trouvée en utilisant un `break` en C ou une exception en OCaml.

>[!example]- Exemple du Sudoku
>Au Sudoku, la force brute consiste à tester tous les 81-uplets à valeurs dans $[\![1;9]\!]$, ce qui représente $9^{81}$ candidats possibles (autant de candidats que d'éléments dans $[\![1;9]\!]^{81}$).

---

### 2. Retour sur trace (*Backtracking*)

>[!definition] Retour sur trace (Backtracking)
>Méthode de recherche où l'on cherche à construire la solution **de proche en proche** (étape par étape) en revenant en arrière à chaque fois que l'on arrive à une impasse. On recule juste suffisamment pour pouvoir tester d'autres options.

* **Modélisation par un arbre :** On peut se figurer la recherche au travers d'un arbre :
    * **Nœud interne :** Étape intermédiaire de construction (possède autant de fils que de choix possibles).
    * **Feuille :** Correspond soit à une impasse, soit à une solution finale.

>[!example]- Exemple des 4 reines
>On cherche à placer 4 reines sur un plateau de 16 cases de sorte qu'aucune n'en menace une autre. Pour qu'une configuration soit solution, il faut (contrainte forte) qu'il y ait exactement une reine par ligne, ce qui guide la construction étape par étape.

---

### 3. Algorithmes gloutons
* **Champ d'application :** Problèmes d'**optimisation** (choisir parmi plusieurs solutions possibles celle qui maximise ou minimise une certaine quantité, appelée fonction objectif).

>[!definition] Algorithme glouton
>Algorithme qui effectue une suite de choix les uns après les autres, **sans jamais remettre en cause un choix passé**. À chaque étape, on utilise une **heuristique** pour faire le choix localement optimal.

* **Limitation :** Rien n'assure de façon générale qu'un algorithme glouton fournisse la solution optimale globale. On cherche un compromis entre complexité et qualité de l'approximation.

>[!example]- Exemple 1 : Le problème du sac à dos (*Knapsack problem*)
>* **Problème :** $n$ objets possédant chacun un poids $p_i$ et une valeur $v_i$. On dispose d'un sac de capacité maximale $C$. On souhaite maximiser la valeur totale des objets emportés sans dépasser le poids $C$.
>* **Stratégie gloutonne :** Nécessite de trier préalablement les objets selon un critère, d'où une complexité générale en $O(n \log n)$ due au tri.
>* **Trois heuristiques possibles du cours :**
>  1. *Par valeur décroissante :* On choisit l'objet restant le plus précieux.
>  2. *Par poids croissant :* On choisit l'objet restant le plus léger.
>  3. *Par rapport $\frac{v_i}{p_i}$ décroissant (valeur massique) :* Donne souvent de meilleurs résultats, mais reste non optimale dans le cas général (sac discret).

>[!example]- Exemple 2 : Le rendu de monnaie
>* **Principe :** Choisir toujours la pièce ou le billet de plus grande valeur possible inférieur à la somme restante à rendre.
>* **Optimalité :** L'algorithme donne la solution optimale (un nombre minimal de pièces) pour un système de monnaie dit **canonique** (comme l'Euro), mais échoue à être optimal pour d'autres systèmes (ex: l'ancien système britannique).

>[!example]- Exemple 3 : La planification d'événements
>* **Problème :** On cherche à planifier un nombre maximal d'événements compatibles dans une seule salle, chaque événement $i$ ayant une date de début $d_i$ et de fin $f_i$.
>* **Heuristique optimale :** Choisir systématiquement l'événement compatible qui se **finit le plus tôt** (date de fin $f_i$ minimale). C'est la seule stratégie gloutonne qui garantit l'optimum global ici. Complexité en $O(n \log n)$ induite par le tri initial des dates de fin.

---

### 4. Diviser pour régner (*Divide and Conquer*)

>[!definition] Diviser pour régner
>Stratégie de conception algorithmique basée sur trois étapes fondamentales :
>1. **Décomposer (Diviser) :** Découper le problème en sous-problèmes indépendants et de plus petite taille.
>2. **Résoudre (Régner) :** Résoudre les sous-problèmes de manière récursive (ou directement si la taille est minimale).
>3. **Combiner :** Réunir les solutions des sous-problèmes pour obtenir la solution du problème d'origine.

>[!example]- Exemples de référence
>* **Tri fusion (*Merge Sort*) :** On coupe le tableau en deux, on trie récursivement chaque moitié, puis on fusionne (interclasse) les deux sous-tableaux triés.
>* **Tri rapide (*Quick Sort*) :** On choisit un élément appelé *pivot*, on partitionne le tableau en mettant d'un côté les éléments plus petits et de l'autre les plus grands, puis on trie récursivement les deux blocs.
>* **Recherche dichotomique :** Cas particulier où le problème est réduit à **un seul** sous-problème plus petit (on ne cherche que dans une seule moitié).

---

### 5. Programmation dynamique

>[!definition] Programmation dynamique
>Méthode consistant à décomposer un problème en sous-problèmes qui **ne sont pas indépendants** (les sous-problèmes se chevauchent). Pour éviter de recalculer de nombreuses fois les mêmes instances, on stocke les résultats intermédiaires dans une structure de données (mémoire).

* **Deux approches d'implémentation :**
    1. **TOP - DOWN (Méthode descendante / Mémoïsation) :** Résolution récursive où l'on utilise une table (ou dictionnaire). Avant tout calcul, on vérifie si le problème a déjà été résolu. Si oui, on renvoie la valeur stockée ; si non, on fait le calcul et on l'enregistre.
    2. **BOTTOM - UP (Méthode ascendante) :** Résolution itérative. On résout tous les problèmes de plus petite taille, puis de proche en proche tous les problèmes de taille croissante en remplissant un tableau jusqu'à atteindre l'instance d'origine.

>[!example]- Exemple : Suite de Fibonacci
>* **Relation de récurrence :** $F_0=0, F_1=1$ et $\forall n \ge 2, F_n = F_{n-1} + F_{n-2}$.
>* **Problème de la récursion naïve :** Pour calculer $F_4$, on appelle $F_3$ et $F_2$. Mais $F_3$ appelle lui-même $F_2$ et $F_1$. Le sous-problème $F_2$ est ainsi résolu deux fois indépendamment. La complexité devient exponentielle.
>* **Solution dynamique :** On sauvegarde les valeurs calculées de $0$ à $n$ dans un tableau, ce qui ramène la complexité temporelle à une étude linéaire $O(n)$.

---

## PARTIE II : BASES DE DONNÉES S2 - LANGAGE SQL (CHAPITRE 24)

>[!rappel] Note du programme
>On se limite volontairement à une description applicative des bases de données en langage SQL permettant d'interroger plusieurs relations. L'algèbre relationnelle et le calcul relationnel sont strictement hors programme.

### 1. Vocabulaire et concepts fondamentaux

>[!definition] Relation / Table
>On appelle **relation** (ou **table**) un ensemble d'**enregistrements** (ou lignes). Chaque enregistrement d'une table est la description d'une entité du monde réel.

* **Attributs :** Les caractéristiques décrivant une entité (les colonnes d'une table).

>[!definition] Schéma d'une relation
>On appelle **schéma** d'une relation la donnée de tous les **attributs** et de leur **domaine**, c'est-à-dire de l'ensemble des valeurs que chaque attribut peut prendre.

* **Domaine :** Au programme, on s'en tient à une notion sommaire de domaine : `entier`, `flottant`, `chaîne`.
>[!remarque] Limites du programme sur les domaines
>Aucune considération quant aux types spécifiques des moteurs SQL (comme la représentation complexe des dates ou les notions de collations) n'est au programme.

>[!definition] Clé primaire (Primary Key)
>Un attribut (ou un groupe d'attributs) dont la valeur permet d'identifier de manière unique chaque enregistrement de la table. La notion d'*index* est hors programme.

>[!definition] Clé étrangère (Foreign Key)
>Un attribut d'une table qui fait référence à la clé primaire d'une autre table. Elle sert à matérialiser des liens et assure les **contraintes d'intégrité référentielle**.

* **Contraintes d'intégrité référentielle :** Interdiction d'insérer une valeur inexistante dans la table pointée ou de supprimer un enregistrement référencé.

---

### 2. Syntaxe des requêtes SQL sur une table

#### A. Structure générale, Sélection et Projection
* `SELECT * FROM table` : Renvoie tous les attributs et tous les enregistrements.
* **Projection :** Sélectionner uniquement certains attributs (colonnes), les réordonner, ou appliquer des opérations arithmétiques (`+`, `-`, `*`, `/`). On peut renommer le résultat d'un attribut à l'aide du mot-clé `AS`.
* **Sélection (Clause `WHERE`) :** Filtrer les lignes (enregistrements) pour ne conserver que celles qui vérifient un prédicat/critère précis.

#### B. Opérateurs de conditionnement
* **Logiques et comparaisons :** `=`, `<>` (différent), `<`, `<=`, `>`, `>=`, `AND`, `OR`, `NOT`.
* **Valeurs manquantes :** Test du vide à l'aide de `IS NULL` et `IS NOT NULL`.
>[!remarque] Attention (Erreur classique)
>L'expression `attr = NULL` est incorrecte en SQL et ne renverra jamais le résultat attendu. Il faut obligatoirement utiliser `IS NULL`.

#### C. Mots-clés de tri et de restriction
* `DISTINCT` : Placé juste après `SELECT`, il élimine les doublons du résultat.
* `ORDER BY attr1 ASC | DESC` : Permet de trier les lignes selon un ou plusieurs attributs. Le tri est par défaut croissant (`ASC`).
* `LIMIT n` : ne renvoie que les `n` premiers enregistrements.
* `LIMIT n OFFSET p` : Renvoie `n` enregistrements après avoir ignoré (sauté) les `p` premiers du résultat.
* `COUNT(*)` : Fonction d'agrégation permettant de compter le nombre total d'enregistrements répondant aux critères.

>[!example]- Exemples de requêtes sur une table
>* **Sélection avec filtres cumulés :**
>  ```sql
>  SELECT * FROM pays WHERE population > 100e6 AND superficie > 1e6;
>  ```
>* **Projection avec calcul et renommage :**
>  ```sql
>  SELECT nom AS "Nom du Pays", population / superficie AS densite FROM pays;
>  ```
>* **Tri combiné avec restriction :**
>  ```sql
>  SELECT nom FROM pays ORDER BY population DESC LIMIT 5;
>  ```

---

### 3. Sous-requêtes (Requêtes imbriquées)
La table ou la valeur renvoyée par une requête peut être réutilisée directement à l'intérieur d'une autre requête selon 3 cas de figure :
1. **Comme une valeur unique :** Lorsque la sous-requête renvoie une table d'une seule ligne et d'une seule colonne.
2. **Comme une liste de valeurs :** Utilisée généralement avec l'opérateur de comparaison `IN`.
3. **Comme une table intermédiaire :** La sous-requête est placée directement dans la clause `FROM` pour agir comme une table virtuelle.

>[!example]- Exemples de sous-requêtes
>* **Sous-requête comme valeur unique :**
>  ```sql
>  SELECT nom FROM pays 
>  WHERE pib > (SELECT pib FROM pays WHERE nom = "Islande");
>  ```
>* **Sous-requête comme liste de valeurs (`IN`) :**
>  ```sql
>  SELECT nom FROM pays 
>  WHERE continent IN (SELECT continent FROM pays ORDER BY population DESC LIMIT 3);
>  ```
>* **Sous-requête après le FROM (table intermédiaire) :**
>  ```sql
>  SELECT nom, population 
>  FROM (SELECT nom, continent, population FROM pays WHERE population > 10e6)
>  WHERE continent = "Europe";
>  ```


#Informatique #Fiches 
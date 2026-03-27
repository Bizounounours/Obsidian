## I)<u>Structure de données de dictionnaire</u> :

>[!info] Définition 
>Un <u>dictionnaire</u> ou <u>tableau associatif</u>, permet de manipuler un ensemble d'associations.
>Une <u>association</u> est un lien entre un <u>clé</u> et une <u>valeur</u>.
>On peut se figurer une association comme une application d'un ensemble de clés vers un ensemble de valeurs.

>[!important] Remarque
>Les clés doivent être toutes distinctes, alors que les valeurs associées ne le sont pas nécessairement.

>[!info] <u>Interface</u>$^*$ pour la structure de données de dictionnaire
>>$^*$ : interface pour une structure de données : liste des fonctions et types définis pour cette structure de données
>>- <u>En C</u> : l'interface est donnée par le fichier $.h$
>>- <u>En OCaml</u> : l'interface est donnée par la description du module que l'on trouve en ligne (<u>ex</u>: module Array) On y trouve le nom du type et la liste de toutes les fonctions avec leur <u>spécifications</u> et leurs <u>signatures</u>
>
> - insertion d'un couple clé-valeur
> - recherche de la présence d'un clé
> - suppression d'un clé (et du coup de la valeur associée)
> - <u>éventuellement</u> : modification de la valeur associée à une clé
> 
> <u>Contrainte</u> :
>  ▪ toutes les clés doivent être de même type 
>  ▪ toutes les valeurs doivent être de même type
>  ▪ chaque clé doit être unique (les valeurs elles peuvent être présentes plusieurs fois)

>[!tip] Remarque
>On peut utiliser la structure de dictionnaire pour implémenter la structure de données d'ensemble$^*$ (dans ce cas, on associerait la même valeur à toutes les clés)
>>$^*$ : Précédemment on a implémenté la structure d'ensemble avec les ABR.

## II)<u>Réalisation avec un ABR</u> : (structure de données concrète) [^1]


>[!info] Info
>On stockera dans les nœuds la clé et la valeur associée mais les comparaisons ne se feront que sur la valeur des clés.
>> <u>Ex</u> : `type noeud = V | N of int * string` (clé) * (valeurs)
>
>>[!tip] <u>Cas particulier</u> :
>>Lorsque les clés sont des entiers positifs. On pourrait représenter le dictionnaire à l'aide d'un tableau.
>>
>>Si on connait la valeur maximale possible pour les clés, alors, la création du dictionnaire (via celle du tableau) se ferait en temps linéaire ($O(taille-max)$) et les opérations se feraient en temps constant.
>>Il faudrait convenir que si une clé n'existe pas, on lui associe dans le tableau une valeur non ambigüe, différente des valeurs autorisées, ou alors définir un second tableau dans lequel on indique par un tableau, par exemple que la clé existe ou non.

>[!example] Exemple
>dictionnaire associant aux codes ASCII des lettres de l'alphabet latin, la lettre (caractère) correspondant :
> - de $65$ à $65+26=90$ --> A;B;...;Z
> - de $97$ à $122$ --> a;b;...;z
> 

<u>Sous forme d'un tableau</u> : on aurait (par principe) la valeur maximale des entiers $127$ (ou 255 ASCII étendu)

| 0    | 1    | ... | 64   | 65       | ... | 90       | 91   | ... | 97       | ... | 122      | 123  | ... | 127 |
| ---- | ---- | --- | ---- | -------- | --- | -------- | ---- | --- | -------- | --- | -------- | ---- | --- | --- |
| None | None | ... | None | Some 'A' | ... | Some 'Z' | None | ... | Some 'a' | ... | Some 'z' | None | ... | ... |
ou bien 2$^e$ façon :

|      | 0     | 1     | ...   | 64   | 65  | ...  | 90   | ... |
| ---- | ----- | ----- | ----- | ---- | --- | ---- | ---- | --- |
| tab1 | '  '  | '  '  | ...   | '  ' | 'A' | ...  | 'Z'  | etc |
| tab2 | 0     | 1     | ...   | 64   | 65  | ...  | 90   | ... |
|      | False | False | False | True | ... | True | True | etc |
>[!note] Complexité des opérations élémentaires
> - recherche si une clé est présente : $O(1)$ , on teste si `tab1.(i)` vaut `None` ou non, ou si `tab2.(i)`  vaut $false$ ou $true$
> - ajouter un couple clé, valeur $(i,v)$ ou modifier une valeur : `tab.(i) <- v`, ou `tab2.(i) <- true` et `tab1.(i) <- v`
> - suppression d'une clé $i$ (et par suite de la valeur associée) : `tab.(i) <- None` ou bien `tab2.(i) <- false` (la modification de `tab1.(i)` n'est pas absolument nécessaire)

>[!warning] Inconvénients 
> 1. les clés doivent être entières
> 2. complexité spatiale potentiellement mauvaise (si beaucoup de clés ne sont pas utilisées entre $0$ et $taille-1$)

## III)<u>Implémentation avec une table de hachage</u> [^2]

>[!note] Info
>Une table de hachage permet de stocker un dictionnaire sous la forme d'un tableau, sans condition sur le type des clés
>
>>[!info] Idée
>>On dispose d'une fonction (fonction de hachage) qui associe à toute clé un entier qui permet de désigner une cellule du tableau où on stockera la valeur associée.
>
>Si l'ensemble des clés est $A$, et si on utilise un tableau de taille $N$ on doit disposer d'une fonction de hachage $h : K \to [\![0, N-1]\!]$ avec $A \subset K$ 
>Pour traiter une clé $k$, on calcule $h(k)$ (le "haché" de $k$) et on place la valeur $\theta$ associé à $k$ dans l'<font color = "red">alvéole</font> d'indice $h(k)$ (cellule d'indice $h(k)$ du tableau).
>Idéalement, on souhaite que la valeur $h(k)$ se calcule en temps constant.

>[!danger] Problème :
><u>le nombre</u> de valeur possibles pour <u>les clés</u> est potentiellement infini (ou très grand) tandis que le tableau où on stocke les valeurs est de taille fixe $N$. D'où le fait que la fonction $h$ ne pourra globalement pas être injective.
>C'est-à-dire qu'il existera des clés dont le haché sera le même càd 
>> $h(k) = h(k')$ avec $k \not = k'$
>> haché égaux mais clé distinctes
>
>Lorsque Cette situation se présente on parle d'une <u>collision</u>
### 1)<u>Gestion des collisions par chaînage</u> : [^3]

>[!info] Idée
>Dans chaque alvéole on placera les couples $(clé,valeur)$ $(k,v)$ pour lesquels le haché de $k$ est le même, dans une liste chaînée.

>[!note] Note 
>Le fait d'utiliser une liste chaînée permet (par rapport à l'utilisation d'un sous-tableau) de ne pas avoir à réserver de l'espace mémoire "par avance".

>[!example] Exemple
>clés, valeur : $k_{1}$ $k_{2}$ $k_{3}$ $k_{4}$ $k_{5}$ $k_{6}$ $k_{7}$ $k_{8}$ $k_{9}$ 
>haché : $3,1,4,1,4,5,8,2,6$
><u>Si N = 10</u> :
>
|     | 0            | 1                               | 2                 | 3                 | 4                           | 5                 | 6                 | 7            | 8                 | 9            |
| --- | ------------ | ------------------------------- | ----------------- | ----------------- | --------------------------- | ----------------- | ----------------- | ------------ | ----------------- | ------------ |
| tab | $[\text{ }]$ | $[(k_{4},v_{4});(k_{2},v_{2})]$ | $[(k_{8},v_{8})]$ | $[(k_{1},v_{1})]$ | $[(k_{5},v_{5});(k_{3},3)]$ | $[(k_{6},v_{6})]$ | $[(k_{9},v_{9})]$ | $[\text{ }]$ | $[(k_{7},v_{7})]$ | $[\text{ }]$ |
>
>$v_{i}$ valeur associée a $k_{i}$

>[!tip] Complexité des opérations
> - Recherche de la présence d'un clé : 
> -  - on calcule le haché de la clé $h(k)$ -> $O(1)$ 
> -  - on parcourt la liste chaînée présente dans l'alvéole -> $O(n_{h(k)})$
> - Insertion d'un couple $(clé,valeur)$ (ou modification d'une valeur) :
> -  - $O(1)$ sauf si on doit s'assurer que la clé n'est pas déjà présente
> -  - $O(n_{h(k)})$ si on doit vérifier que la clé n'est pas déjà présente (dans le cas d'un ajout)
> -  - $O(n_{h(k)})$  pour une modification (il faut trouver le couple dans la liste pour le modifier soit pour le supprimer et le remplacer)
> - Suppression d'une clé :
> -  - $O(n_{h(k)})$ (parcourir la liste pour atteindre le couple)
> 
>>[!failure] Pire cas 
>>$O(n)$ : si tous les couples sont dans la même alvéole

>[!info] Définition
>Le facteur de remplissage $\alpha$ d'une table de hachage possédant $N$ alvéoles et contenant $n$ couples $(clé,valeur)$ est la longueur moyenne des listes chaînées : $\alpha = n / N$
>$n \to \text{nbr de clés (couples clés-valeurs)}$
>$N \to \text{nbr d'alvéoles}$

>[!tip] Complexité des opérations (compléments)
> - complexité de la recherche/modification :
> 	$$O(1) + O(n_{h(k)}) =^\text{en moy} O(1) + O(\alpha) = O(\alpha)$$
> 	On a utilisé que, en <u>moyenne (hypothèse de travail</u>[^4])
> 	On s'efforce donc d'avoir $\frac{\alpha}{N}$ proche de 1 quel que soient n et N, et donc, on prendra un nombre d'alvéolees de l'ordre de n. (ce qui ne dispense pas de l'hypothèse[^4])


### 2)<u>Gestion des collisions par sondage</u> : ("à adressage ouvert")

>[!tip] Remarqe
>"adressage fermé" signifie qe l'adresse (le n° de l'alvéole contenant la clé) est complètement déterminé par la valeur de $h(k)$ ce qui ne sera plus le cas ici.

>[!info] info
>On présente ici la méthode du sondage "linéaire" :
> - on calcule le $h(k)$
> - si l'alvéole $h(k)$ est déjà occupée, alors on recherche la première alvéole libre, à droite de la position occupée. On teste donc les positions $h(k)+i$[^5] en choisisant le plus petit $i\geq 0$ tel que l'alvéole d'indice $h(k)+i$ est libre

>[!example] Exemple 
> nombre d'alvéoles : $N = 10$
>
| $k(clé)$ | $k0$ | $k1$ | $k2$ | $k3$ | $k4$ | $k5$ | $k6$ | $k7$ | $k8$ |
| -------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| $h(k)$   | 3    | 1    | 4    | 1    | 4    | 5    | 8    | 2    | 6    |
>
> - <u>Insertion des clés au fur et à mesure</u> :
>table de hachage
>
| 0   | 1          | 2          | 3          | 4          | 5          | 6          | 7          | 8          | 9          |
| --- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
|     | $k_{1}(1)$ | $k_{3}(1)$ | $k_{0}(3)$ | $k_{2}(4)$ | $k_{5}(5)$ | $k_{5}(5)$ | $k_{7}(2)$ | $k_{6}(8)$ | $k_{8}(6)$ |

>[!info] <u>recherche d'une clé k</u> :
> on calcule le haché de $k$ 
> <u>Sur notre exemple</u> : 
>  ▪ si $h(k) = 0$, on constate que l'alvéole est vide donc la clé $k$ est absente.
>  ▪ si $h(k) = 3$ (par exemple) : on constate que l'alvéole n°3 est occupée, donc on doit comparer $k$ à la clé situées dans l'alvéole 3 si en position 3 on a $k' \not = k$, il faut tester toutes les alvéoles situées à droite : 
> 	  - si l'alvéole est occupée, on compare la clé présente $k'$ à $k$ si $k' = k$ : la clé est présente, sinon on poursuit
> 	  - si l'alvéole est libre, on s'arrête : la clé $k$ est absente.
>
> Ainsi deux problème se posent :
>  1. on peut avoir comme dans l'exemple des "grumeaux" de clés càd un agrégat d'alvéole consécutive occupées. Ce qui augmente la complexité de la recherche d'une clé absente (car la recherche ne s'arrête qui si <font color = "red">l'on arrive</font> sur une  vide)
>  2. Lorsque l'on supprime une clé (càd un couple $(clé,valeur)$) clea peut créer un trou dans ce était une agrégat. 
>  <u>sur l'exemple</u> : si on supprime $k_{0}$ (qui est en position 3) et qu'ensuite on recherche la présence de $k_{7}$ dont le haché est 2 : on examinera l'alvéole 2 occupée (par la clé $k_{2} \not= k_{7}$), puis l'alvéole 3 vide et on concluera que $k_{7}$ est absente, ce qui est <font color = "red">faux</font>.
>
>Ainsi, lors d'une suppression, on devra convenir d'une trace à laisser pour exprimer que l'alvéole à été occupée. (par exemple une valeur $\not=$ des valeurs possibles pour les clés et $\not=$ de la valeur des cases vides).

>[!note] N.B
>Avec cette méthode, on doit avoir $n < N$ ($\text{nbr clés} < \text{nbr alvéoles}$) (on agrandit le tableau si cela arrive)
>>nécessité d'une case vide pour que toute recherche termine

### 3)<u>Choix de la fonction de hachage</u> :

>[!info] Info 
>On attend de la fonction de hachage que : 
> - elle se calcule rapidement (complexité constante[^6]);
> - suite à l'ordre des caractères (si les clés sont des chaînes)[^8];
> - distribution de valeur uniforme[^7];
>   

>[!info] Info 
>Si les clés sont des chaînes, on a choisit usuellement une fonction de la forme :
>$h : c_{0}c_{1}\dots c_{l-1} \to (\sum^{l-1}_{i =0 }code(c_{i})A^i) \mod N$[^9]
>où A est un entier fixé (généralement premier, souvent égal à 31 pour que $h$ ait de bonnes propriétés)

>[!tip] Remarque 
>Pour $A = 31$ et $N = 10000$ on a $<10$ colliq=sion sur l'ensemble des mots du dictionnaire français.
>

 >[!info] Calcul de $h(k)$ :
 > - on fera attention aux éventuels dépassements de capacité et si $h(k) < 0$ on changera le signe (pour que $h(k) \in [|0,N-1|]$ soit une position valide)
 > - on calculera la valeur du polynôme avec l'algorithme de Hörner (qui calcule $h(c_{0}c_{1}\dots c_{l})$ en $O(l)$) ($l$ le degré du polynôme)

## IV)<u>Module Hashtabl</u> (Ocaml)

>[!note] interface
>`Hashtabl.create n` : pour créer une table de capacité donnée.
>`Hashtabl.add t k v` : ajoute la clé `k` associée à la valeur `v`.
>`Hashtabl.remove t k` : supprime la clé `k` (et `v` associée) dans la table `t`
>`Hashtabl.mem t k` : renvoie un booléen (true si la clé `k` est présente)
>`Hashtabl.find t k` : renvoie la valeur associé à `k` (erreur si `k` absente)
>`Hashtabl.find-opt t k` : comme `find` mais renvoie `None` si `k` absente et la valeur sinon (`Some v`)
>`Hashtabl.iter f t` : applique `f` à tous les couples clé, valeur de `t` et renvoie `unit` (`f` renvoie des valeurs `unit`, agit par effet)





[^1]: réalisation de la structure de données abstraite

[^2]: hashtable

[^3]: ou "adressage fermé"

[^4]: l'hypothèse est que la fonction de hachage prend des valeurs <font color = "red">h(k) </font> uniformément réparties dans $[|0,N-1|]$ lorsque $k$ parcourt l'ensemble des clés.

[^5]: en vérité $h(k)+i$ <font color = "red"> mod N</font> (au cas où $h(k)+i\geq N$)

[^6]: comme pour les fonctions mathématiques $\cos$,$\exp$,...

[^7]: ensemble des clés $A \subset K$
$h : K \to [|0,N-1 |]$ avec $N$ le nombre d'alvéole
$\forall m \in h(A) \subset [|0,N-1|]$, les valeurs de P$(c=m)$ pour toute clé c doivent être de même type. 

[^8]: si les clés ont des chaînes et que $h(k)$ ne dépend pas de l'ordre des caractères, les valeurs de $h(k)$ ne seront pas assez diversifiées

[^9]: entier modulo $N$ 
	(entier % N en C 
	entier mod $N$ en OCaml
	reste dans la division euclidienne par $N$ )

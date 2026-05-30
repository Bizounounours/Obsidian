>[!cour]
>On discute ici de différente possibilités (approches) pour concevoir un algorithme pour résoudre un problème donné

# I)<u>Force brute</u> :

>[!cour] 
>Cette démarche (la plus élémentaire) consiste à tester toutes les solutions envisageables de problème.
>Ce qui suppose que : 
> - il est possible de parcourir l'ensemble des solutions envisageables (candidats)
> - il est possible de tester si un candidat est solution

>[!example] 
>Au sudoku on peut tester $9^{81}$ candidats (autour de candidats que d'éléments dans $[\![1;9]\!]^{81}$, on teste tous les 81-uplets à valeurs dans $[\![1;9]\!]$)
>
>>[!warning] La complexité est souvent exponentielle et la résolution par cette méthode irréaliste
>
>Généralement on s'arrête à la $1^{ère}$ solution trouvée, en utilisant un break (C) ou une exception (OCaml)

# II)<u>Retour sur trace</u> : (backtracking)

>[!cour]
>On cherche à construire la solution de proche en proche en revenant en arrière à chaque fois que l'on arrive à une impasse.
>On revient en arrière, juste suffisamment pour pouvoir tester d'autres options.
>On peut se figurer la recherche au travers d'un arbre.
>comme dans l'exemple suivant.

>[!example] Problèmes de 8 reines (ici 4 reines)
>On cherche à placer 4 reine sur un plateau de 16 cases de sorte qu'aucune n'en menace une autre :

>[!note] N.B
>Pour qu'elles ne se menace pas l'une l'autre, il ne peut y en avoir qu'une par ligne 

# III)<u>Algorithmes gloutons</u> :

>[!cour]
>On peut rechercher une solution à un problème avec un algorithme glouton lorsqu'il s'agit d'un problème d'optimisation, dans lequel des choix doivent être fait afin de maximiser/minimiser une certaine quantité sans certaines contraintes.
>
>Mettre en place un algorithme glouton constera à se donner une ou des règles pour faire ces choix : 
> - les uns après les autres
> - sans jamais les remettre en cause et en essayant que chacun de ces choix soit le meilleur possible au moment où il est fait.

>[!example] Exemple 1 : sac à dos
>On dispose de $n$ objets avec un poids (masse) et une valeur (€)
>
>
|i | objet | Masse | Valeur (€) |
| ---- | ----- | ----- | ---------- |
| 1  | A     | 9     | 10         |
| 2  | B     | 12    | 7          |
| 3  | C     | 2     | 1          |
| 4  | D     | 7     | 3          |
| 5  | E     | 5     | 2          |
>
>On veut remplir un sac à dos de capacité maximale $C=15kg$ de sorte à maximiser la valeur des objets dans le sac.
>
><u>Problème à résoudre</u>:
>On a $n$ objets caractérisés chacun par un couple $\underbrace{(p_{i},v_{i})}_{(poids(kg),valeur(\text{€}))}$
>Et un sac de capacité $C(kg)$
>On veut maximiser $\underbrace{V=\sum^{m}_{k=1} v_{i_{k}}}_{\text{valeur totale}}$ sous la contrainte $\underbrace{\sum^{m}_{k=1}p_{i_{k}} \leq C}_{\text{masse totale }\leq C}$ par le choix de $m$ objets d'indices $(i_{1},i_{2},i_{3},\dots,i_{m})$ parmis les $n$ objets disponibles.
>
>**Résolution en force brute :**
>Il y a $n+1$ valeurs possibles pour $m$ ($m \in [\![0;n]\!]$)  et $m$ étant choisi, $\binom{n}{m}$ choix possible d'objets.
>Soit, au total, $\sum^{n}_{m=0}\binom{n}{m} = 2^k$ choix envisageables.
>
>**Résolution exacte :** programmation dynamique :
>choix de l'objet 1 :
>``` mermaid
>graph TD;
>id0((_)) --> id1((oui))
>id0((_)) --> id2((non))
>```
> - <u>si oui</u>[^1] rechercher le meilleur choix (si on a pris l'objet 1) 
>   $$\boxed{\text{maximiser somme +}v_{1}\text{ des valeurs, sous la Contrainte : }\text{somme des poids }\leq C-p_{1}}$$
> - <u>si non</u> rechercher le meilleur choix (si on n'a pas pris l'objet 1)
> $$\boxed{\text{pb inchangé à résoudre avec n-1 autres objets}}$$
> 
> *On compare les réponses et cela indiquera si l'on doit prendre ou non l'objet 1*
> 
> On aura a priori encore un arbre avec $2^n$ nœuds à explorer mais la programmation dynamique pourra nous économiser des calculs.
> 
> **Stratégie gloutonne :** 
> On a $n$ choix à faire (choisir ou non l'objet $i$)
> On se donne une stratégie de choix de l'objet $i$.
>  - <u>possibilité 1</u> : choisir toujours l'objet restant de plus grande valeur possible.
>  - <u>possibilité 2</u> : choisir toujours l'objet restant de poids minimal.
>  - <u>possibilité 3</u> : choisir toujours l'objet restant de plus grand rapport $\frac{v_{i}}{p_{i}}$ (valeur massique).
>
><u>Stratégie 1</u> : par val décroissante :
>
|              | A   | B   | C   | D   | E    |
| ------------ | --- | --- | --- | --- | ---- |
| $v_{i}$      | 10  | 7   | 3   | 2   | 1    |
| $p_{i}$      | 9   | 12  | 7   | 5   | 2    |
| poids cumulé | 9   | 21  | 16 | 14 | 16 |
>
>On choisit {A,E} 
>poids total : 14 kg
>valeur totale : 12 €
>
><u>Stratégie 2</u> : par poids croissant
>
|              | C   | E   | D   | A   | B    |
| ------------ | --- | --- | --- | --- | ---- |
| $p_{i}$      | 2   | 5   | 7   | 9   | 12   |
| $v_{i}$      | 1   | 2   | 3   | 10  | 7    |
| poids cumulé | 2   | 7   | 14  | 14+9 | 14+12 |
>
>On choisit {C,E,D} 
>poids total : 14 kg
>valeur totale : 6 €
>
><u>Stratégie 3</u> : par rapport $\frac{v_{i}}{p_{i}}$ décroissant
>
|                              | A    | B    | C   | D    | E    |
| ---------------------------- | ---- | ---- | --- | ---- | ---- |
| $\frac{v_{i}}{p_{i}}$ (€/kg) | 1.11 | 0.58 | 0.5 | 0.43 | 0.4  |
| $v_{i}$                      | 10   | 7    | 1   | 3    | 2    |
| $p_{i}$                      | 9    | 12   | 2   | 7    | 5    |
| poids cumulé                 | 9    | 21  | 9+2  = 11| 11 + 7 = 18  | 11 + 5  = 16 |
>
>On choisit {A,C} 
>poids total : 11 kg
>valeur totale : 11 €
>
><u>Analyse</u> : pour chacune des stratégies, la complexité est en : 
>$$\underbrace{O(n\log(n))}_{\text{tri préalable}}+ \underbrace{O(n)}_{\text{parcours de la liste des objets avec tests et choix}}$$
>
>On a "échappé" à une complexité exponentielle mais on n'a pas l'assurance d'obtenir la solution exacte.
>
>>[!note] N.B
>>Il faudra au cas par cas, examiner si la stratégie assure de trouver la meilleur solution (solution exacte) ou pas.
>>
>>On cherche souvent un compromis entre gain de complexité et qualité de l'approximation de la solution 

>[!example] Exemples classiques :
> - <u>Rendu de monnaie</u> : un ensemble ce valeurs de pièces ou de billets étant donné, avec des pièces et billets en quantités illimitées
>   trouver le nombre minimal de pièces ou billets pour rendre une somme $S$ en monnaie
>   - *stratégie gloutonne* : choisir toujours la pièce/billet de plus grande valeur pour rendre la monnaie restante:
>   - *Info* : cette stratégie donne l'optimum mais seulement pour crains ensemble de valeurs de billets (dont le système €, mais pas l'ancien système £).
>
>>[!important] Remarque 
>Si on considère l'ensemble des valeurs des pièces déjà trié, la complexité est en $O(S)$ 
>$S$ la somme à rendre (plus précisément $O(S)$ divisé par la plus petite valeur de pièce)
>
> - <u>planification d'évènements</u> : 
>   On considère un ensemble d'évènements, chacun caractérisé par une date de début et une date de fin, ($d_{i},f_{i}$), se déroulant sur une période donnée. 
>   Et on souhaite assister à un maximum d'entre eux.
>   On peut envisager plusieurs stratégie gloutonnes :
>   - *choisir en priorité l'évènement de durée la plus courte*[^2] (sans réserve de compatibilité avec les choix précédents)
>   ou bien
>    - *choisir en priorité l'évènement de début le plus proche*[^3] (sans réserve de compatibilité avec les choix précédents)
>    ou bien
>    - *choisir en priorité l'évènement de fin la plus proche*[^4] (sans réserve de compatibilité avec les choix précédents)
>    
>    <font color ="red">On peut montrer que la dernière stratégie donne toujours l'optimum</font>
>
>>[!important] Remarque
>>complexité en $\underbrace{O(n\log (n))}_{Tri}+ \underbrace{O(n)}_{choix} = O(n\log(n))$ avec $n$ le nombre d'évènements

# IV)<u>Diviser pour régner</u> :

### 1)<u>Principe</u> :

>[!cour]
> - On décompose le problème à résoudre en sous-problèmes <font color="red">indépendants</font>, de plus petite taille.
> - On résout les sous-problèmes récursivement
> - On combine les solutions des sous problèmes pour obtenir la solution du problème initial.

### 2)<u>Exemples</u> :

>[!cour] Tri fusion
> - on décompose la liste ou le tableau en 2
> - on trie les 2 parties récursivement
> - on fusionne/interclasse les 2 sous-listes/sous-tableaux triés 

>[!cour] Tri fusion
> - On choisit un pivot, on sépare en plus petits et plus grands
> - On trie récursivement plus petits et plus grands
> - On juxtapose petits triés, pivots, grands triés

>[!cour] Recherche dichotomique dans une liste triée
>>[!warning] Cas particulier
>
>- viser le milieu de la liste (terminer si valeur trouvée)
>- séparer la liste triée en 2 parties (> et < à la valeur du milieu) poursuivre la recherche <font color="red">dans l'une des 2 sous-listes <u>(cas particulier)</u></font>
>- renvoyer l'indice où se trouve la valeur dans la sous-liste) <u>ou</u> true/false
# V)<u>Programmation dynamique</u>

### 1)<u>Principe</u> :

>[!cour]
>On décompose le problème en sous-problèmes
>On résout les sous-problèmes mais en veillant à ne pas résoudre plusieurs fois le même sous-problème (les sous-problèmes ne sont pas a priori indépendants)
>On résout le problème d'origine à partir des solutions des sous-problèmes grâce à une relation de récurrence liant la solution du problème aux solutions du sous-problèmes. 
>
>Ce principe se met en place de deux façon possibles :
> - <u>méthode de haut en bas</u> : TOP-DOWN (*méthode descendante*)
>   On résout le problème récursivement et on stocke chaque solution de sous-problème trouvée dans un dictionnaire ou un tableau.
>
>- <u>méthode de bas en haut</u> : BOTTOM - UP (*méthode ascendante*)
>  On résout tous les problème de plus petite taille.
>  Puis de proche en proche tout les problèmes de taille croissante, jusqu'au problème d'origine.

>[!example] Calcul du terme de rang $n$ de la suite de Fibonacci
>>[!note] Rappel
>>$F_{0} = 0$
>>$F_{1} = 1$
>>$\forall n \geq 2, F_{n} = F_{n-1} + F_{n-2}$
>
><u>Résolution</u> :
>``` mermaid
>graph TD
>id0(F4) --> id1((F2))
>id0(F4) --> id2((F3))
>id1((F2)) -->  id3((F0))
>id1((F2)) --> id4((F1))
>id2((F3)) --> id5((F1))
>id2((F3)) --> id6((F2))
>id6((F2)) --> id7((F0))
>id6((F2)) --> id8((F1))
>```
>
>> carré => sous-problèmes
>> <u>Mauvais</u> : $F_{2}$ résolut 2 fois
>
><u>Solution récursive</u>
>``` C
>int fibo(int n){
>	if (n <= 1) return n;
>	int a = fibo(n-1);
>	int b = fibo(n-2);
>	return a+b;
>}
>```
> - <u>méthode</u> : TOP-DOWN
>   On se donne un tableau de tableau de taille *$N$ (le plus grand $n$ par lequel on veut calculer fibo)* passé en paramètre
>   à chaque fois que l'on doit calculer un fibo(n)
>   - On examine si sa valeur est déjà dans le tableau.
>      - si on la renvoie
>      - sinon on la calcule et on l'inscrit dans le tableau
>
> - <u>méthode</u> : BOTTOM-UP 
>   On remplit le tableau directement de la case 0 à la case $N$ avec la relation de récurrence




[^1]: possible si $p_{1}\leq C$

[^2]: classer par $(f_{i}-d_{i})$ croissants

[^3]: classer par $d_{i}$ croissants

[^4]: classer par $f_{i}$ croissants
---
#Informatique #cours
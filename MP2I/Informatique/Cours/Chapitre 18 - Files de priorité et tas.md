# I)<u>Tas</u> :

### 1)<u>Définition</u> : tas min

>[!note] Définition
>Un tas min est un arbre binaire complet à gauche tel que l'étiquette de tout nœud interne est inférieure (ou égale) à celle de ses fils

>[!tip] <u>Remarque</u>
>on définit de même les tas_max

>[!example] Exemple 
>```mermaid
>graph TD
>id1((1)) --> id2((2))
>id1((1)) --> id3((3))
>id2((2)) --> id4((17))
>id2((2)) --> id5((19))
>id3((3)) --> id6((36))
>id3((3)) --> id7((7))
>id4((17)) --> id8((25))
>id4((17)) --> id9((100))
>```

>[!info] Info
>On a donc la possibilité de le représenter en stockant son parcours en largeur dans un tableau.

| 0   | 1          | ... | i      | ... | 2i      | 2i + 1  |
| --- | ---------- | --- | ------ | --- | ------- | ------- |
|     | r (racine) |     | $\phi$ |     | $f_{g}$ | $f_{d}$ |
>[!info] Info (Suite)
>Pour aller de 2i à i :
>$\lfloor \frac{i}{2} \rfloor$ ou $\frac{i}{2}$ quotient dans la division euclidienne par deux

>[!note] Implémentation en C 
>``` C
>struct tas {
>	int* tab; //la case d'indice 0 contiendra la taille du tableau (nombre de cases occupées)
>	int capacity;  // nombre de cellules occupées ou non
>}
>
>int fils_gauche (int i){
>	return 2*i
>}
>
>int pere (int i){
>	return i/2
>}
>
>void swap (struct tas t, int i, int j){
>	int temp = t.tab[i];
>	t.tab[i] = t.tab[j];
>	t.tab[j] = temp;
>}
>```

# II)<u>Opération sur le tas min</u> :

### 1)<u>UP</u> :

>[!note] <u>N.B</u> 
>Dans un tas min, en tout nœud les sous-arbres g et d sont des tas_min.

>[!info] info
>On va s'intéresser à 2 opérations :
> - `void up (struct tas t, int i)` qui, 
> 	 || dans le cas où `t` est un tas min sauf éventuellement au nœud i où l'étiquette `t.tab[i]` peut être inférieure à celle du père. ||
> va rétablir la structure de tas
> 	<u>ou/autre version</u>
> 	|| Rétablis la propriété de tas min dans l'hypothèse où `t` est un tas min sauf éventuellement `t.tab[i]` qui peut être inférieur à son père. (à ceci près que la structure de tas min doit être respectée càd, pour tout nœud du tas, tous les nœuds de ses sous-arbres ont une étiquette supérieure ou égale à celle du nœud ) ||

>[!tip] Rappel 
>``` C
>struct tas {
>	int* tab; //valeurs dans le tas
>	int capacity; //nb de cases alloués
>}
>```

<u>t.tab</u> :

| i        | 0                                        | 1             | 2   | ... | ... | ... | ... | ... | ... | t   |              |
| -------- | ---------------------------------------- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | ------------ |
| t.tab[i] | taille (càd le nb de nœuds dans l'arbre) | 1<br>(racine) | 2   | 3   | 17  | 19  | 36  | 7   | 25  | 100 | non remplies |

>[!info] Code de void up :
>``` C
>void up (struct tas t, int i){
>	int p = pere(i);
>	while (p > 0 && t.tab[p] > t.tab[i]){ //p > 0 : 1 /t.tab[p] > t.tab[i] : 2
>		swap(t, i, p);
>		i = p;              // i = p : 3 
>		p = pere(i);        // p = pere(i) : 3
>	}
>}
>```
>
> 1 : Vérifier que `i` n'est pas à la racine
> 2 : On vérifie s'il faut inverser père et fils
> 3 : préparation de l'itération suivante (éventuelle)

>[!important] Complexité 
>Le nombre d'itérations est au plus égal à la profondeur du nœud `i`.
>Donc la complexité est en $\log_{2}(i)^*$ (majoré par $O(h)$).
>>[!note] $*$
>>``` mermaid
>>graph TD
>>id1((1)) --> id2((2))
>>id1((1)) --> id3((3))
>>id2((2)) --> id4(( ))
>>id2((2)) --> id5((i))
>>id3((3)) --> id6(( ))
>>id3((3)) --> id7(( ))
>>```
>>la tableau de l'indice `i` correspond à des nœuds formant un arbre complet qui comporte `i` nœuds, et donc (propriété du cours) la hauteur de cet arbre càd la profondeur de `i` vaut $\lfloor \log_{2}(i) \rfloor$

>[!example] Exemple d'ajout
>```mermaid
>graph TD
>id1((1)) --> id2((5))
>id1((1)) --> id3((3))
>id2((5)) --> id4((17))
>id2((5)) --> id5((20))
>id3((3)) --> id6((36))
>id3((3)) --> id7((7))
>id4((17)) --> id8((4))
>id4((17)) --> id9((100))
>id5((20)) --> id10((30))
>id5((20)) --> id11((25))
>id6((36)) --> id12((40))
>id6((36)) --> id13((38))
>id7((7)) --> id14((9))
>id7((7)) --> id15((16))
>id8((4)) --> id16((18))
>id8((4)) --> id17((25))
>id9((100)) --> id18((110))
>```
>
>On a rajouter 18, 25 et 110
>respectivement supérieurs à leur pères afin de conserver la structure de tas.

### 2)<u>Down</u> :

>[!info] Info (suite) [[Chapitre 18 - Files de priorité et tas#II)<u>Opération sur le tas min</u>| lien]]
>`void down (struct tas t, int i)` 
>||Rétablit la propriété de tas min dans l'hypothèse où `t` est un tas min sauf éventuellement au nœud `i`, qui peut être supérieur à l'un de ses fils.
>
>``` mermaid
>graph TD
>id1((1)) --> id2((110))
>id1((1)) --> id3((3))
>id2((110)) --> id4((17))
>id2((110)) --> id5((19))
>id3((3)) --> id6((36))
>id3((3)) --> id7((7))
>id4((17)) --> id8((25))
>id4((17)) --> id9((100))
>```
> /////////////////////////////////////////////////////////////////////////////////////////////////////
>``` mermaid
>graph TD
>id110((110)) --> idtg((tg))
>id110((110)) --> idtd((td))
>```
>
>Si ce cas advient on va descendre d'un niveau la valeur en `i` mais en échangeant avec le fils le plus petit
>Si on remplace 19 (racine de $t_{d}$) par 110 le nouveau sous-arbre droit $t_{d'}$ sera un tas min si on itère le procédé et qu'il est correct (hypothèse d'induction)
> - cas n°1 : où 110 n'est pas le fils de 19
> - cas n°2 : cas complémentaire du cas n°1
> 
>>[!info] Cas n°2
>>```mermaid
>>graph TD
>>id2((19)) --> id4((17))
>>id2((19)) --> id5((110))
>>id4((17)) --> id8((25))
>>id4((17)) --> id9((100))
>>```
>>On a un problème avec le fils gauche car $19>17$.
>>On n'a pas avancé : en position `i` où il y avait $110$, on a encore une valeur supérieur à l'un des fils
>>
>>La bonne  méthode est d'**échanger avec le plus petit des deux fils**
>>
>>``` mermaid
>>graph TD
>>id1((1)) --> id2((110))
>>id1((1)) --> id3((3))
>>id2((110)) --> id4((17))
>>id2((110)) --> id5((19))
>>id3((3)) --> id6((36))
>>id3((3)) --> id7((7))
>>id4((17)) --> id8((25))
>>id4((17)) --> id9((100))
>>```
>>Puis :
>>``` mermaid
>>graph TD
>>id1((1)) --> id2((*17*))
>>id1((1)) --> id3((3))
>>id2((*17*)) --> id4((*110*))
>>id2((*17*)) --> id5((19))
>>id3((3)) --> id6((36))
>>id3((3)) --> id7((7))
>>id4((*110*)) --> id8((25))
>>id4((*110*)) --> id9((100))
>>```
>>on a donc :
>>$$\begin{align} r = 110 \\ r_{g} = 17 \\ r_{d} = 19 \end{align}$$ 
>>puis,
>>$$\begin{align} r' = 17 \\ r_{g}' = 110 \\ r_{d}' = 19 \end{align}$$ 
>>
>>comme on a choisi $17 = \min(r_{g},r_{d}) = r_{g}$
>>on a l'assurance que $r' \geq r_{d}' = r_{d}$*
>>On a donc l'assurance qu'il n'y a pas de problème à droite.
>>et à gauche : pas de problème (vérifier si $r_{g}' \leq \text{ses fils}$)
>>ou le problème se règle par un nouvel appel à down

>[!note] Code de void down
>``` C
>void down (struct tas t, int i){
>	int taille = t.tab[0];
>	while (i <= taille){  // si i est bien l'indice d'un noeud existant
>		int gauche = fils_gauche(i);
>		int droite = fils_droite(i);
>		int minIndex = i; //indice du plus petit entre i,fg,fd initialisation.
>		//si le fils gauche existe et est plus petit que le plus petit déjà
>		//trouvé (ici i)
>		if (gauche <= taille && t.tab[gauche]<t.tab[minIndex]){
>			minIndex = gauche;
>		}
>		// idem à droite
>		if (droit <= taille && t.tab[droit] < t.tab[minIndex]){
>			minIndex = droit;
>		}
>		// si le plus petit est à la racine : on arrête
>		if (minIndex == i) return ;
>		// sinon on échange i avec le plus petit.
>		swap(t, i, minIndex);
>		//préparation de l'itération suivante (suite éventuelle de la descente)
>		i = minIndex;
>	}
>}
>```

### 3)<u>Extraire le min</u> :

>[!note] Principe 
> - le min est à prendre à la racine
> - on rétablit le tas en plaçant à la racine la dernière feuille (pour être dans un cas d'application de down)
>```C
>int extraire_min (struct tas t){
>	int taille = t.tab[0];
>	int min = t.tab[1];
>	t.tab[1] = t.tab[taille];
>	t.tab[0] = taille - 1;
>	down(t,1);
>	return min;
>}
>```

### 4)<u>Ajouter un élément</u> :

>[!info] Def/info
>On ajoute en dernière position ($\text{taille} + 1$) (préserve la structure d'arbre complet)
>On applique `up` (préserver la structure de tas)
>Actualiser la taille càd `t.tab[0]` (* ajouter 1)

### 5)<u>Mettre à jour un élément</u> :

>[!info] Def/info
><u>Càd</u> changer la valeur en position `i` 
>On change la valeur : 
> - si la nouvelle valeur est plus grande : on appelle `down`.
> - si la nouvelle valeur est plus petite : on appelle `up`.


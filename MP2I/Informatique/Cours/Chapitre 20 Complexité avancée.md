# I)<u>Complexité en moyenne</u> :

>[!note] Définition
>Soit $E$ l'ensemble des entiers possibles pour un algorithme $A$
>Si $c(e)$ désigne le nombre d'opération exécutées par $A$ pour $e \in E$,
>alors on appelle complexité en moyenne de $A$ l'application : 
>$$ C_{m} : \cases{\begin{align} & \mathbb{N} \to \mathbb{R}_{+}  \\
>  & n \to \sum_{e \in E, e\text{ de taille n}} c(e)
\end{align}}$$
>> ${e \in E | e \text{ de taille n}}$
>> <font color = "red">pour chaque taille possible d'instance en calcule la moyenne des complexités c(e)</font>

### 1)<u>Exemple 1</u> : recherche dans un tableau de booléens

>[!bug] Code / exemple
>``` C
>bool contient_true (bool* tab, int n){
>	for (int i = 0; i < n; i++){
>		if (tab[i]) return true
>	}
>	return false;
>}
>```
>$E$ : ensemble des tableaux de booléens || taille d'une instance : taille du tableau
>$A$ : l'algorithme renvoie un booléen indiquant si le tableau contient au moins 1 valeur True
>complexité dans le pire cas [^1] : $O(n)$ (si aucun true dans le tableau ou si true est en dernière position)
>complexité dans le meilleur cas [^1] : $O(1)$ (si $tab[0]$ vaut true)
>>[!note] <u>Complexité en moyenne</u>
>>Pou run certain $n$, la complexité $c(e)$, pour en entrée $e$ prend (à une constante près) une valeur entre $1$ et $n$, selon la position de 1er true.
>>$$c(e) = k+1 \text{ si le } 1^{er} true \text{ est en position } k$$
>
>>[!tip] Remarque 
>>On écrira souvent que la complexité vaut $k$ pour dire qu'elle est de la forme : 
>>$$ \alpha k + \beta \text{ ou } \Theta(k) \text{ ou } O(h)$$
>
>- dénominateur de $C_{n}(n) : |\lbrace e \in E | e \text{ de taille n}\rbrace|$
>>avec $\lbrace e \in E | e \text{ de taille n} \rbrace$ : l'ensemble des tableau des taille $n$
>>ce cardinal vaut $$ \begin{align} 2^n & = |\lbrace true,false \rbrace \times \lbrace true,false \rbrace \times \dots \times \lbrace true,false \rbrace | \\
 & = |\lbrace true,false \rbrace ^{n} | = |\lbrace true,false \rbrace| ^{n} \end{align}$$
>>C'est le nombre de $n$-uplets à valeurs dans $\mathscr{E} = \lbrace true, false \rbrace$ 
>
> - numérateur de $C_{n}(n)$ : on ajoute $c(e)$ pour toutes entrées de taille $n$. 
>> Les valeurs possibles de $c(e)$ sont tous les $k$, $k \in [| 1 , n |]$
>> Nombre d'entée telles que $c(e) = k$ :
>> $$2^{n-k}$$
>> (le contenu des $k$ $1^{ères}$ cases est imposé, le contenu des $n-k$ dernières cellules est quelconque)
>> Une entrée telle que $c(e)=k$ a la forme :
>>
| 0     |     |       | $k-1$ |     | $n-1$           |
| ----- | --- | ----- | ----- | --- | --------------- |
| false | -   | false | true  | ~~  | ~~ (quelconque) |
>>
>>et <u>le cas où il n'y a que des false : complexité n</u>
>
>$$\begin{align} C_{m}(n) &= \frac{\sum^{n}_{k = 1}2^{n-k}\times k  + n}{2^n}
 & = \sum^{n}_{k=1} k \times \frac{1}{2^k} + \frac{n}{2^n} 
\end{align}$$
> Pour calculer : 
> $$\sum_{e \in E,e \text{ de taille n}} c(e) = \sum^{n}_{k=1} \left(\sum_{\begin{align}
& e \in E ,\\ & e \text{ de taille n}, \\& c(e) = k\end{align}} k\right) $$
>on a scindé la somme entre $n$ somme 
>
>Pour le numérateur, on a regardé et dénombré les entrées $e$ de taille $n$ telles que $c(e)=k$ pour chaque $k \in [|1,n|]$
>
>On a encore 
>$$ \forall n \geq 1, C_{m}(n) = \frac{n}{2^{n-1}} + \sum^{n}_{k =1} \frac{k}{2^k}$$
>D'où l'on déduit que 
>Pour tout $n \geq_{1}$ 
>$$\begin{align}
 C_{m}(n+1) - C_{m}(n) & = \left(\frac{n+1}{2^n} + \sum^{n}_{k=1}\frac{k}{2^k}\right)-\left(\frac{n}{2^{n-1}} + \sum^{n-1}_{k=1}\frac{k}{2^k}\right)  \\
 & = \frac{n+1}{2^n} - \frac{n}{2^{n-1}} + \frac{n}{2^n} \\
 & = \frac{1}{2^n} ((n+1) - 2n + n) \end{align}$$
$$\forall n \geq 1, C_{m}(n+1) - C_{m}(n) = \frac{1}{2^n}$$
>
>On en conclut, par télescopage que : 
>$$ \sum^{n}_{k=1}C_{m}(k+1) - C_{m}(k) = \sum^{n}_{k=1}\frac{1}{2^k} = 1 - \left( \frac{1}{2} \right) ^n$$
>
>On a obtenu :
>$$ \forall n \geq 1, C_{m}(n+1) - C_{m}(1) = 1 - \left(\frac{1}{2} \right)^n \\
>\forall n \geq 1, C_{m}(n+1) = 2 - \frac{1}{2^n}$$
>ou encore $\forall n\geq 2,C_{m}(n)=2-\frac{1}{2^{n-1}}$ (valable encore si $n=1$)
>
><u>Conclusion</u> : la complexité en moyenne $C_{m}(n)$ est en $O(1)$($C_{m}(n)$est majorée par une constante)

### 2)<u>Complexité du tri-bulle</u> : 

>[!warning] tri-bulle et tri sélection
>OK pour des exercices, mais à ne pas citer en exemple 
>(préférer : 
>- tri insertion
>- tri fusion
>- tri rapide)

>[!bug] Implémentation
>Une implémentation en C du tri bulle en place [^2]
>``` C
>void tri_bulle (int* tab, int n){
>	int j = n-1;
>	while (j > 0) {
>		permutation = false;
>		for (int i = 0; i < j; i++){
>			if (tab[i] > tab[i+1]) {
>				int tmp = tab[i];
>				tab[i] = tab[i+1];
>				tab[i+1] = tmp;
>			}
>		}
>		j = j-1;
>	}
>}
>```
>
><u>Principe</u> : 
>on parcourt le tableau en redressant les inversions
>on répète cette opération jusqu'à ce que le tableau soit trié
>
><u>Exemple</u> :
>Premier parcourt 
>
|   i  | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  tab[i]   | 7   | 6   | 5   | 8   | 4   | 2   | 6   | 3   |
|  tab[i]   | 6   | 7   | 5   | 8   | 4   | 2   | 6   | 3   |
|   tab[i]  | 6   | 5   | 7   | 8   | 4   | 2   | 6   | 3   |
|   tab[i]  | 6   | 5   | 7   | 4   | 8   | 2   | 6   | 3   |
|   tab[i]  | 6   | 5   | 7   | 4   | 2   | 8   | 6   | 3   |
|  tab[i]   | 6   | 5   | 7   | 4   | 2   | 6   | 8   | 3   |
|  tab[i]   | 6   | 5   | 7   | 4   | 2   | 6   | 3   | 8   |
>
>Après un parcours on  a :
>
|  i   | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  tab[i]   | 6   | 5   | 7   | 4   | 2   | 6   | 3   | 8   |
>
>On appelle inversion pour la paire $\lbrace i,j \rbrace$ si $i<j$ tandis que $tab[i] > tab[j]$
>Dans le tableau initial : comptons les inversions.
>> - inversion avec $i = 1$ (exemple)
>>$\lbrace i,j \rbrace = {1,2}$ ; $tab[1] =  6$ et $tab[2] = 5$  -> inversion
>>$\lbrace i,j \rbrace = {2,3}$ ; $tab[1] = 6$ et $tab[3] = 8$  -> pas d'inversion
>
> - <u>Algorithme</u> : on parcourt le tableau, en redressant, au fil du parcours les inversions pour les paires $\lbrace i,i+1 \rbrace$. ($0\leq i<n-1$)
>   
>>[!tip] Remarque
>>Lors du premier parcours, le maximum se retrouve à la fin de la liste, car il sera toujours plus grand que l'élément suivant.
>
>>[!info] <u>Invariant de boucle</u>
>>À la fin de la $k^{ème}$ itération, les $k$ plus grands éléments du tableau sont triées et occupent les $k$ dernières cellules.
>>>[!note] Démonstration
>>>À faire ! (démonstration par récurrence sur $k$ initialisation pour $k=0$(avant toute itération))
>
>Si l'invariant de boucle à été prouvé, après $n-1$ itérations les $n-1$ plus grands éléments du tableau seront triés et occuperont les $n-1$ dernières cases.
>Et donc en position $0$, on aura une valeur $\leq$ à toutes les autres et les tableau sera trié.
>
>>[!success] On en conclut que :
>>- après $n-1$ itération le tableau sera trié. (preuve de correction).
>
>La terminaison est assuré par $j$ (variant de boucle).
>Il y a $n-1$ itérations, ce qui assure la correction
>
>>[!tip] Complexité : en comptant les échange et les tests
>>- <u>pire cas</u>
>>$$\begin{align} 
 \sum^{n-1}_{j = 1} \sum^{j-1}_{i = 0} \underbrace{1}_{test} + \underbrace{1}_{échange} & = \sum^{n-1}_{j} 2j \\
 & = 2 \times \sum^{2}_{j = 1} j \\
 & = 2 \times \frac{(n-1)n}{2} \\
 & = (n-1)n = O(n^2)
  \end{align} $$
>> - <u>meilleur cas</u> :
>> $$ \sum^{n-1}_{j} \sum^{j-1}_{i = 0} \underbrace{1}_{test} + \underbrace{0}_{échange} = 1 \frac{(n-1)n}{2}$$
>>
>>Le meilleur cas correspondant à un tableau déjà trié (tous les tes évalués à true)
>>
>> Le pire cas correspond à un tableau triée dans l'ordre décroissant
>>
>> Entre le meilleur et le pire cas, la complexité n'est affecté que par un facteur multiplicatif, mais ne change pas d'ordre de grandeur.
>> Dans tout les cas elle est en $O(n^2)$
>> 
>> - <u>Complexité moyenne</u> : [[Chapitre 20 Complexité avancée#I)<u>Complexité en moyenne</u>|définition]]
>>  $$ C_{m}(n) = \frac{\sum_{\text{entrées de taille n}} c(e)}{\text{nombre d'entrées de taille n}} $$
>>  <u>Ici</u> : les entrées de taille $n$ soit des tableaux de $n$ entiers 
>>  S'il y a $N$ valeurs pour les entiers en machine, il y a $N^n$ entrées possibles (nombre de $n\text{-uplets}$ à valeur dans $E$ de cardinal $N$)
>>  - si l'on s'intéresse à des tableau de $n$ entiers distincts compris entre 1 et $n$, il y a $n!$ entrées possibles.
>>
>>>[!warning] La formule proposée pour la complexité moyenne, toutes des entrées sont supposées <u>équiprobables</u>
>>>Si tel n'est pas le cas, il faudrait utiliser la formule suivante :
>>>$$C_{m}(n) = \sum_{\text{entrée e de taille n}}f(e)c(e)$$
>>>avec $f(e)$ la fréquence de l'entrée $e$
>>
>>Pour l'algorithme proposé : pour toute entrée $\underbrace{1}_{test} \leq c(e) \leq \underbrace{2}_{test + échanges}$
>>$$ \frac{\sum_{\text{entrée e de taille n}} \frac{n(n-1)}{2}}{\text{nbr entrées taille n}} \leq C_{m}(n) \leq \frac{\sum_{\text{entrée e de taille n}} 2\frac{n(n-1)}{2}}{\text{nbr entrées taille n}} \\
 \frac{n(n-1)}{2 \leq C_{m}(n) \leq n(n-1)}$$
>> donc $C_{m}(n) = \Theta(n^2)$
>>> car en divisant par $\frac{n(n-1)}{2}$ il apparaît que $1 \leq \frac{C_{m}(n)}{\frac{n(n-1)}{2}} \leq 2$
>>> Donc  $C_{m}(n) = \Theta(\frac{n(n-1)}{2}) = \Theta(n^2)$
>>> car $\frac{n(n-1)}{2} \sim_{n \to +\infty} n^2$
 

# II)<u>Complexité amortie</u> :

>[!info] Définition
>La complexité amortie étudie la complexité (temporelle) d'une suite d'opérations éffectuées sur une même structure de données

>[!example] Exemples embématiques
>>[!example] ajout d'une valeur dans un <u>tableau dynamique</u>
>>Il s'agit du cas où on stocke des valeurs dans un tableau de taille donnée $n$ et lorsque le tableau est plein on recopie les valeurs dans un tableau de taille $2n$
>
>>[!example] réalisation d'un fille avec deux piles $(entrée,sortie)$
>>Où lorsque la sortie est vide, on bascule (ou vide) la pile "entrée" dans la pile "sortie"
>
>Dans ces deux exemples, <u>l'ajout d'une valeur</u>[^3] est généralement en $O(1)$ masi ponctuellement l'ajout est en $O(n)$
>L'étude de "complexité amortie" permet d'établir sur ces exemples que la complexité moyenne est en $O(1)$.

>[!note] Notions 
>On considère une structure de données initialement vide (pour simplifier) et une suite d'opérations $p_{1},p_{2},\dots,p_{n}$ sur cette structure.
>On suppose que l'on connaît le coût $c_{i}$ de l'opération $p_{i}$, en terme d'opération élémentaires.
>On cherche à déterminer le coût moyen d'une opération,  càd $\frac{1}{n} \sum^{n}_{i = 1}c_{i}$

### 1)<u>Méthode du banquier</u> :

>[!info] info
>Cette méthode consiste à "provisionner de la complexité" en vue des opérations futures.
>Plus précisément, à chaque opération $p_{i}$ :
>on associe :
> - un apport $a_{i}$ que l'on met en réserve
> - une dépense à effectuer $d_{i}$
> On cherche à maintenir l'invariant 
> $$\sum^{k}_{i = 1}a_{i}\geq \sum^{k}_{i = 1}d_{i}$$
> Ce qui traduit que les dépenses n'excédent jamais les placaments
> On pose, pour tout $i$ $c_{i}' = c_{i} + a_{i} - d_{i}$ et grâce à l'invariant, on a :
> $$ \sum^{n}_{i = 1}c_{i}' = \underbrace{\sum^{n}_{i = 0} (c_{i}+a_{i}-d_{i})}_{\sum^{n}_{i = 1}c_{i} + \underbrace{\sum^{n}_{i = 1}(a_{i}-d_{i})}_{\geq 0 \text{(invariant)}}} \geq \sum^{n}_{i = 1}c_{i}$$
> Ainsi, une majoration du membre de gauche, donne une majoration de $\sum^{n}_{i=1}c_{i}$[^4]
>Le but est de choisir des $a_{i}$ et $d_{i}$ permettant d'avoir une majoration "raisonnable" des $c_{i}$
>>[!example] pour les tableaux dynamiques, on peut majorer les $c_{i}$ par une constante
>>>$c_{i} : \text{coût réel de l'opération}$
>>>$a_{i} : \text{ce qu'on ajoute à l'épargne}$
>>>$d_{i} : \text{ce que l'on prélève de l'épargne}$
>>>$c_{i}' : \begin{cases} \text{coût "fictif" résultant}\\ c_{i}'= c_{i} + a_{i} - d_{i} \\ \underbrace{\sum^{n}_{i =1}c_{i}'}_{\text{somme des coûts fictifs}}  \geq \underbrace{\sum^{n}_{i=1}c_{i}}_{\text{somme des coûts réels}} \end{cases}$
>>
| $v_{i}$          | $v_{1}$        | $v_{2}$                                    | $v_{3}$              | $v_{4}$ | $v_{5}$              | $v_{6}$ | $v_{7}$ | $v_{8}$ | $v_{9}$ | $v_{10}$ | ... |
| ---------------- | -------------- | ------------------------------------------ | -------------------- | ------- | -------------------- | ------- | ------- | ------- | ------- | -------- | --- |
| $c_{i}$          | $1$ (écriture) | 1 copie de $v_{1}$ + 1 écriture de $v_{2}$ | 2 copie + 1 écriture | 1       | 4 copie + 1 écriture | 1       | 1       | 1       | 8 + 1   | 1        | ... |
| $a_{i}$          | 1              | 2                                          | 2                    | 2       | 2                    | 2       | 2       | 2       | 2       | 2        | ... |
| $d_{i}$          | 0              | (-)1                                       | (-)2                 | 0       | (-)4                 | 0       | 0       | 0       | (-)8    | 0        | ... |
| $\text{épargne}$ | 1              | 2                                          | 2                    | 4       | 2                    | 4       | 6       | 8       | 2       | 4        | ... |
| $c_{i}'$         | 2              | 3                                          | 3                    | 3       | 3                    | 3       | 3       | 3       | 3       | 3        | ... |
>>
>>On veut enregistrer des données dans un tableau, et doubler la taille du tableau lorsqu'il est plein. Initialement le tableau comporte une case sans valeur.
>>
>>>[!tip] Schema 
>>>$$ \fbox{} \to \fbox{v1} \to \fbox{v1}; \fbox{v2} \to \fbox{v1}; \fbox{v2}; \fbox{v3} ; \fbox{}; \to \fbox{v1}; \fbox{v2} ; \fbox{v3} ; \fbox{v4} \to \fbox{v1} ; \fbox{v2} ; \fbox{v3} ; \fbox{v4} ; \fbox{v5} ; \fbox{} ; \fbox{} ; \fbox{}$$
>>
>>Premier ajout $a_{1} = 1$ $d_{1}=0$
>>Pour tout $i\geq_{2}$ $a_{i}=2$
>>les $d_{i}$ sont tous nuls sauf lorsqu'il y a doublement càd l'ordre $i$ est de la forme $2^j+1,j\geq 0$
>>
>>>[!important] Propriété
>>>$\forall n\geq_{1}, \sum^{n}_{i=1}a_{i} \geq \sum^{n}_{i=1} d_{i}$ (1)
>>
>>>[!tip] Preuve
>>>Pour tout $$\begin{align}
 n\geq 1, \sum^{n}_{i=1}a_{i} & = 2(n-1)+1 \\ 
 & = 2n - 1 \\
a_{1} = 1 \text{ et } a_{i} = 2  \end{align} $$
>>>Si $n$ est tel que $2^k<n<2^{k+1}$ :
>>>$$\begin{align} \sum^{n}_{i=1} d_{i} & = \sum^{k}_{j=0} d_{2^j+1}  \\
 & = \sum^{k}_{j=0} 2^j = 2^{k+1} - 1
\end{align}$$
>>>$\sum^{n}_{i=1} d_{i} < 2n-1 \text{(} 2^k<n \text{ donc } 2^{k+1}<2n \text{ et } 2^{k+1}-1 < 2n-1 \text{)}$
>>>donc $\sum^{n}_{i=1} d_{i} \leq \sum^{n}_{i=1} a_{i}$
>>
>>>[!important] Propriété
>>>$\forall n\geq 1, c_{i}' \leq 3$  (2)
>>
>>>[!tip] Preuve
>>>Pour $i=1$ $c_{1}' = c_{1}+a_{1}-d_{1}=1+1-0=2$
>>>Pour tout $i\geq 2$
>>> - s'il n'y a pas de doublement ($i$ n'est pas de la forme $i=2^{j} +1$) :
>>> $c_{i}'=c_{i}+a_{i}-d_{i}=1+2-0=3$
>>> - si doublement : 
>>> $c_{i}' = c_{i}+a_{i}-d_{i}=2^j+1+2-2^j=3$
>>>> <u>Conclusion</u> : Par la proprité (1) : 
>>>> $$\sum^{n}_{i=1} = \sum^{n}_{i=1} c_{i}+a_{i}-d_{i} = \sum^{n}_{i=1}c_{i} + \underbrace{\sum^{n}_{i=1} a_{i} - \sum^{n}_{i=1} d_{i}}_{\geq 0 \text{ par } (1)}$$
>>>
>>>On  a donc $\sum^{n}_{i=1}c_{i}' \geq \sum^{n}_{i=1}c_{i}$ or par (2) 
>>>$\sum^{n}_{i=1} 3 \geq \sum^{n}_{i=1} c_{i}' \geq \sum^{n}_{i=1} c_{i}$
>>>d'où $0 \leq \sum^{n}_{i=1} c_{i} \leq 3n$
>>>d'où la complexité moyenne 
>>>$C_{m}(n) = \frac{1}{n} \sum^{n}_{i=1}c_{i} \leq 3$ donc $C_{m}(n) = O(1)$


### 2)<u>Méthode du potentiel</u> : 

>[!info] Info
>Ici on affecte une valeur, le potentiel, à chaque configuration possible de la structure de données.
>On note ici $\Phi(D)$ le potentiel de la configuration $D$.
>
>Si on note $D_{0}$ la configuration initiale de la structure de donnée. Et $D_{i}$ la configuration après la $i^{ème}$ itération.
>On appelle coût amorti :
>$$c_{i}' = c_{i} + \underbrace{\Phi(D_{i})}_{\text{après ième op}}  - \underbrace{\Phi(D_{i-1})}_{\text{avant ième op}}$$
>
>Le coût amorti des $n$ premières opérations :
>$$\begin{align} \sum^{n}_{i=1} c_{i}' & = \sum^{n}_{i=1} \lbrace c_{i} + \Phi(D_{i}) - \Phi(D_{i-1}) \rbrace \\ \\
& = \lbrace \sum^{n}_{i=1} c_{i} \rbrace + \lbrace \sum^{n}_{i=1} \Phi(D_{i})-\Phi(D_{i-1}) \rbrace \\ \\
\sum^{n}_{i=1} c_{i}' & = \lbrace \sum^{n}_{i=1} c_{i} \rbrace + \underbrace{\Phi(D_{n}) - \Phi(D_{0})}_{\text{on fera en sorte de définir }D_{n}^* \\ \text{ pour que } \forall n \in \mathbb{N}, \Phi(D_{n})\geq \Phi(D_{0}) \\ \text{ de sorte que } \\ \forall n \geq 1, \sum^{n}_{i=1} c_{i}' \geq \sum^{n}_{i=1} c_{i}}
\end{align}$$
>$^*$ : on pend souvent $\Phi(D_{0}) =0$ et $\forall i\geq 1, \Phi(D_{i})>0$

>[!example] <u>Exemple</u> :  Structure de donnée de file construit avec deux piles :
> $D = \left( \underbracket{-}_{in}, \underbracket{-}_{out}\right)$ 
>> - on enfile dans la pile $in$ toujours
>> - pour défiler, on défile depuis $out$ si $out$ non vide. Si $out$ vide, on vide $in$ dans $out$ et on défile depuis $out$
>> (<u>rq</u> : si $in$ et $out$ sont vide on ne peut pas défiler)
>
>On posera $\Phi(D) = 2|in|$ nombre d'élément dans $\underline{in}$.
>La fonction de potentiel est bien positive (et si $D_{0}$ vide $\Phi(D_{0})=0$) 
>
>> -<u>calcul de </u>$\underline{c_{i}'}$ :
>> ▪ si l'opération $i$ est <u>un ajout</u> on a $c_{i} = 1$ (ajout à $in$) et la taille de $in$ augmente de 1, donc $\Phi(D_{i}) - \Phi(D_{i-1}) = 2$
>> $c_{i}' = c_{i} + \underbrace{\Phi(D_{i}) - \Phi(D_{i-1})}_{2}$
>> $c_{i}' = 1+2=3$
>> ▪ <u>si l'opération est un retrait sans basculement</u> : 
>> $c_{i} = 1$, pas de variation de potentiel, $in$ inchangé
>> $c_{i}'=1$
>> ▪<u>si retrait avec basculement</u> :
>> si on note $A = |in|$ $c_{i}' = 2A + 1 + \Phi(D_{i}) - \Phi(D_{i-1})$ (chaque élément de $in$ est dépilé depuis $in$ empilé dans $out$)
>>  $= 2A + 1 + 0 - 2A$
>>  $= 1$
>
>Ainsi on a montré que : $\forall i\geq 1 : c_{i}'\leq 3$ donc $\sum^{n}_{i=1}c_{i}'\leq 3n$ 
>et comme $$\sum^{n}_{i=1}c_{i}' = \lbrace \sum^{n}_{i=1} c_{i} \rbrace + \underbrace{ \Phi(D_{n}) - \Phi(D_{0})} $$
>$$ 0 \leq \\sum^{n}_{i=1}c_{i} \leq \sum^{n}_{i=1} c_{i}' \leq 3n$$
>Donc pour la complexité moyenne :
>$$ C_{m}(n) = \frac{1}{n} \lbrace \sum^{n}_{i=1}c_{i} \rbrace \leq \frac{1}{n} \sum^{n}_{i=1}c_{i}' \leq 3$$
>
>><u>Conclusion</u> :
>>$C_{m}(n) = O(1)$





[^1]: à rechercher pour un $n$ donné. (et non pour des cas particuliers comme $n=0$ ou $n=1$)

[^2]: <u>càd</u> : on modifie le tableau sans en créer un nouveau

[^3]: (exemple 1) ou <u>le retrait d'une valeur</u> (exemple 2)

[^4]: coût réel

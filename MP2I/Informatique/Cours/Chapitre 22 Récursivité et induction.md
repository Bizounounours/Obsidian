# I)<u>Récurrence sur </u>$\underline{\mathbb{N}}$ (cas particulier d'induction)

>[!tip] Théorème
>Soit $P(n)$ un prédicat sur les entiers naturels
>Si les deux conditions suivantes sont réalisées :
> - $P(0)$ vraie
> - $\forall n \in \mathbb{N}, P(n) \implies P(n+1)$ 
>
>alors : $\forall n \in \mathbb{N}, P(n)\text{ vraie}$

>[!check] Démonstration
>On propose une démonstration par l'absurde en s'appuyant sur le fait que <i>toute partie non vide de $\mathbb{N}$ admet un plus petit élément (★)</i>.
>Soit $E = \lbrace n,n \in \mathbb{N} | P(n) faux \rbrace$, on suppose que $E$ est non vide (déni par l'absurde).
>
>$E$ étant non vide, il admet un élément minimal par (★) que l'on note $n_{0}$
> - $n_{0}$ est non nul, d'après le cas de base
> - donc $n_{0}-1$ (prédecesseur de $n_{0}$) existe et comme $n_{0}$ éléments minimal de $E$ : $n_{0}-1 \not \in E$ donc $P(n_{0}-1)$ vraie.
>
>Par suite, d'après l'hypothèse d'hérédité [^1] , $P((n_{0}-1)+1) = P(n_{0}) vraie$
>Ce qui contredit l'hypothèse
>
><u>Conclusion</u> : $E$ est vide


# II)<u>Ensembles ordonnées</u> :

>[!cour] Rappel
>Si $E$ est un ensemble non vide, une <font color = 'red'><u>relation bianire</u></font> sur $E$ est un sous-ensemble de $E\times E$

>[!example] 
>Dans $\mathbb{N}, a\mathscr{R}_{1}b \text{ si}_{def } \text{ } a|b$ (relation d'ordre)
>Dans $\mathbb{Z}$,  $a\mathscr{R}_{2}b$ $si_{def}$ $a \equiv b [4]$ (relation d'équivalence)
>Dans $E = \lbrace1,2,3,4 \rbrace$, $a\mathscr{R}_{3}b$ $si_{def}$ la case de coordonnées $(a,b)$ est cochée dans : 
>
>
| a\b | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
| 1   | X   |     |     |     |
| 2   |     |     | X   |     |
| 3   |     |     |     |     |
| 4   |     | X   | X   |     |
>
><u>ici</u> : $2\mathscr{R}_{3}3$ vraie et $3\mathscr{R}_{3}2$ faux

>[!cour] Définition
>Soit $E$ un ensemble non vide, et $\color{cyan} \leq$ une relation binaire sur E,
>La relation binaire $\leq$ est une relation s'ordre si $si_{df}$ :
> - $\leq$ est réflexive : $\forall x \in E, x\leq x$
> - $\leq$ est antisymétrique : $\forall(x,y)\in E\times E, (x\leq y \text{ et } y\leq x) \implies (x=y)$
> - $\leq$ est transitive : $\forall(x,y,z)\in E^3, (x\leq y \text{ et } y\leq z) \implies (x\leq z)$

>[!example] 
> - ordre usuel sur $\mathbb{N}$
>$(x\leq y)\text{ }si_{df}\text{ }(\exists z \in \mathbb{N} | y=x+z)$
>- relation de divisibilité dans $\mathbb{N}$ 
>$(x|y)\text{ }si_{df}\text{ }(\exists z \in \mathbb{N} | y=xz)$
>- un exemple dans $\mathbb{R}[X]$
>$(P\leq Q)\text{ }si_{df}\text{ }(\underbrace{P=Q\text{ ou }}_{\text{pour assurer l'antisymétrie}}\deg(P)\leq \deg(Q))$

>[!important] Remarque 
>on note $x<y$ pour exprimer que $x\leq y$ et $x \not=y$
>on note $x\geq y$ pour exprimer que $y\leq x$
>on note $x>y$ pour exprimer que $y\leq x$ et $x \not=y$

>[!warning] $>$ et $<$ ne sont plus des relations d'ordre (car propriété de symétrie perdue)

>[!cour] Définition
>Soit deux éléments distincts $x$ et $y$ d'un ensemble $E$, muni de l'ordre $\leq$, on dit que
>>$x$ est un prédécesseur de $y$ (ou de façon équivalente $y$ est un successeur de $x$) si on peut comparer $x$ et $y$ et que $x\leq y$
>
>On parle de prédécesseur immédiat (respectivement successeur immédiat)
>> si $(x\leq z \text{ et } z\leq y) \implies(z=x\text{ ou }z=y)$
>
>>[!tip] remarque
>>c'est-à-dire $x\leq y$ et on ne peut intercaler aucun élément entre $x$ et $y$

>[!cour] Définition
>Soit $E$ un ensemble ordonnée (<font color ='cyan'>i.e.</font> muni d'un ordre) et $x \in E$
>
>On dit que $x$ est un <font color ='red'><u>élément minimal</u></font> (resp. <font color ='red'><u>maximal</u></font>) de $E$
>$si_{df}$ $x$ n'admet pas de prédécesseur (resp. successeur) dans $E$

>[!example] 
>$0$ éléments minimal de $\mathbb{N}$
>Pas d'éléments maximal dans $\mathbb{N}$
>
>Dans $\mathbb{R}[X]$ muni de l'ordre précédent : plusieurs éléments minimaux (tous les polynômes constants). <font color ='cyan'>(si on n'a pas affecté le degré </font>$\color{cyan} -\infty$<font color ='cyan'> ou polynôme nul).</font>

>[!cour] Définition
>Une relation d'ordre $\leq$ sur un ensemble $E$ est un <font color ='red'><u>ordre total</u></font> $si_{df}$ $\forall x,y \in E$ $x$ et $y$ sont comparables (càd $x\leq y$ ou $y\leq x$).
>Un ordre qui n'est pas total est dit **partiel**

>[!example] 
>- l'ordre usuel sur $\mathbb{N}$, sur $\mathbb{Z}$, sur $\mathbb{R}$ est total
>- l'ordre induit par la divisibilité est partiel sur $\mathbb{N}$ ou $\mathbb{Z}$


>[!cour] Défnition
>Un ensemble muni d'un ordre total possède <font color ='red'><u>au plus</u></font> un <font color ='red'><u>élément minimal</u></font> (resp. maximal)
>On l'appelle, *s'il existe*, plus petit (resp. plus grand) éléments

>[!important] Remarque 
>La donnée d'un ordre sur un ensemble, induit un ordre sur chacun de ses sous-ensembles, on étendra de ce fait les définitions d'éléments minimal/maximal et plus petit/plus grand élément.

>[!check] Démonstration
>s'il existe deux éléments minimaux $a$ et $b$, alors :
> - l'ordre étant supposé total, $a$ et $b$ sont alors comparables et on supposes, quitte à échanger leurs noms que $a\leq b$
> - or par hypothèse $b$ est un élément minimal (même si on a échanger les noms) donc (par def) $b$ n'admet pas de prédécesseurs. 
>   donc $a\leq b \implies a=b$
>
>On conclut à l'unicité si existence de l'élément minimal

>[!important] Propriété *(point clé du cours)*
>Soit $E$ un ensemble ordonnée par $\leq$
>Les deux propriétés suivantes sont équivalentes :
>$(1)$-> tout sous-ensemble non vide de $E$ admet un élément minimal
>$(2)$ -> toute suite infinie décroissante d'éléments de $E$ est stationnaire[^2]
>>[!note] Note : il n'est pas demandé ici que l'ordre soit total

>[!check] Démonstration 
>$(1) \implies (2)$ :
>
>On considère une suite $(x_{n})_{n \in \mathbb{N}}$ d'éléments de $E$ décroissante. *On cherche à montrer qu'elle est stationnaire*.
>On note $F = \lbrace x_{n},n \in \mathbb{N} \rbrace$ (ensemble des valeurs de la suite)
>$F$ est non vide (car $(x_{n})$ est une suite infinie)
>donc, par $(1)$, $F$ admet un élément minimal, que l'on peut noter $x_{k_{0}}$
>Alors $\forall n\geq k_{0}, x_{n}\leq x_{k_{0}}\text{ car }(x_{n})décroissante$
>Or $x_{n}$ et $x_{k_{0}}$ sont comparables (*non pas parce que l'ordre est total mais parce qu'on sait que*$\color{cyan} x_{n}\leq x_{k_{0}}$)
>et, par ailleurs $x_{k_{0}}$ est minimal.
>donc $(2)$ $x_{n}\geq x_{k_{0}}$
>et par antisymétrie[^3] $x_{n}=x_{k_{0}}$
>Ce qui établi que : 
>$$\forall n\geq k_{0}, x_{n} = x_{k_{0}}$$
>et prouve que la suite est stationnaire (à partir du rang $k_{0}$)
>
>$(2) \implies (1)$:
>
>Considérons $F$ un sous-ensemble non vide de $E$.
>$F$ est non vide et on note $\color{cyan}a$ un élément de $F$
>On construit la suite $(x_{n})_{n \in \mathbb{N}}$ définie par : 
>>$x_{0} = a$
>>et pour tout $n\geq_{0}, x_{n+1}=\cases{\text{un prédécesseur de }x_{n}\text{ s'il en exite} \\ x_{n}\text{ sinon}}$
>
>D'après $(2)$, la suite $(x_{n})$ est stationnaire, donc, il existe un rang $n_{0}$ et un élément $b$ de $E$ tels que : $\underline{\forall n\geq n_{0}, x_{n}=b}$
>$x_{n}=b$ et $x_{n+1}=b$ donc par définition de $(x_{n})$ cela signifie que $b$ n'a pas de prédécesseur, donc $b$ est un élément minimal de $F$
>
>Ce qui termine la démonstration.

>[!cour] Définition : Ordre bien fondé
>Un ordre bien fondé est un ordre qui vérifie l'une des deux propriétés équivalentes précédentes

>[!cour] Corolaire
>Si E est un <font color="red"><u>ensemble muni</u></font> d'un <font color="red"><u>ordre bien fondé</u></font>:
>il n'existe pas de suite infinie strictement décroissante

>[!example] 
>L'ordre usuel sur $\mathbb{N}$ est bien fondé
>L'ordre usuel sur $\mathbb{Z}$ ne l'est pas
>L'ordre alphabétique sur les mots, ne l'est pas 
> --> pour cela, considérer la suite $(a^nb)_{n \in \mathbb{N}}$ (infinie strictement décroissante, $\underbrace{a\dots ab}_{n+1\text{ fois}} < \underbrace{a\dots a}_{n\text{ fois}}b$)

>[!cour] Application : généralisation de variant d'appel
> -$\underline{\text{Sur }\mathbb{N}}$ :
>  1. quantité entière
>  2. positive (tout les appels se poursuivent)
>  3. strictement décroissante à chaque appel <u>récursif</u>
>
>-$\underline{\text{Sur }E\text{ muni d'un ordre bien fondé}}$ :
> 1. une valeur élément de $E$
> 2. diminuant strictement à chaque appel <u>récursif</u>
>    
>Dans les deux cas ($\mathbb{N}$ ou $E$), les appels terminent sinon il existerait une suite infinie strictement décroissante (la suite des valeurs du variant)

### -<u>Ordres sur les produits d'ensembles</u> :

>[!cour] Définition
>Soit une famille d'ensembles ordonnées $(E_{i},\leq_{i})_{i \in I}$
>l'ordre produit sur l'ensemble $\prod_{i \in I}E_{_{i}}$ est défini par :
>$$(x_{i})_{i \in I} \leq (y_{i})_{i \in I} \text{  si}_{df}\text{  } \forall i \in I, x_{i}\leq_{i} y_{i}$$

>[!important] Remarque
>$\prod_{i \in I}E_{i}$ désigne l'ensemble des éléments de la forme $(x_{i})_{i \in I}$

>[!example] 
>$I=[\![1,3]\!]$ $\prod_{i \in I}\mathbb{R} = \mathbb{R}\times\mathbb{R}\times\mathbb{R} = \mathbb{R}^3$ les éléments de $\prod_{i \in I}E_{i}$ (où $E_{i} = \mathbb{R}$) sont des triplets $(x_{1},x_{2},x_{3})$
>
>$I=\mathbb{N}$ et si $\forall i \in \mathbb{N}, E_{i} = \mathbb{C}$ alors $\prod_{i \in \mathbb{N}}E_{i} = \mathbb{C}^\mathbb{N}$ ensemble des suites à valeurs dans $\mathbb{C}$
>
>$I=\mathbb{R}$ et $\forall i \in I, E_{i} =\mathbb{R}$ alors $\prod_{i \in I}E_{i} = \mathbb{R}^\mathbb{R}$ ensemble des fonctions de $\mathbb{R}$ dans $\mathbb{R}$

>[!note] N.B
>Même si l'ordre sur les $E_i$ est total, l'ordre sur le produit ne l'est pas nécessairement.
>>[!example] 
>>$(2,4)$ et $(3,1)$ ne sont pas comparables si $E_{1}=E_{2}=\mathbb{N}$ muni de l'ordre usuel.
>>car $(2,4)\leq(3,1)$ signifierait que $2\leq 3$ et $\underbrace{4\leq 1}_{faux}$
>>$(3,1)\leq(2,4)$ signifierait que $\underbrace{3\leq 2}_{faux}$ et $1\leq 4$ 

>[!note] N.B
>Cette définition cache aussi une propriété :
>on peut démontrer que la relation ainsi définie est bien un ordre sur $\prod_{i \in I}E_{i}$

>[!important] Propriété
>L'ordre produit sur une famille <font color="red">finie</font> d'ensembles munis chacun d'un ordre bien fondé 
>est un ordre bien fondé

>[!check] Démonstration
>Notons $I=[\![1,k]\!]$ (on s'intéresse à une famille finie).
>et considérons une suite $x=(x_{n})_{n \in \mathbb{N}}$ une suite d'éléments de $E=\prod^{k}_{i=1}E_{i}$ qui soit décroissante.
>On note pour chaque terme $x_{n} = (x_{n}^{(1)},x_{n}^{(2)},\dots,x_{n}^{(k)})\in E_{1}\times E_{2}\times\dots E_{k}$
>
>Par définition de l'ordre produit :
>la décroissance de $(x_n)$ : $\forall n \in \mathbb{N}, x_{n+1} \leq x_{n}$
>signifie que $\forall n \in \mathbb{N}, \forall i \in [\![1,k]\!], x_{n+1}^{(i)}\leq_{i} x_{n}^{(i)}$
>càd : $\forall i \in [\![1,k]\!], (x_{n}^{(i)})$ décroissante.
>
>Or chaque $(x_{n}^{(i)})_{n \in \mathbb{N}}$ est à valeur dans $E_{i}$ dont l'ordre est bien fondé et donc la décroissance implique l'existence d'un rang :
>$n_{0}^{(i)}$ tel que $\forall n \geq n_{0}^{(i)}, x_{n}^{(i)}=x_{n_{0}^{(i)}}^{(i)}$ (stationnarité)
>
>Si on pose $n_{0} = max_{1\leq i\leq k\text{ }} n_{0}^{(i)}$
>on a : $\forall n \geq n_{0}, \forall i \in [\![1,k]\!], \underbrace{x_{n}^{(i)} = x_{n_{0}}^{(i)}}_{\text{i.e }x_{n}=x_{n_{0}}}$
>


### -<u>Ordre Lexicographique</u> : [^4]

>[!cour] 
>Soit $E$ un ensemble ordonné par un ordre $\leq$ et un entier $n$,
><font color = "red"><u>l'ordre lexicographique</u></font> sur $E^n$, ensemble de <font color = "red">n-uplets</font> d'éléments de $E$ est défini par :
>$$(x_{i})_{1\leq i\leq n}\leq(y_{i})_{1\leq i\leq n}\text{  si}_{df}\text{ } \left( (x_{i})_{1\leq i\leq n} = (y_{i})_{1\leq i\leq n} \text{ ou } \exists N \in [\![1,n]\!], \forall i<N, x_{i}=y_{i} \text{ et } x_{N}<y_{N} \right)$$

>[!important] Propriétés
>Si $E$ est non vide et son ordre est total (respectivement bien fondé) alors l'ordre lexicographique sur $E^n$ est total (respectivement bien fondé)

>[!check] Démonstration
>À faire

>[!example] 
>*Montrer que la fonction d'Ackermann termine*
>``` OCaml
>let rec ack n p = match n,p with
>	|0,p -> p+1
>	|n,0 -> ack (n-1) 1
>	|n,p -> ack (n-1) (ack n (p-1))
>```
>
><u>Indication</u> :
>utiliser $(n,p)$ comme variant d'appel et l'ordre lexicographique sur $\mathbb{N}^2$

# III)<u>Induction</u> :

### 1)<u>Induction bien fondée</u> : (généralisation du raisonnement par récurrence)

>[!cour] Théorème
>Soit $(X,\leq)$ un ensemble ordonnée non vide, et une propriété $P$ sur $X$.
>si $\leq$ est bien fondé, alors :
>$$(\forall x \in X,\underbrace{(\forall y \in X, y<x \implies P(y)) \implies (P(x))}_{I_{p}(x)}) \implies (\forall x \in X, P(x))$$
>
>$I_{p}(x)$ signifie : "Si la propriété est vrai pour tous les prédécesseurs $y$ de $x$ alors elle est vraie pour $x$"
>L'hypothèse du théorème est que $I_{p}(x)$ est vraie pour tout $x$

>[!note] N.B
>- Supposer que $I_{p}(x)$ est vraie pour un $x$ qui n'a pas de prédécesseur, revient à supposer que : "vrai"$\implies P(x)$ vraie
>càd revient à supposer $P(x)$ est vraie sans pouvoir s'appuyer sur aucune hypothèse
>
>$\color{cyan}\text{Ce qui correspond à faire l'hypothèse que }P(x)\text{ est vraie "sur les cas de base",}$
>$\color{cyan}\text{càd sur les éléments minimaux de X}(\underline{ex}: n=0\text{ pour }X=\mathbb{N})$
>
>- Pour $X=\mathbb{N}$, faire l'hypothèse que $I_{p}(x)$ est vraie pour tout $x \in X$, revient, pour les éléments ayant des prédécesseur, à faire l'hypothèse $\forall n \in \mathbb{N}^*, (\forall k \in [\![0,n-1]\!],P(k)) \implies P(n)$ *hypothèse d'hérédité de la récurrence forte*

>[!check] Démonstration
>On considère $A=\lbrace x \in X, P(x) faux \rbrace$
>On suppose que $A \not = \emptyset$
>et comme $X$ est muni d'un ordre bien fondé, il existe un élément minimal dans $A$ qui permet de mettre en évidence une contradiction

>[!example] 
>Prouver par induction sur $\mathbb{N}^2$ muni de l'ordre lexicographique que la fonction 
>``` OCaml
>let rec somme a b = 
>	if a = 0 then b else somme (a-1) (b+1)
>```
>revoie bien $a+b$ pour tout $(a,b)\in \mathbb{N}^2$

### 2)<u>Ensembles inductifs</u>

>[!cour] Définition "Définition inductive" (appelé jusqu'alors : définition récursive)
>Soit $E$ un ensemble.
>Une définition inductive sur $E$ est la donnée :
> - d'un sous-ensemble $B$ non vide de $E$,
> - d'un ensemble de fonctions $(r_{i})_{i \in I}$ d'<font color = "red"><u>arités</u></font>[^5] respectives $(m_{i})_{i \in I}$ appelées <font color = "red"><u>règles d'inférences</u></font> telles que :
> $$ r_{i} : \underbrace{X^{m_{i}}}_{m_{i}-uplets\text{ d'éléments de X}} \to X$$

>[!example] 
>pour définir une type d'arbre binaire :
>``` OCaml
>type arbre = Vide | Noeud of arbre * arbre
>(* ici |l'ensemble B={Vide}  cas de base *)
>(*     |uen seule règle d'inférence r (Noeud, à voir comme une focntion à 2 paramètres permettant de fabriquer des éléments de X)*)
>```

>[!important] remarque
>On peut autoriser les règles d'inférence à prendre des arguments, ailleurs que des X, par exemple des étiquettes comme on fait pour les arbres

>[!cour] Définition : Ensemble Inductif
>Soit $E$ une ensemble, et une définition inductive sur $E$, d'ensemble de base $B$, et d'ensemble de règles d'inférence $R$,
>On définit : 
>> $X_{0} = B$
>> $\forall n \in \mathbb{N}, X_{n+1} = X_{n \bigcup \lbrace r_{i}(x_{1},x_{2},\dots,x_{m_{i}}),r_{i}\in \mathbb{R},(x_{1},x_{2},\dots,x_{m_{i}})\in X_{n} \rbrace}$

>[!note] 
>On note $\color{red} X=\bigcup_{n \in \mathbb{N}} X_{n}$ qui est l'ensemble construit par induction à partir de $R$ et $B$

>[!important] Propriété
>$X$ est le plus petit ensemble qui contient $B$ et qui est stable par $R$

>[!example] 
>$X =\mathbb{N}$ est un sous-ensemble de $\mathbb{R}_{*}$ défini inductivement :
>> par $0 \in X$ $\color{grey}( B=\lbrace 0 \rbrace)$  
>> et $n \in X \implies n \underbrace{+1}_{\text{ici addition dans }\mathbb{R}} \in X$ $\color{grey}\left(\text{règle d'inférence : }r:\cases{X=\underbrace{X^1}_{\text{arité de r=1}}\to X \\ n \mapsto n+1}\right)$ 

>[!important] Remarque
>Si on ne fait pas référence à $\mathbb{R}$ on présentera plutôt 
>$$ (*) \begin{cases}
zéro \in X \text{\color{grey}zéro est une assertion}  \\
x \in X \implies \text{succ } x \in X \text{\color{grey}(règle d'inférence)}
\end{cases}$$
>
>Les éléments de $\mathbb{N}$ sont ici des mots écrits avec l'alphabet latin et des ( ).

>[!example] exemples
>-<u>ensemble des entiers pairs</u> :
>Sous-ensemble de $\mathbb{N}$ défini inductivement par :
>$$\begin{cases}
0 \in X \color{grey} \text{ (ou zero } \in X \text{ si }\mathbb{N} \text{ défini par *)} \\
n \in X \implies n+2 \in X \color{grey} \text{ (ou succ (succ x)} \in X \text{ si } \mathbb{N} \text{ défini par (*))}
\end{cases}$$
>
>- <u>ensemble des expressions bien parenthésées (exemple simplifié)</u> :
>cas de base :
>> $\epsilon = \text{""} \in X \color{grey} \text{ (le mot vide appartient à X) ("" est l'unique assertion)}$
>> $x \in X \implies (x)\in X \color{grey}\text{ (règle d'inférence : }r_{1}\cases{X \to X \\ x \mapsto r_{1}(x)=(x)}$
>> $x \in X, y \in X \implies xy \in X \color{grey}\text{ règle d'inférence : }r_{2}\cases{X^2 \to X \\ (x,y) \mapsto xy}$
>
><u>ex</u> : de mots de  cet ensemble (ensemble de Dyck)
> - mot vide noté $\epsilon$
> - $r_{1}(\epsilon) = ()$

>[!cour] Définition : hauteur
>Soit $X$ un ensemble inductif et $x \in X$
>On appelle hauteur de $x$, le plus petit indice, $n_{0}$, tel que $x \in X_{n_{0}}$ *(voir définition par récurrence sur page précédente)*
>càd $h:x \mapsto min \lbrace n \in \mathbb{N} |x \in X_{n}\rbrace$

>[!example] Exemple
>Arbres binaires non étiquetés
>$$\begin{cases} Vide \in AB \text{\color{grey} (AB ensemble des arbres binaires)} \\
g \in AB, d\in AB \implies N(g,d)\in AB
\end{cases}$$
>
>□ $h(Vide) = 0$,  $X_{0}= \lbrace Vide \rbrace$ ensemble des assertions
>□$h(N(Vide,Vide))=1$, $X_{1}= \cases{X_{0}\bigcup \lbrace N(x,y),(x,y)\in X_{0}^2 \rbrace \\ X_{0}\bigcup \lbrace N(Vide,Vide) \rbrace \\ \lbrace Vide,N(Vide,Vide)\rbrace}$
>□<u>un élément de hauteur 2</u> :
>$$N(N(Vide,Vide),Vide)$$ est de hauteur 2
>les autres sont :
>$$N(Vide,N(Vide,Vide))$$
>$$N(N(Vide,Vide),N(Vide,Vide))$$
>en tout 3 éléments de hauteur 2, càd éléments de $X_{2} \setminus X_{1}$

>[!cour] Définition
>Sur tout ensemble définit inductivement on peut définir la relation $\mathscr{R}$ suivante :
>$x \mathscr{R}y\text{ }$ $\text{ }si_{df}\text{ }$ $\exists n \in \mathopen{R},\text{ d'arité m, et }(x_{1},x_{2},\dots,x_{m})\in X\text{ et }i_{0}\in[\![1,m]\!]$
>$\text{tel que } y = r(x_{1},x_{2},\dots,x_{m})\text{ et }x_{i_{0}}=x$
>>càd $x \mathscr{R}y$ si "$y$ peut être construit à partir de $x$"

>[!example] Exemple
>Pour des arbres binaires $a=N(g,d)$ : $g \mathscr{R}a$

>[!important] À remarquer
>Si $x \mathscr{R}y$ alors $h(y)\geq h(x)+1$ *(à démontrer)*

>[!warning] $\mathscr{R}$ n'est pas une relation d'ordre

>[!cour] Définition : composition de deux relations :
>>Si $\mathscr{R}$ et $\mathscr{R}'$ deux relations sur un ensemble $E$ alors  $\mathscr{R} \circ \mathscr{R}'$ définie par :
>>$x \mathscr{R}\circ\mathscr{R}'y \text{ }$ $\text{ }si_{df\text{ }}$ $\exists z \in E\text{ tel que } x\mathscr{R}z\text{ et }z\mathscr{R}'y$
>>est appelée composition de $\mathscr{R}$ avec $\mathscr{R}'$
>
>C e qui permet de définir par récurrence pour tout $n \in \mathbb{N}n \mathscr{R}^n$ par :
>$\mathscr{R}^{0} = \lbrace(x,x),x \in E \rbrace$ *($\mathscr{R}^{0}$ est la relation par laquelle tout $x$ est en relation avec lui même)*
>$\mathscr{R}^{n+1} = \mathscr{R}^n \circ \mathscr{R}$

>[!cour] Définition
>On appelle <font color = "red"><u>clôture transitive</u></font> d'une relation $\mathscr{R}$ sur un ensemble $E$, on note $\leq_{E}$ la relation :
>$$\leq_{E} = \bigcup_{n \in \mathbb{N}} \mathscr{R}^{n}$$

>[!cour] <u>Signification de la définition</u> :
>$x\leq_{E}y$ signifie que le couple $(x,y)$ appartient à la partie $\bigcup_{n \in \mathbb{N}} \subset E\times E$
>
><u>càd</u> : $x\leq_{E}y$ s'il existe $n \in \mathbb{N}$ tel que $x\mathscr{R}^ny$

>[!important] Propriété
>$\boxed{\leq_{E}\text{est une relation d'ordre}}$ 

>[!check] Démonstration
> - $\leq_{E}$ réflexive : où $(\forall x \in E, x\leq_{E}x)$
><u>car</u> : 
>$(x,x)\in\mathscr{R}^0$ $(x\mathscr{R}^0x)$
>donc $(x,x)\in \bigcup_{n \in \mathbb{N}} \mathscr{R}^n$
>>[!note] 
>>c'est l'ajout (imposé par la définition) de $\mathscr{R}^0$ dans l'union qui assure la réflexivité, on peut parler de "clôture réflexive" de la relation $\mathscr{R}$
>
>------------------------------------------------------------------------
>
>- $\leq_{E}$ antisymétrique : càd $\forall x,y \in E, si (x \leq_{E}y et y\leq_{E}x)$ alors $(x=y)$
><u>car</u> : 
>si $x \leq_{E}y$, cela signifie que $\exists n_{1} \in \mathbb{N}$ tel que $x\mathscr{R}^{n_{1}}y$
>si $y \leq_{E}x$, cela signifie que $\exists n_{2} \in \mathbb{N}$ tel que $y\mathscr{R}^{n_{2}}x$
>
>(Par l'absurde) si $x \not= y$ alors $n_{1}\not=0$ (car $x\mathscr{R}^0y$ est faux) donc $n_{1}\geq1$ et de même $n_{2}\geq1$
><u>et donc pour la propriété de la fonction hauteur</u>
>$n_{1}\geq 1$ <u>donc</u> $h(y)\geq h(x)+1$ $\color{red}\text{càd }h(y)>h(x)$
>$n_{2}\geq 1$ <u>donc</u> $h(x)\geq h(y)+1$ $\color{red}\text{càd }h(x)>h(y)$
>$\color{red} CONTRADICTION$
><u>Conclusion</u> : $x=y$ (par l'absurde)
>
>------------------------------------------------------------------------
>
>- $\leq_{E}$ transitive : 
>si $x\leq_{E}y$ et $y\leq_{E}z$ alors $\exists n_{1},n_{2}\in \mathbb{N}$ tel que $x\mathscr{R}^{n_{1}}y$ et $y\mathscr{R}^{n_{2}}z$
>ce qui implique $x\mathscr{R}^{n_{1}+n_{2}}z$ (par définition de $\mathscr{R}^n$)
>càd $x\leq_{E}z$
>
>><u>suite</u> : c'est un ordre bien fondé, on a un principe d'induction.

>[!important] Propriété 
>$\boxed{\leq_{X} \text{est un ordre bien fondé}}$ 

>[!check] Démonstration
>Pour $x, y \in X$, tels que $x \mathscr{R}y$, comme on vient de le démontrer, on a $h(y) \geq h(x) + 1$. 
>Il en découle, par récurrence et d’après la définition de $\mathscr{R}^k$ , que pour tout $k \in \mathbb{N}$ : 
>$$\text{(4) si } x \mathscr{R}^k y,\text{ alors } h(y) \geq h(x) + k$$
> (démonstration laissée au lecteur). 
> En conséquence, puisque $x \leq_{X}y$ signifie qu’il existe $k \in \mathbb{N}$ tel que $x \mathscr{R}^k y$, et pour lequel on a $h(y) \geq h(x) + k$, et, a fortieri, $h(x) \leq h(y)$, on peut énoncer que la fonction ℎ vérifie : 
> $$(5) (x \leq_{X}y) \implies (h(x)\leq h(y))$$ 
> Considérons maintenant une suite $u = (x_{n})_{n \in \mathbb{N}}$ décroissante d’éléments de $X$, et la suite des hauteurs des éléments des éléments de cette suite, $v = (h(x_{n}))_{n \in \mathbb{N}}$.
> 
> En vertu de la propriété $(5)$, la décroissance de la suite $u$ implique celle de la suite $v$. Or la suite $v$ est à valeurs dans $\mathbb{N}$, et décroissante pour l’ordre usuel sur $\mathbb{N}$, bien fondé, donc la suite $v$ est stationnaire, i.e. constante à partir d’un certain rang $n_{0}$. 
> 
> Or, si $x_{n+1}\leq x_{n}$, cela signifie qu’il existe $k \in \mathbb{N}$ tel que $x_{n+1}\mathscr{R}^kx_{n}$, et il en découle, par $(4)$, que $h(x_{n+1}) \geq h(x_{n})+k),$ et, comme ici, pour tout $n \geq n_{0}, h(x_{n+1}) = h(x_{n})$, cela impose que $k=0$, et donc $x_{n+1}\mathscr{R^0x_{n}}$, c’est-à-dire que $x_{n+1} = x_{n}$, et établit que la suite $(x_{n})$ est constante au-delà du rang $n_{0}$. 
> 
> On a ainsi montré que toute suite décroissante d’éléments de $X$ est nécessairement stationnaire, ce qui établit que l’ordre $\leq_{X}$ est bien fondé.

>[!cour]
>L'ordre $\leq_{X}$ étant bien fondé +, on en déduit le <font color="red"><u>principe d'induction</u></font> pour les ensembles inductifs :
>
>Soit $P$ une propriété sur $X$ telle que :
> - $\forall x_{0} \in B, P(x_{0})\text{ vraie}$
> - $\forall r \in R$ d'arité $m$, $\forall(x_{1},\dots,x_{m})\in X^m,(\forall i \in [\![1,r]\!],P(x_{i}))\implies(P(r(x_{1},x_{2},\dots,x_{m})))$
>   Alors $\forall x \in X, P(x)\text{ vraie}$
> 
>Il s'agit ici de l'analogue du principe de récurrence faible :
> - $\color{cyan}\text{si P est vraie sur les éléments de B (assertions)}$
> - $\color{green}\text{si lorsque } \color{red} \boxed{\color{green}\text{x est construit à partir d'élément de }x_{1},x_{2},\dots,x_{m}\text{ pour lesquels P est vraie}}$
>   $\color{green}\text{alors P vraie pour x}$
>On en conclut $P$ vraie pour tout $x$ de $X$
>
>L'analogue de la récurrence forte serait (cf. théorème de l'induction bien bien fondée avant dans le cour.)
>$$(\forall x \in X, \underbrace{(\forall y \in X, y <_{X}x \implies P(y))}_{\text{si P vraie sur tous les prédécesseurs de x}}\implies \underbrace{P(x)}_{\text{alors P(x) vraie}}) \implies (\forall x \in X,P(x))$$
>et si $x$ n'admet pas de prédécesseur : $P(x)$ vraie 

>[!example] Montrer que tout mot du langage de Dyck possède autant de parenthèses ouvrantes que fermantes
> -<u>Langage de Dyck</u> :
>  - - éléments de base : le mot vide $\epsilon$ $B={\epsilon}$[^6]
>  - - règles d'inférence : $\cases{r_{1}(x) = (x)\\ r_{2}(x,y) = xy}$[^7]
>
><u>Notons</u>, pour tout $x \in X$ ($X$ : ensembles des mots du langage de Dyck)
>$P(x)$ la propriété "$x$ comporte autant de parenthèses ouvrantes que fermantes"
>
> - <u>Initialisation</u> : vrai pour le mot vide (*aucune parenthèse*)
> - <u>Hérédité</u> : Supposons que $P$ est vraie pour un certain $x$ et un certain $y$ de $X$ (hypothèse d'induction, H.I) alors :
>    - $(x)$ contient *une parenthèse $($ et une $)$ de plus que $x$* et $x$ vérifie $P$ donc $(x)$ vérifie $P$
>   - le nombre de parenthèses ouvrantes (resp. fermantes) dans $xy$ est *la somme des nombre de telles parenthèses* dans $x$ et dans $y$.
>    donc, si $x$ et $y$ vérifient $P$, $xy$ vérifient $P$

### 3)<u>Fonctions définies par induction</u> :

>[!cour]
>Sur un ensemble défini par induction, on défini une fonction en la définissant sur les éléments de base ($B$), et en définissant, pour chaque règle d'inférence $r \in R$,
>$$f(r(x_{1},x_{2},\dots ,x_{m})) \text{en fonction des }x_{i}\text{ et des }f(x_{i}), 1\leq i \leq m$$

>[!example] Exemple : longueur d'une liste chaînée
>$$\cases{len([ ]) = 0 \\ len(x:: lst) = 1 + len(lst)}$$

>[!note] N.B
>Définir ainsi une fonction n'est possible que s'il n'existe qu'une unique façon de construire un élément $x \in X$



[^1]: $\forall n \in \mathbb{N},P(n) vraie \implies P(n+1) vraie$

[^2]: suite constante à partir d'un certain rang.
	càd : $(u_{n})_{n \in \mathbb{N}}\in E^{\mathbb{N}},\exists \alpha \in E,\exists n_{0}\in \mathbb{N},\forall n\geq n_{0}, u_{n}=\alpha$

[^3]: $(1)$ et $(2)$

[^4]: ordre du dictionnaire mais sur des n-uplets

[^5]: nombre de variables de la fonction

[^6]: mettre des parenthèses autour d'un élément déjà construit

[^7]: accoler deux éléments déjà construits 
---
#Informatique #cours 
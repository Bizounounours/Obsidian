# I. Syntaxe des formules propositionnelles

> [!definition] Definition 1
> Soit $\mathbb{V}$ un ensemble dénombrable, dont les éléments sont appelés **variables** (*propositionnelles*).
> 
> L'**ensemble des formules propositionnelles** sur $\mathbb{V}$ est défini inductivement par :
> - $B=\mathbb{V} \cup \{ \top, \bot \}$  [^1]
> - Si $\phi$ et $\psi$ sont des formules[^2] alors : 
>   - $\lnot \phi$ est une formule; (non phi)
>   - $\phi \wedge \psi$ est une formule; (phi et psi)
>   - $\phi \vee \psi$ est une formule; (phi ou psi)
>   - $\phi \to \psi$ est une formule; (phi implique psi)
>   - $\phi \leftrightarrow \psi$ est une formule; (phi équivaut psi)

> [!example] Exemple de formule
> $(\lnot ((\psi \wedge \phi) \psi))$où $\phi$ et $\psi$ sont aussi des formules
> 
> On parle de **formule stricte** lorsque tous les parenthèsages sont bien présents, ceci est l'écriture canonique des formules propositionnelles

> [!example] Autre exemple
> Si $\mathbb{V} = \{v_{1}, v_{2}, v_{3}\}$
> Alors une formule possible est :
> $$((\lnot(v_{1} \wedge v_{2}))\vee (\lnot v_{3}))$$

> [!example] Implémentation possible en OCaml
> ```ocaml
> type formule = Variable of Int (* ici on reprèsente les variables par des entiers, ex 1 au lieu de v1 *)
> 	| Top
> 	| Bottom
> 	| Non of formule
> 	| Et of formule * formule
> 	| Ou of formule * formule
> 	| Impl of formule * formule
> 	| Eq of formule * formule
> ```

Fondamentalement toute formule s'écrit à l'aide des variables (éléments de $\mathbb{V}$) de $\top$,$\bot$ des connecteurs binaires ($\wedge,\vee,\to,\leftrightarrow$) et du correcteur unaire $\lnot$.

> [!example] Représentation sous forme d'arbre
> Toute formule propositionnelle peut se représenter par un arbre selon le principe suivant :
> - Chaque feuille est étiquetée par un élément de base (variable ou constante $\top$ ou $\bot$)
> - Chaque noeud interne est étiqueté par une règle d'inférence (un connecteur logique)
>   
> Pour $((\lnot(v_{1} \wedge v_{2}))\vee (\lnot v_{3}))$ :
> ```mermaid
> graph TD;
> id1((or))-->id2((not))-->id3((and))-->id4((v1));
> id3-->id5((v2));
> id1-->id6((not))--> id7((v3));
> ```
> 
> A chaque formule correspond ainsi un arbre unique ce qui définit une injection (*pas plus d'un antécédent pour un arbre donné*).

> [!abstract] Définition 2
> On défini inductivement :
> - La taille d'une formule $\phi$, notée $|\phi|$ :
>   - $|v|=0$, $|\top|=0$,$|\bot|=0$ [^1]
>   - $|\lnot \phi| = 1 + |\phi|$, $|\phi \wedge \psi| = 1 + |\phi| + |\psi|$ (*de même pour $\vee$, $\to$ et $\leftrightarrow$*) [^2]
>- La hauteur d'une formule $\phi$, notée $h(\phi)$ :
>   - Pour tout $v$ de $\mathbb{V}$, $h(v)=0$, $h(\top)=0$, $h(\bot)=0$ [^1]
>   - $h(\lnot \phi)=1+h(\phi)$, $h(\phi \diamond \psi)=1 + \max (h(\phi),h(\psi))$ où $\diamond \in \{\vee,\wedge,\to,\leftrightarrow\}$ [^2]
 
> [!tip] La taille d'une formule est égale au nombre de connecteurs qu'on y trouve.
> 
> Sur l'exemple précédent :
> ```mermaid
> graph TD;
> id1((or))-->id2((not))-->id3((and))-->id4((v1));
> id3-->id5((v2));
> id1-->id6((not))--> id7((v3));
> ```
> 
> Taille : 4
> Hauteur : 3

> [!abstract] Sous-formule
> On définit inductivement les sous-formules d'une formule, soit $A$, $B$ des formules et $\diamond \in \{\vee,\wedge,\to,\leftrightarrow\}$ :
> - Une formule est une sous-formule d'elle-même
> - $A$ est une sous-formule (*immédiate*) de $(\lnot A)$
> - $A$ et $B$ sont des sous-formules (*immédiates*) de $A \diamond B$
> - Toute sous-formule d'une sous-formule d'une formule $A$ est une sous-formule de $A$
>
>> [!tip] Un sous-formule d'une forme correspond ainsi à un sous-arbre de l'arbre représentant la formule.
# II. Sémantique des formules propositionnelles

> [!abstract] Ensemble des valeurs de vérité
> On note $\mathscr{B} = \{F,V\}$ l'**ensemble de valeurs de vérité** où $V$ désigne le vrai et $F$ désigne le faux.

> [!abstract] Valuation
> Une **valuation** sur $\mathbb{V}$ (*ens de variables*) est une application (*parfois partielle*) $v : \mathbb{V} \to \mathscr{B}$ 
>
>> [!tip] Une valuation est ainsi un moyen d'attribuer une valeur de vérité à tout ou partie des variables propositionnelles

> [!example] Exemple
> 
>```handdrawn-ink
>{
>	"versionAtEmbed": "0.3.4",
>	"filepath": "Asset/Ink/Drawing/20d 166.2 - 9.02am.drawing",
>	"width": 500,
>	"aspectRatio": 1
>}
>```

> [!abstract] Définition
> Soit $\phi$ une formule propositionnelle sur un ensemble de variables $\mathbb{V}$.
> 
> Toute valuation $v$ définie sur $\mathbb{V}$, permet d'associer à $\phi$ une valeur de vérité calculée inductivement à partir des règles suivantes (*tables de vérité des connecteurs*) :[^3]

| $P$ | $Q$ | $\lnot P$ | $P \wedge Q$ | $P \vee Q$ | $P \to Q$ | $P \leftrightarrow Q$ |
| --- | --- | --------- | ------------ | ---------- | --------- | --------------------- |
| F   | F   | V         | F            | F          | V         | V                     |
| F   | V   |           | F            | V          | V         | F                     |
| V   | F   | F         | F            | V          | F         | F                     |
| V   | V   |           | V            | V          | V         | V                     |

On notera $\bar{v}(\phi)$ la valeur de vérité ainsi associée à $\phi$.

> [!example] Exemple
> $\phi = (p \wedge q) \to (p \vee r)$ où $\mathbb{V} = \{ p,q,r \}$
> 
> On peut calculer les valeurs de vérité de $\phi$ pour toute valuation $v$ sur $\mathbb{V}$ grace à une table de vérité.

> [!tip] On pourra implémenter en OCaml, les fonctions taille, hauteur, et le calcul de $\bar{v}(\phi)$ en fonction de $\phi$ et $v$.
# III. Satisfiabilité d'une formule

> [!abstract] Définition
> Soit $\phi$ une formule d'un ensemble de variables $\mathbb{V}$.
> 
> Une valuation $v$ de $\mathbb{V}$ est un **modèle** de $\phi$ (*on dit "satisfait" $\phi$*) si $v$ associe à $\phi$ la valeur de vérité $V$. cad que $\bar{v}(\phi)=\mathscr{V}$.
> 
> On notera alors : $v \models \phi$ (*on lit $v$ satisfait $\phi$ ou "est un modèle de $\phi$"*)
> 
> On dit qu'une formule propositionnelle est **satisfiable** (*satisfaisable*)  si elle admet un modèle.
> 
> L'**ensemble de modèles** d'une formule $\phi$ est l'ensemble de ses modèles.

> [!abstract] Définition
> Une formule propositionnelle $\phi$  sur un ensemble de variables propositionnelles $\mathbb{V}$ est une **tautologie** (resp. **antilogie**) si toue (resp. aucune) valuation est un modèle de $\phi$.
> 
>> [!tip] Ainsi la dernière colonne de la table de vérité d'une tautologie ne contient que des $V$ (resp. $F$)

> [!info] Une formule $\phi$ est une tautologie ssi ($\lnot \phi$) est une antilogie
>> [!note] Démo immédiate

> [!danger] Important
> $\phi \vee (\lnot \phi)$ où $\phi$ est une tautologie connue sous le nom de **tiers-exclu**.

> [!example] Exemple
> - Une application du principe de tiers-exclu 
>   
>   On note $\phi$ l'énoncé "$\sqrt{ 2 }^{\sqrt{ 2 }}$ est rationnel" alors, d'après le principe du tiers-exclu, $\phi$ est vraie ou $\phi$ est fausse
>   
>   - Si $\phi$ est vraie, on apprend qu'il existe deux irrationnels ($x = \sqrt{ 2 },y = \sqrt{ 2 }$ ) tel que $x^y$ est rationnel;
>   - Si $\phi$ est faux cad si $\sqrt{ 2 }^{\sqrt{ 2 }}$  est irrationnel, noté $a$ alors $a^\sqrt{2} = (\sqrt{ 2 }^{\sqrt{ 2 }})^\sqrt{ 2 }=\sqrt{ 2 }^{\sqrt{ 2 }\times \sqrt{ 2 }} = \sqrt{ 2 }^2=2$ et on a donc $x = a = \sqrt{ 2 }^{\sqrt{ 2 }}$ irrationnel et $y = \sqrt{ 2 }$ irrationnel tel que $x^y$ rationnel.[^4]
>     
>     On a remarqué soit $\sqrt{ 2 }^{\sqrt{ 2 }}$ soit $(\sqrt{ 2 }^{\sqrt{ 2 }})^\sqrt{ 2 }$ rationnel.

> [!abstract] Formules sémantiquement équivalentes
> Deux formules propositionnelles sur le même ensemble de variables sont dites **équivalentes** si elle admettent le **même ensemble de modèle**.
> 
> On note alors $\phi = \psi$.
> 
>> [!tip] Elles admettent la même table de vérité

> [!info] $\phi \equiv \psi \leftrightarrow  \phi \leftrightarrow \psi$ est une tautologie
>
> >[!note] Laissé aux lecteurs-lectrices

> [!example] Exemple
> Si $\phi$ formule propositionnelle alors $(\phi \to \bot) \equiv \lnot \phi$

> [!abstract] Liste des équivalences à connaitre
> - [[Loi de De Morgan]] : 
>   $$\begin{align}
>   \lnot(p \wedge q) \equiv (\lnot p)\vee(\lnot q) \\
>   \lnot(p \vee q) \equiv (\lnot p)\wedge(\lnot q)
>   \end{align}$$
> 
> - Equivalences sémantiques relatives à l'implication :
>   $$\begin{align}
>   &\phi \to \psi \equiv \lnot \phi \vee \psi &\text{ (Implication)} \\
>   &\phi \to \psi \equiv \lnot \psi \to \lnot \phi &\text{ (Contraposition)} \\
>   &(\phi \wedge \psi) \to \theta \equiv \phi \to (\psi \to \theta) &\text{ (Curryfication)} \\
>   \end{align}$$
>   
> - Equivalences sémantiques relatives à la négation :
>   $$\begin{align}
>   &\phi \wedge \lnot \phi \equiv \bot &\text{ (Non-contradiction)} \\
>   &\phi \vee \lnot \phi \equiv \top &\text{ (Tiers exclu)} \\
>   &\lnot \lnot \phi \equiv \phi &\text{ (Double négation)}
>   \end{align}$$
>   
> - $\top$ est le neutre pour la conjonction ($\wedge$) et l'élément absorbant pour la disjonction ($\vee$)
>   $$\begin{align}
>   &\phi \wedge \top \equiv \phi \\
>   &\phi \vee \top \equiv \top
>   \end{align}$$
> - $\bot$ est le neutre pour la conjonction ($\vee$) et l'élément absorbant pour la disjonction ($\wedge$)
>   $$\begin{align}
>   &\phi \vee \bot \equiv \phi \\
>   &\phi \wedge \bot \equiv \bot
>   \end{align}$$
> - La conjonction et la disjonction sont commutatives
>   $$\begin{align}
>   &\phi \wedge \psi \equiv \psi \wedge \phi \\
>   &\phi \vee \psi \equiv \psi \vee \phi
>   \end{align}$$
> - La conjonction **seule** est associative
>   $$\begin{align}
>   &(\phi \wedge \psi) \wedge \theta \equiv \phi \wedge (\psi \wedge \theta) \\
>   \end{align}$$
> - La disjonction **seule** est associative
>   $$\begin{align}
>   &(\phi \vee \psi) \vee \theta \equiv \phi \vee (\psi \vee \theta) \\
>   \end{align}$$
> - La conjonction est distributive par rapport à la disjonction et réciproquement.
> - Idem potence
>   $$\begin{align}
>   \phi \vee \phi = \phi \\
>   \phi \wedge \phi = \phi
>   \end{align}$$

> [!abstract] Conséquence logique
> Soient $\phi$ et $\psi$ sont deux formules propositionnelles, on dit que $\psi$ est la **conséquence logique** de $\phi$ si tout modèle de $\phi$ est un modèle de $\psi$.
> 
> C'est-à-dire lorsque toute valuation $v$ telle que $\bar{v}(\phi)=\mathscr{V}$ vérifie $\bar{v}(\psi)=\mathscr{V}$ ou encore si $\forall v \in \mathbb{V}, (\bar{v}(\phi)=\mathscr{V})\implies(\bar{v}(\psi)=\mathscr{V}$

> [!example] Exemple
> Parmi les affirmations suivantes lesquelles sont vraies : $x,y$ étant des variables propositionnelles.
> 
> $$\begin{align}
> &x \underbrace{ \models }_{ ? } x \vee y \\
> &x \vee y \underbrace{ \models }_{ ? } x \\
> &x \wedge (x \to y) \underbrace{ \models }_{ ? } y
> \end{align}$$
>
| $x$ | $y$ | $x\to y$ | $x\wedge(x\to y)$ |
| --- | --- | -------- | ----------------- |
| F   | F   | V        | F                 |
| F   | V   | V        | F                 |
| V   | F   | F        | F                 |
| V   | V   | V        | V                 |
>
> Donc la 3 est vraie.

> [!abstract] Definition
> On étend ces définitions à un ensemble de formule $\Gamma$ :
> - Une valuation est un **modèle d'un ensemble de formule** $\Gamma$, si c'est un modèle de chaque formule de $\Gamma$.
> - Une formule $\phi$ est une conséquence logique de $\Gamma$, si toute valuation qui est un modèle (*de toutes les formules*) de $\Gamma$ est un modèle de $\phi$.
>   
> On note alors $\Gamma \models \phi$ et si $\Gamma = \{ \phi_{1}, \phi_{2},\dots ,\phi_{n}\}$ on peut aussi noter $\phi_{1},\phi_{2},\dots, \phi_{n} \models \phi$

> [!example] Exemple
> $p, p\to \lnot q \models \lnot q$
> Car
>
| $p$   | $q$ | $p\to \lnot q$ | $\lnot q$ |
| ----- | --- | -------------- | --------- |
| F     | F   | V              | V         |
| F     | V   | V              | F         |
| **V** | F   | **V**          | **V**     |
| V     | V   | F              | F         |
>
> On ne regarde que les lignes où toutes les formules sont vraies.

> [!tip] Pour une tautologie $\phi$, on notera $\models \phi$

> [!info] $(\phi \models \psi) \text{ ssi } (\models \psi \rightarrow \phi )$
>> [!note] Aux lecteurs-lectrices

> [!info] Une formule propositionnelle est une tautologie ssi elle est conséquence logique de tout ensemble de formules.

> [!info] $\psi \equiv \phi \text{ ssi } \psi \models \phi \text{ et } \phi \models \psi$
# IV. Formes normales
## 1. Formes normales négatives (FNN)

> [!abstract] FNN
> Les négations ne portent que sur les variables

> [!example] Exemple
> $$\phi = (p \wedge \lnot r) \to (\lnot p \wedge \lnot (q \wedge \lnot r))$$
> 
> On souhaite que les noeuds soient uniquement occupés par $\vee$ ou $\wedge$ et ramener les négations aux feuilles. 
> 
> $$ \begin{align}
> \phi &\equiv \lnot (p \wedge \lnot r) \vee (\lnot p \wedge \lnot(q \wedge \lnot r)) \\
> &\equiv ((\lnot p) \vee (\lnot \lnot r)) \vee (\lnot p \wedge (\lnot q \vee ( \lnot \lnot r))) \\
> &\equiv (\lnot p \vee r) \vee ( \lnot p \wedge ( \lnot q \vee r))
>  \end{align}
> $$
> 
> ```mermaid
> graph TD;
> id1((V))-->id2((V))-->id3((not))-->id4((p));
> id2-->id5((r));
> id1-->id6((^))-->id7((not))-->id8((p));
> id6-->id9((V))-->id10((not))-->id11((q));
> id9-->id12((r))
> ```

> [!abstract] Littéral
> On appelle **littéral** une formule qui est une variable propositionnelle (*littéral positif*) ou la négation d'une variable propositionnelle (*littéral négatif*).

> [!abstract] Définition
> On définit les formes normales négatives (*FNN*) inductivement :
> - Les assertions (*éléments de base*) sont : littéraux
> - Les règles d'inférences sont : $(\phi,\psi) \mapsto (\phi \wedge \psi);(\phi,\psi) \mapsto (\phi \vee \psi)$
>   
>   Si $\phi$ et $\psi$ sont des FNN alors $\phi \wedge \psi$, $\phi \vee \psi$ sont des FNN.

> [!info] Toute formule $\phi$ admet une écriture sous forme de FNN[^5]
> >[!note] Démo
> > Par induction en utilisant ce qui a été utilisé dans l'ex. (formules sémantiquement équivalentes à $\leftrightarrow$ et $\to$, de Morgan, double-négation) 

> [!example] Donner une FNN équivalente à $\lnot (p \leftrightarrow q)$
>> [!tip] On passe facilement d'une FNN équivalente à une formule $\phi$ à une FNN équivalente à $\lnot \phi$
>> En changeant les littéraux en leurs opposés et en échangeant conjonction et disjonction.

> [!example] $\phi \equiv (\lnot p \vee r) \vee (\lnot p \wedge ( \lnot q \vee r))$
> $\lnot\phi \equiv (p \wedge \lnot r) \wedge (p \vee ( q \wedge \lnot r))$

## 2. Formes normales conjonctives (FNC)

> [!abstract] Clause disjonctive
> Une **clause disjonctive** est une disjonction de littéraux

> [!example] $\lnot p \vee q \vee \lnot r$

> [!abstract] Définition
> Une FNC est une **conjonction de clause disjointes**.

> [!example] $(\lnot p \vee r) \wedge (\lnot p \vee q \vee \lnot r) \wedge (p \vee q)$

> [!tip] On peut obtenir une FNC à partir d'une FNN
> En appliquant les équivalences sémantiques de distributivité, associativité et commutativité.

> [!example] $\phi = (\lnot p \vee r ) \vee (\lnot p \wedge ( \lnot q \vee r ))$

> [!danger] La taille d'une FNC obtenue par ses méthodes peut être exponentielle en la taille de la formule de départ.

> [!example] $\phi_{n}= V_{i \in [\![1,n]\!]}(p_{i \wedge q_{i}})$
> Sur l'ensemble de variables propositionnelles $\{p_{i},q_{i},i \in [\![1,n]\!]$
> 
> On peut montrer que FNC ($\phi_{n}$) comporte $2^n$ clauses.
## 3. Formes normales disjonctives

> [!abstract] [[Forme normale disjonctive]]
> - Une **clause conjonctive** est une conjonction de littéraux.
> - Une **forme normale disjonctive** (\*) est une disjonction de clauses conjonctives.

> [!example] $\underbrace{ (p \wedge \lnot q \wedge \lnot r) }_{ \text{clause conjonctive} } \vee \underbrace{ (\lnot p \wedge r) }_{  } \vee \underbrace{ q }_{  }$

On peut passe de FNC à FND en appliquant la distributivité :
$$\begin{align}
\phi &\equiv (\lnot p \vee r) \wedge (\lnot p \vee \lnot q \vee r) \\
&\equiv ((\lnot p \vee r) \wedge \lnot  p) \vee ((\lnot p \vee r) \wedge \lnot q) \vee ((\lnot p \vee r) \wedge r)\\
&\equiv (\lnot p \wedge \lnot p) \vee (r \wedge \lnot p) \vee (\lnot p \wedge \lnot q) \vee (r \wedge \lnot q) \vee (\lnot p \wedge r) \vee (r \wedge r) \\
&\equiv \lnot p \vee (r \wedge \lnot p) \vee (\lnot p \wedge \lnot q) \vee (r \wedge \lnot q) \vee (\lnot p \wedge r) \vee r
\end{align}$$
On peut directement obtenir l'écriture d'une formule $\phi$ sous forme de FND à partir de sa table de vérité.

> [!example] [[TD 16 - Sémantique de la logique propositionnelle#Exercice 3|Ex 3 TD 16]]
> 
>
| $p$ | $q$ | $r$ | $\phi$ |
| --- | --- | --- | ------ |
| F   | F   | F   | F      |
| F   | F   | V   | V      |
| F   | V   | F   | V      |
| F   | V   | V   | F      |
| V   | F   | F   | V      |
| V   | F   | V   | F      |
| V   | V   | F   | F      |
| V   | V   | V   | V      |
>
>Chaque ligne décrivant une valuation rend vraie une seule clause conjonctive impliquant toutes les variables.
>
>$\phi$ est vraie uniquement pour les valuations telles que
>
>Ex :
>Ligne 2 : $\lnot p \wedge \lnot q \wedge r$
>Ligne 3 : $\lnot p \wedge q \wedge \lnot r$
>Ligne 5 : $p \wedge \lnot q \wedge \lnot r$
>Ligne 8 : $p \wedge q \wedge r$
>
>En mettant des $\vee$ entre ces expressions, cette FND est vraie ssi au moins une d'entre elle est vraie
>
>Or si l'une d'entre elle est vraie, les autres sont nécessairement fausses donc seules les valuations des lignes 1,2,3,4 rendent la FND vraie.
>
>La FND est donc sémantiquement équivalente à $\phi$.

## 4. Représentation en OCaml
```ocaml
type variable = int
type litteral = Pos of variable | Neg of variable
type clause = litteral list (*sous entendu liste de litteraux dont on forme la disjonction (resp. conjonction) si on veut construire des FNC (resp. FND)*)
type FNC (*Ou FND*) = clause list
```

*cf notebook [a29b-11248893](https://capytale2.ac-paris.fr/p/basthon/n/?kernel=ocaml-legacy&mode=assignment&id=11284085&extensions=linenumbers)*

```ocaml
let phi = [
	[Neg(0),Pos(2)],
	[Neg(0),Neg(1),Pos(2)] (*en prenant 0,1,2 pour p,q,r*)
]
```
# V. Le problème SAT
La satisfiabilité d'une formule permet de savoir si un problème modélisé par une formule logique (ex: un [[TP 25|sudoku]]) admet une solution ou non.
## 1. Définition
> [!abstract] Problème SAT
> - **Entrée** : Une formule propositionnelle $\phi$
> - **Sortie** : V (*ou 1*) si $\phi$ est satisfiable, F (*ou 0*) sinon.
> Ce problème se classe dans la catégorie des problèmes de décision (*sortie binaire*).
> C'est un problème difficile à résoudre : il est de la classe des problèmes. NP-Complet (n'a pas a priori de solution en temps polynomial).

> [!abstract] Problème k-SAT
> - **Entrée** : une FNC $\phi$ dont les clauses ont $k$ littéraux ou moins
> - **Sortie** : 0 ou 1 (V ou F) selon que $\phi$ est satisfiable ou non

> [!example] Coloriage d'une carte
> On dispose de quatre couleurs pour colorier une carte : $c \in \{1,2,3,4\}$ avec la contrainte que deux pays qui ont une frontière commune (non réduite à un ou plusieurs points isolés) ne soient pas coloriés de la même couleur.
> 
> On se donne les variables propositionnelles suivantes :
> $$x_{i,c} : \text{ vraie si le pays i est colorié avec c}$$
> 
> Les contrainte sont les suivantes :
> - chaque pays doit avoir (*au moins*) une couleur :
>   $$\forall i, x_{i,1}\vee x_{i,2}\vee x_{i,3} \vee x_{i,4}$$
> - chaque pays doit avoir au plus une couleur :
>   $$\forall i, \forall c, \forall c', \lnot x_{i,c} \vee \lnot x_{i,c'} \equiv \lnot(x_{i,c} \wedge x_{i,c'})$$
> - deux pays adjacentes doivent avoir des couleurs différentes :
>   
>   Si deux pays $R_{i}$ et $R_{j}$ sont adjacentes : $\forall c, \lnot x_{i,c} \vee \lnot x_{j,c}$ cad $\lnot (x_{i,c} \wedge x_{j,c}$
> 
> Il s'agit de déterminer s'il existe une valuation sur l'ens de variables $\{x_{i,c}\}_{\begin{align}&1\leq i\leq n \\ &1 \leq c \leq c\end{align}}$ qui rend vraie la conjonction de toutes ces formules.
## 2. Résolution
### A. Force-brute
 Pour une formule $\phi$ comportant $n$ variables, on $2^n$ valuations possibles.
 
 Si on les teste exhaustivement, l'évaluation d'une formule ayant une complexité en $O(n)$ (*taille de l'arbre implémentant la fonction de valuation, et qu'en chaque noeud interne, on doit évaluer le connecteur en fonction de la valeur de vérité de ses fils*)
 
 Ainsi l'algorithme en force brute a une complexité (*peu pratiquable*) en $O(n2^n)$
#### a. Algorithme en OCaml
```ocaml
let rec f_eval v phi = match phi with
    | Variable x -> v x
    | Top -> true
    | Bottom -> false
    | Non psi -> not (f_eval v psi)
    | Et (psi1, psi2) -> (f_eval v psi1) && (f_eval v psi2)
    | Ou (psi1, psi2) -> (f_eval v psi1) || (f_eval v psi2)
    | Impl (psi1, psi2) -> not (f_eval v psi1) || (f_eval v psi2)
    | Eq (psi1, psi2) -> (not (f_eval v psi1) || (f_eval v psi2)) && (not (f_eval v psi2) || (f_eval v psi1))
```

```ocaml
let satifiabilite phi n = 
    let valuation = Array.make n false in
    let rec aux i = match i with
        | -1 -> let v x = valuation.(x) in f_eval v phi
        | _ -> if aux (i - 1) then true
        else (valuation.(i) <- true; aux (i - 1))
    in 
    aux (n - 1)
```

1er appel `aux 2` renvoie ce que renvoie `aux 1` (qui appelle `aux 0` etc pour cela) si `aux 1` renvoie vrai.
![[Drawing 2026-06-09 09.44.00.excalidraw|1000x10]]
![[Drawing 2026-06-12 08.15.43.excalidraw|1000x10]]
La hauteur de l'arbre des appels donne la hauteur maximale de la pile des  appels récursifs (*cad le nombre maximal d'appels encore non terminés*).[^6]

### B. Algorithme de Quine

> [!abstract] [[Substitution]]
> Soient $\phi$ et $\psi$ deux formules propositionnelles $p$ une variable propositionnelle.
> 
> La substitution de $p$ par $\psi$ dans $\phi$  est la formule obtenue en remplaçant chaque occurrence de $p$ dans $\phi$ par $\psi$.
> 
> On la note $\phi[\psi / p]$ on lira **$\phi$ dans laquelle $\psi$ remplace $p$**.

Pour simplifier une FNC $\phi$, on pourra la remplacer par une formule sémantiquement équivalente, en appliquant les règles suivantes :
- Si une clause contient la constante $\top$ (*littéral*), elle est satisfaite et peut être supprimée de la formule
- Inversement si une clause contient la constant $\bot$, on peut la supprimer de la clause, **sauf si elle est seule**.

> [!note] [[Algorithme de Quine]]
> - [[Entrée]] : une formule $\phi$ sous la forme d'une FNC
> - [[Sortie]] : Vraie (*1*) si $\phi$ est satisfiable, Faux (*0*) sinon
>   
> 1. On simplifie chaque clause (*cf précédemment*) 
> 2. Si $\phi$ ne contient aucune clause, renvoyer Vrai
> 3. Si $\phi$ contient la clause $\bot$, renvoyer Faux
> 4. Choisir la prochaine (*une nouvelle*) variable propositionnelle $p$ qui qpparait dans une clause de $\phi$
>    - Si $\text{Quine}(\phi [\bot / p])$ est vrai, retourner Vrai
>    - Sinon retourner $\text{Quine} ( \phi [\top / p ]$
>
> >[!tip] Rappel
> >- $\phi [ \bot / p]$ (*substitution*) : $\phi$ dans laquelle $\bot$ remplace $p$.
> >- $\phi [\top / p ]$ (*substitution*) : $\phi$ dans laquelle $\top$ remplace $p$.

> [!example] $\phi = (p_{1} \vee p_{2}) \wedge (\lnot p_{1} \vee \lnot p_{2}) \wedge (p_{2} \vee \lnot p_{3})$
> $\text{Quine}(\phi)$ :
> 1. Rien à faire
> 2. Non
> 3. Non
> 4. On choisit $p_{1}$
>    - On remplace $p_{1}$ par $\bot$ dans $\phi$ :
>      1. $\begin{align} &\text{Quine}((\bot \vee p_{2}) \wedge (\lnot bot \vee \lnot p_{2}) \wedge (p_{2} \vee \lnot p_{3})) \\ &\text{Quine}(p_{2} \wedge (p_{2} \vee \lnot p_{3})) \end{align}$
>	  2. RAS
>	  3. RAS
>	  4. On choisit $p_{2}$ :
>	     - On remplace $p_{2}$ par $\bot$
>	       1. $\begin{align} &\text{Quine}(\bot \wedge (\bot \vee \lnot p_{3})) \\ &\text{Quine}(\bot) \end{align}$
>	       2. Rien car $\phi$ contient une clause
>	     - On remplace $p_{2}$ par $\top$
>	       1. $\text{Quine}(\top \wedge (\top \vee \lnot p_{3}))$
>	       2. Formule vide (*ne contient aucune clause*)
>	       3. On renvoie Vrai
>    - Renvoyer vrai 
> 
> >[!tip] Terminaison
> > On a comme [[Variant d'appel]] le nombre de variable dans la formule à tester. (*à chaque appel récursif une variable est éliminée par substitution*)
>
> > [!tip] Correction
> > $\phi$ est sémantiquement équivalente à :
> > $$(\phi \wedge p_{1}) \vee (\phi \wedge \lnot p_{1}) \text{ (tiers-exclu)}$$
> > $\phi$ est satisfiable s'il existe une valuation $v$ telle que :
> > $$\bar{v}((\phi \wedge p_{1}) \vee (\phi \wedge \lnot p_{1})) = V$$ 
> > Or ceci est vrai (*règle de l'évaluation inductive des formules*) 
> > ssi $\bar{v}(\phi \wedge p_{1}) = V$ [^7]
> > ou $\bar{v}(\phi \wedge \lnot p_{1}) = V$ [^8]
> > 
> > Donc **Hypothèse de récurrence sur le nombre de variables** : Quine est correct sur tout prédécesseur de $\phi$ 
> > 
> > **Initialisation** : Quine correct sur les variables propositionnelles et les constantes (*formules à une variable ou moins*)



[^1]: Ensemble de base

[^2]: Règles d'inférences

[^3]: Si on définit comme connecteur de base (règle d'inférence) uniquement $\lnot$, $\wedge$, $\vee$ les tables de $P\to Q$ et $P \leftrightarrow Q$ se déduisent de celles de $\lnot$, $\wedge$, $\vee$ 

[^4]: On a prouvé qu'il existe deux irrationnels tels que $x^y$ est rationnel

[^5]: C'est-à-dire qu'il existe une FNN sémantiquement équivalente

[^6]: Il est stocké dans le [[contexte de la fonction]]

[^7]: Vérifié ssi $\phi[T / p_{1}]$ est satisfiable résolu par l'appel récursif de Quine

[^8]: Vérifié ssi $\phi [ \bot / p_{1}]$ est satisfiable par l'appel n2 de Quine

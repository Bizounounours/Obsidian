On cherche dans un texte *T* un motif *M* :

| T   | <   | <   | <     |
| --- | --- | --- | ----- |
| $0$ | $1$ | ... | $n-1$ |

| M   | <   | <   | <     |
| --- | --- | --- | ----- |
| $0$ | $1$ | ... | $m-1$ |
avec $n$ la longueur du texte et $m$ la longueur du motif
# Recherche de motif
## 1. Algorithme naif
On parcourt le texte et à chaque position on recherche le motif

| T     | <   | <     |
| ----- | --- | ----- |
| $i=0$ | ... | $n-1$ |

| M     | <   | <     |
| ----- | --- | ----- |
| $j=0$ | ... | $m-1$ |
Pour tout $i \in [\![0,n-m]\!]$m on teste si $T[i:i+m] = M$[^1]

| T   | <         | <   | <   |
| --- | --------- | --- | --- |
| ... | $i_{max}$ | ... | $n$ |
$i_{max}$ est le $i$ tel que $i+m=n$ donc $i_{max} = n - m$
### A. Algorithme
#### Si on cherche toutes les positions
```
S = Vide
s = 0
Tant que s <= n-m :
	Si T[s:s+m] = M alors :
		S = S union {s}
	s = s + 1
Fin Tant que
Renvoyer S
```

> [!example] Meilleur cas
$\text{T = "aa ... aa"}$
$\text{M = "b ... b"}$
En $O(n-m)$

> [!example] Pire cas
$\text{T = "aa ... aa"}$
$\text{M = "a ... a"}$
En $O(m(n-m))$

#### Si on cherche si le motif est présent
```
s = 0
flag = False
Tant que s <= n-m et flag = False :
	Si T[s:s+m] = M alors :
		flag = True
		renvoyer s
	sinon
		s = s + 1
Fin Tant que
Renvoyer s
```

**Meilleur cas**
$O(n)$ le motif est trouvé au début du mot.

**Pire cas**
$O(nm)$ même que précédemment.
### B. Complexité pire cas

| T     | <   | <     |
| ----- | --- | ----- |
| $i=0$ | ... | $n-1$ |
| a     | a   | a     |

## 2. Algorithme de Bayer-Moore
On peut l'améliorer l'algorithme naif en effectuant un prétraitement du motif.[^2]

### A. Idée
On parcours le texte de gauche à droite mais on parcourt le motif de droite à gauche.

Et on se donne une [[table "de saut"]] : dans laquelle on consigne les positions les plus à droite de chaque lettre dans le motif.

> [!example] Exemple
> $M = \text{"}\underbrace{ \text{adbabb} }_{ \text{0 1 2 3 4 5} }\text{"}$
> 
> **Table de saut**
>
| a   | b   | c   | d   |
| --- | --- | --- | --- |
| 3   | 5   | -1  | 1   |
>
> On parcours le texte de gauche à droite, et à chaque position possible pour le motif, on distingue plusieurs cas.
> 
#### 1er cas
```handdrawn-ink
{
	"versionAtEmbed": "0.3.4",
	"filepath": "Asset/Ink/Drawing/2026.5.26 - 8.35am.drawing",
	"width": 500,
	"aspectRatio": 2
}
```
 Le caractère du motif et du texte coincident :
 On poursuit d'un rang vers la gauche.
 
 Si en poursuivant vers la gauche, on trouve tout le motif :
 
```handdrawn-ink
{
	"versionAtEmbed": "0.3.4",
	"filepath": "Asset/Ink/Drawing/2026.5.26 - 8.45am.drawing",
	"width": 500,
	"aspectRatio": 1.5
}
```

 On poursuit en changeant $i$ en $i+1$ pour chercher le motif à partir de $i+1$ (vers la gauche)

#### 2e cas 
 
 Les deux caractères lus diffèrent :

```handdrawn-ink
{
	"versionAtEmbed": "0.3.4",
	"filepath": "Asset/Ink/Drawing/2026.5.26 - 8.48am.drawing",
	"width": 500,
	"aspectRatio": 1.2
}
```

##### **Si le caractère lu dans le texte est absent du motif**
 
 On peut faire un saut dans le texte car la prochaine occurrence du motif ne peut être qu'au-delà de ce caractère.
 
 Si ce caractère est en $i_{0}$, on poursuit en $i=i_{0}+m$ 
##### **Si son occurrence la plus à droite, est plus à droite encore**
```handdrawn-ink
{
	"versionAtEmbed": "0.3.4",
	"filepath": "Asset/Ink/Drawing/2026.5.26 - 8.58am.drawing",
	"width": 500,
	"aspectRatio": 2
}
```
L'occurrence la plus à droite de $a$ dans $M$ est la 2e.
On poursuit en changeant $i$ en $i+1$.

##### **Le caractère lu dans le texte est présent dans le motif, mais sa 1ere occurrence est plus à gauche**

```handdrawn-ink
{
	"versionAtEmbed": "0.3.4",
	"filepath": "Asset/Ink/Drawing/2026.5.26 - 9.01am.drawing",
	"width": 500,
	"aspectRatio": 2
}
```

On poursuit en cherchant le motif à partir du prochain $i$ pour lequel le caractère est en coincidence avec sa position la plus à droite dans le motif.

> [!example] Autre exemple
> 
>```handdrawn-ink
>{
>	"versionAtEmbed": "0.3.4",
>	"filepath": "Asset/Ink/Drawing/2026.5.26 - 9.08am.drawing",
>	"width": 500,
>	"aspectRatio": 2
>}
>```
>
  
> [!tip] A retenir
> 1. On parcourt le texte et leur motif **en sens inverse**.
> 2. Table de saut
> 3. Cas où le caractère lu n'est pas dans le motif
>    Cas où le caractère a sa *première* occurrence plus à gauche dans le motif.

## 3. Algorithme de Rabin-Karp
Au lieu de comparer un à un les caractères, on utilise une fonction de hachage $h$ afin de comparer le haché d'une tranche de texte $h(T[i:i+m])$ et le haché du motif.

Ce qui permet potentiellement de remplacer la comparaison **caractère pour caractères** ($O(m)$) par une comparaison de haché en $O(1)$).

> [!danger] Le calcul de h(T[i:i+m]) nécessite d'accéder néanmoins à m caractères de T donc son calcul resterait en O(m) en raison des temps d'accès.

On peut contourner ce problème de la façon suivante.

On choisit une fonction de hachage de la forme :
$$\begin{align}
h(\underbrace{ c_{i}c_{i+1}\dots c_{i+m-1} }_{ \text{caractère du motif} })
&=\sum^{m-1}_{j=0}B^{m-1-j}\underbrace{ c_{i+j} }_{ \text{encodé par un entier} }\text{ polynome de degré m-1 en B (un entier "bien choisi")} \\
&= B^{m-1}c_{i}+B^{m-2}c_{i+1}+\dots+B^{m-1-j}c_{i+j}+\dots+B^0c_{i+m-1}
\end{align}
$$
De sorte que lorsque l'on passe de $h(T[i:i+m])$ à $h(T[i+1:i+1+m])$ seuls deux coefficients sont à changer.

$$\begin{align}
h(\underbrace{ c_{i+1}\dots c_{i+m} }_{ \text{caractères de >T[i+1:i+1+m]} })
&=B^{m-1}c_{i+1}+B^{m-2}c_{i+1+1}+\dots+B^{m-1-j}c_{i+1+j}+\dots+B^0c_{i+1+m-1} \\
&=B\times(h(\underbrace{ c_{i}\dots c_{i+m-1}}_{\text{caractères de T[i:i+m]}})-B^{m-1}c_{i})+c_{i+m} \\
\end{align}$$

Annotation [^4]

4 opérations élémentaires (si $B^{m-1}$ stocké en mémoire)

> [!tip] Remarque
> On fera souvent les calculs modulo un certain entier $q$[^3] pour éviter les débordements (calculs sur des entiers)

> [!tip] Remarque
> Après avoir comparé les hachés, on vérifie le motif pour être sur de ne pas avoir affaire à une collision.

# II. Compression
## 1. Généralités

> [!abstract] [[Alphabet]]
> Un **alphabet** est un ensemble $\Sigma$ fini dont les éléments sont des **lettres**.

> [!abstract] [[Mot]]
> Un **mot** sur un alphabet $\Sigma$ est une suite finie (*une séquence*) $m=a_{1}a_{2}\dots a_{n}$ de lettres.
> 
> On appelle **longueur du mot** et on note $|m|$ le nombre de lettres du mot.
> 
> Le **mot vide** est noté $\epsilon$, $|\epsilon|$.
> 
> $\Sigma^n$ : ensemble des mots de longueur $n$.
> 
> $\Sigma^* = \bigcup_{n \in \mathbb{N}}\Sigma^n$ (inclus le mot vide $\Sigma^0={\epsilon}$)
> 
> Un mot $m_{1}$ est un préfixe d'un mot $m_{2}$, s'il existe un mot $m_{3}$ (Éventuellement vide) tel que $m_{2}=m_{1}m_{3}$.

> [!abstract] [[Algorithme de compression sans perte]]
> Un **algorithme de compression sans perte** consiste à définir deux fonctions.
> $f:\Sigma^* \to \Sigma^*$ (*codage*) et $g:\Sigma^*\to \Sigma^*$ (*décodage*) telles que $f \omicron g = id$ et $|f(m)|<|m|$ pour certains mots.
>
> >[!tip] Note
> > En *espérant que* $|f(m)|$ soit petit par rapport à $|m|$ pour les mots du texte à compresser.

> [!info] Théorème 1
> Il **n'existe pas** de fonction injective $f:\Sigma^*\to \Sigma^*$ telles que $|f(m)|<|m|$ **pour tous les mots** de $\Sigma^*$.
> 
> Ainsi on ne peut que chercher à ce que la compression soit efficace pour les mots spécifiques ou les plus fréquents. 
## 2. Algorithme de Huffman
Les textes que l'on manipule en informatique sont toujours d'emblée codés :
- En binaire 
  - Via le [[code ASCII]] (128 ou 256 en étendu) mais pas tous imprimables. Tous les caractères y sont codés sur le même nombre de bits (*7 ou 8*).
  - Via l'[[UTF-8]] où les caractères sont codés avec 4 octets par caractères le plus souvent.

### A. Idée de l'algorithme de Huffman
 - Codage court (*voire très court*) pour les caractères les plus fréquents.
 - Plus long pour les autres, voire pas de codage si le caractère n'apparait pas.

### B. Les étapes de l'algorithme
- **Prétraitement** : on construit un arbre binaire déterminant le codage de chaque caractère (pour une suite de bits) en fonction de sa fréquence dans le texte. 
- **Codage du texte** (*compression*)
- **Décodage** (*qui nécessite de connaitre l'arbre du codage*) 

> [!example] Exemple 2
> On considère le texte "*abracadabra*" (mot sur l'alphabet $\{'a','b',\dots,'z'\}$
> ![[Pasted image 20260529084959.png|50x50]] ![[Pasted image 20260529085227.png|50x50]]
> 
> On ne codera que les caractères apparaissant dans le texte.
> 
> On a le dictionnaire des nombres d'occurrences suivant :
> $$\{'a':5,'b':2,'c':1,'d':1,'r':2\}$$
> 
> #### Algorithme de prétraitement
> 1. Placer les couples (caractère,fréquence) dans une file de priorité *min* sous la forme d'arbre binaires réduits à une racine.
>    $$\left\{ 'a':\underbrace{ 5 }_{ \frac{5}{11} },'b':\underbrace{ 2 }_{ \frac{2}{11} },'c':\underbrace{ 1 }_{ \frac{1}{11} },'d':\underbrace{ 1 }_{ \frac{1}{11} },'r':\underbrace{ 2 }_{ \frac{2}{11} } \right\}$$
> 2. Tant que la file contient au moins deux éléments :
>    - Extraire les deux éléments de plus petite priorité (plus petite fréquence)
>    - Créer un noeud ayant ces deux éléments comme fils gauche et droit.
>    - Insérer ce noeud dans la file.
> 3. Renvoyer le dernier élément de la file.
> 
> #### Initialement
> ```mermaid
> graph TD;
> id1((a,5/11)); id2((b,2/11)); id3((r,2/11)); id4((c,1/11)); id5((d,1/11))
> ```
> 
> #### 1ere étape
> ```mermaid
> graph TD;
> id1((5/11));
> id2((2/11));
> id3((r,2/11));
> id10((2/11)) --> id11((c,1/11));
> id10 --> id12((d,1/11));
> ```
> Même place car priorité $\frac{2}{11}$ = à celle de *b* et de *r* 
> 
> #### 2e étape
> ```mermaid
> graph TD;
> id7((a,5/11));
> id1((4/11))-->id2((r,2/11));
> id1-->id3((2/11))-->id4((c,1/11));
> id3-->id5((d,1/11));
> id6((b,2/11));
> ```
> 
> #### 3e étape
> ```mermaid
> graph TD;
> id5((a,5/11));
> id7((6/11))-->id1;
> id7-->id6((b,2/11));
> id1((4/11))-->id2((r,2/11));
> id1-->id3((2/11))-->id4((c,1/11));
> id3-->id8((d,1/11));
> ```
> 
> #### 4e étape
> ```mermaid
> graph TD;
> id9((11/11))-->id7;
> id9-->id5((a;5/11));
> id7((6/11))-->id1;
> id7-->id6((b,2/11));
> id1((4/11))-->id2((r,2/11));
> id1-->id3((2/11))-->id4((c,1/11));
> id3-->id8((d,1/11));
> ```
> 
> On obtient un arbre binaire dont les feuilles contienne les caractères présents dans le texte.
> 
> On en tire un codage de chacun d'eux en examinant l'unique chemin de la racine au caractère encodant 0 si on met le fils gauche et 1 pour le fils droit.
> 
>#### Résultat
>
| Caractère | Code |
| --------- | ---- |
| a         | 1    |
| b         | 01   |
| c         | 0010 |
| d         | 0011 |
| r         | 000  |
>
> On obtient des codes d'autant plus courts que le caractère est fréquent et le **codage** obtenu est **préfixe** :
> Cad le code d'un caractère n'est le préfixe d'aucun n'autre code
> 
> Ce qui permet de coder un texte sans utiliser de séparation.
> $\text{abracadabra} \to \underbrace{ 1 }_{ a }\underbrace{ 01 }_{ b }\underbrace{ 000 }_{ r }\underbrace{ 1 }_{ a }\underbrace{ 0010 }_{ c }\underbrace{ 1 }_{ a }\dots$
> On reconstruit le mot en parcourant l'arbre

### C. Inconvénients de Huffman
- On doit parcourir tout le texte avant de commencer à compresser.
  
> [!tip] Remarque
> Si le texte est dans certaine langue, on peut utiliser les fréquences des lettres dans la langue
- L'arbre doit être fourni pour pouvoir décoder
- La compression ne tire pas profit d'éventuelles répétitions de motifs
## 3. Algorithme LZW (Lempel-Ziv-Welch)
### A. Algorithme pour la compression
LZW détermine un codage (*en construisant un dictionnaire*) au fil de la lecture du texte.

- On suppose que l'on dispose initialement d'un dictionnaire, *d*,codant chaque lettre de l'alphabet 
- Tant qu'il reste du texte à coder :
  1. Retirer du texte, *s*, son plus long préfixe, *w*, qui soit déjà dans *d*
  2. Ajouter le code de *w* à la sortie (cad au texte codé en cours d'écriture)
  3. Concaténer *w* au caractère suivant *c*
  4. Affecter à *wc* (concaténation de *w* et *c*) le prochain code non encore utilisé
### B. Algorithme pour la décompression
On dispose initialement du même dictionnaire, *d'* [^5], codant les lettres de l'alphabet(état initial du dico précédent).

Tant qu'il reste du texte, *s'*, à décoder :
1. Retirer de *s'* le premier code
2. Ajouter la séquence décodée, *w'*, à la sortie
3. Concaténer *w'* et le premier caractère, *c*, de la séquence codée par le code suivant
4. Affecter *w'c* au dictionnaire en lui associant le prochain code non utilisé

[^1]: Notation "Python" positions de $i$ inclus à $i+M$ exclu

[^2]: Version Bayer-Moore Hors programme

[^3]: Correspondant au nombre de bits sur lesquels sont codés les entiers manipulés

[^4]: La lettre la plus à droite est multipliée par $B^0$

[^5]: Réciproque du dictionnaire *d* (mot,clé) en (clé,mot)










Si on cherche toutes les positions :
- algo n°1 avec boucle for :






















Meme si le haché est le meme, il faut également vérifier que le motif est identique 



















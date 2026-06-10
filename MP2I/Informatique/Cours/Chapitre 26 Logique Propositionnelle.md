
# I/ Syntaxe des formules propositionnelles


> [!definition] 
> Soit $\mathcal{V}$ un ensemble dénonbrable, dont les éléments sont appelées variables (propositionnelles)
> L'ensemble des formules propositionnelles sur $\mathcal{V}$ est défini inductivement par 
> - $B=\mathcal{V} \cup \{\top,\bot\}$ ($\top$ Top / $\bot$ bottom)
> - Si $\phi$ et $\psi$ sont des formules alors
>   - ($\lnot \phi)$ est une formule (non phi)
>   - ($\phi ∧\psi)$ est une formule (phi et psi)
>   - ($\phi ∨ \psi)$ est une formule (phi ou psi)
>   - ($\phi \to \psi)$ est une formule (phi implique psi)
>   - ($\phi \leftrightarrow \psi)$ est une formule (phi equivalent psi)

>[!example]  Exemple de formule : 
>$(\lnot((\phi ∨ \psi)∧ \phi))$
> On parle de <mark style="background: #ABF7F7A6;">formule stricte</mark> lorsque tous les parenthèsages sont bien présents ; ceci est l'écriture canonique des formules proportionnelles

>[!example] Autre exemples 
>Si $\mathcal{V}= \{v_{1},v_{2},v_{3}\}$ exemple de formules $((\lnot(v_{1} ∧ v_{2}))∨(\lnot v_{3}))$

##### Implémentation possible en OCaml :
```OCaml
Type formule = Variable of int 
	|Top
	|Bottom
	|Non of formule
	|Et of formule*formule
	|Ou of formule*formule
	|Impl of formule*formule
	|Eq of formule*formule
```

Fondamentalement toute formule s'écrit à l'aide des variables (élément de $\mathcal{V}$) de $\top, \bot$ des connecteurs binaires $(∧,∨,\to,\leftrightarrow)$ et du connecteur unaire $\lnot$

##### Représentation sous forme d'arbre : 

Toutes formules propositionnelle peut se représenter par un arbre selon le principe suivant :
- Chaque feuille est étiquetée par un élément de base (variable ou constante $\top$ ou $\bot$)
- Chaque noeud interne est étiqueté par une règle d'inférence (un connecteur logique),

*Ajouter schema :p*


 

## 




























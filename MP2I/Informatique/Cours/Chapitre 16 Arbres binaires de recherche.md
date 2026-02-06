
Les arbres binaires de recherche peuvent permettre d'implémenter les structures de <mark style="background: #FF5582A6;">données</mark> et dictionnaire 

## I \ ABR

<mark style="background: #00688F;"><u>Définition</u></mark> : La structure abstraites d'ensemble permet de stocker des éléments <mark style="background: #FF5582A6;">unique</mark> avec peu d'opération de base :
- Créer des ensemble vide 
- ajouter un élément (distincts de ceux déjà présent)
- supprimer un élément présnet 
- rechercher un élément (tester la présence)

Avec un arbre binaire quelconque, ces opérations sont respectivement, en :
- Création : O(1)
- Supression O(n) car il faut aller voir tous les noeuds

- Ajout :
  - <mark style="background: #BBFABBA6;">Methode 1</mark> :
    - O(1) dans tous les cas si on ajoute comme racine (création d'un nouveau noeud et raccordement)
    - O(h) dans le pire cas si on ajoute à une feuille à un noeud n'ayant qu'un fils.
- <mark style="background: #BBFABBA6;">Méthode 2</mark> : 
  - Si on fait un parcours en largeur jusqu'au 1er noeud  srtictement negatif  de 2 fils : Complexité en O(n)






Les ABR arbres de recherche permettent d'assurer de meilleurs complexité (*cf* : rech. dicho. dans un tableau trié versus recherche sequentielle). 

<mark style="background: #00688F;"><u>Définition</u></mark> : ABR 
	Si E est un ensemble totalement ordonné d'étiquette, on appelle arbre binaire de recherche étiqueté par E un arbre qui est :
		- soit vide 
		- soit de la forme $N(x,g,d)$ avec : 
			1) $g$ et $d$ des ABR 
			2) pour toute étiquette $x_g$ dans $g : x_g<x$
			3) pour toute étiquette $x_d$ dans $d : x_d<x$

$$\begin{align}
E &= \mathbb{N} \ \text{par exemple}\\
&=R\\
&=ensemble\\ 
&=
\end{align}$$

<mark style="background: #00688F;"><u>Propriété (caractéristique)</u></mark> : 
	Un arbre binaire est un ABR 
	<u>ssi</u> la liste de ses étiquettes dans l'ordre infixe est croissante
	
<u>remarque</u> strictement croissante puisque l'on a supposé toute les étiquettes distinctes

>[!summary]+  Démonstration : 
>- <u>sens direct</u> : On va montrer, par induction sur la structure d'ABR que pour tout ABR $a$, la liste de ses étiquettes dans l'ordre issu d'un parcours infixe est croissante --> $\mathscr{P}_a$
>	- si $a$ est vide : (cas de base / initialisation)
>		- une liste est croissante (*cf* il s'agit d'une prpriété qui doit être vraie pour tout couple $(x_i,x_j)$ de la liste : si $i<j$ alors $x_i<x_j$)
>		
>	- si $a=N(x,g,d)$ : Si on suppose que g et d vérifient $\mathscr{P}$
>		- Le parcours infixe de a renvoie la liste $L_g@[x]@L_d$
>		- Par hypothèse d'induction : $L_{g}\nearrow$
>		- Par hypothèse d'induction : $L_{d}\nearrow$
>		- parce que a est un ABR tout élément $x_g$ de $L_g$ est $<x$
>		- parce que a est un ABR tout élément $x_g$ de $L_g$ est $<x$
>		- Donc la liste $L_g@[x]@L_d$ est croissante 


>[!summary]+ Démonstration : 
>- <u>sens indirect</u> : On va montrer, par induction sur la structure d'arbre binaire que si par un arbre binaire $a$, la liste de ses étiquettes dans l'ordre issu d'un parcours infixe est strictement croissante alors a est un ABR --> $\mathscr{P}_a$
>	- si $a$ est vide : (a est un arbre binaire vide)
>		- a est un ABR de par la définition des ABR 
>		
>	- si $a=N(x,g,d)$ : on suppose que $\mathscr{P}$ est vraie pour$g$ et $d$
>		- si la liste des étiquettes issue d'un parcours infixe de $g$ est strictement croissante alors $g$ est un ABR 
>		- et si la liste des étiquettes issue d'un parcours infixes de $d$ est strictement croissante alors $d$ est un ABR 
>		- Considérons un arbre binaire non vides $a=N(x,g,d)$ tel que :
>			- la liste $L$ de ses étiquettes dans un parcours infixe est strictement croissante 
>		- alors (propriété du parcours infixe) $L=L_g@[x]@L_d$
>			1) $L_g$ croissante strictement donc (hypo. d'induction) <mark style="background: #FF5582A6;">$g$ est un ABR</mark>
>			2) $L_d$ croissante strictement donc (hypo. d'induction) <mark style="background: #FF5582A6;">$g$ est un ABR</mark>
>			3) $x>x_g$ pour tout élément de $L_g$
>			4) $x>x_g$ pour tout élément de $L_g$
>- <u>Conclusion</u> : En vertu de 1,2,3 et 4 et de la definition d'ABR, $a$ est un ABR

## II \ Implémentations du type ensemble 

1) <u>Recherche</u> : a est supposé ABR 
   ```Ocaml
   let rec recherche e a = match a with 
	   |Vide -> false
	   |N(x,g,d) -> if x = e then true 
						else if e < x then recherche e g
						else recherche e d 
   ```
- <u>Terminaison</u> : on a pour variant d'appel la taille de l'arbre. 
  Si la recherche se poursuit dans un sous-arbre gauche ou droit qui est de taille strictement plus petite (ne contient pas la racine) donc la fonction termine

- <u>Correction </u> : invariant d'appel : recherche e a renvoie true ssi e est une etiquette d'un noeud de a .
  On procède par induction sur la structure d'arbre binaire 
	-  <u>si a est vide</u> :  vrai recherche e arbre vide renvoie ``false``
				    et e $\notin$ a car a est vide
				    l'équivalence est vraie
	- <u>si a = N(x,g,d)</u> : 
	  si x = e : l'appel renvoie 
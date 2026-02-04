





Champs mutables dans les enregistrements 
- <u>exemple</u> : implémentation de pile mutables
  - <u>Rappel</u> : on a vu une implémentation avec des piles non mutables (pas des listes Ocaml) où la depiler renvoyait le sommet de la pile et la pile modifiée (càd avec le nouveau sommet en tête de liste.)

On doit se donner un nouveau type 
```Ocaml
type 'a maillon = {valeur : 'a ; mutable suivant :'a maillon option}
type 'a pile = {mutable sommet : 'a maillon option}
(*None permettra de représenter une pile vide*)
let est_vide p = (p.sommet = None)
let empile e p =  p.sommet <- Some {valeur = e; suivant = p.sommet}
```

<u>Représntation en machine</u> : 
```Ocaml
let m = {valeur = 2; suivant = Some {valeur = 1 ; suivant = None}}
let p = {sommet =  Some m}
Ajout : 
```










Tableaux à deux dimensions ( ou plus)



3) <u>Copie de tableaux</u> : 
   Pour des tableaux dont les éléments sont de type non mutable on peut faire une copie à l'aide de la fonction Array.copy
   
   Possible donc pour les tableaux d'entiers, ou de flottants etc, mais pas pour les tableaux d'entiers, ou de flottants, etc, mais pour les tableaux 


III \ Bonds 


2) Bonds while 





<u>Complexité</u> : en fonction du nombre de noeuds 
- $C(n_a)= 1 +$ 
  
  On peut montrer, par récurrence forte sur la taille que $C(n)=n$  (En prenant $C(0)=0$)

<u>ou bien</u> : on argumente sur le fait que en chaque noeud on effectue une seule opération élémentaire d'affichage de la valeur.































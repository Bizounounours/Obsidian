
On présente ici les traits impératifs (ou mutables) de OCaml alors que jusque là, on avait utilisé Ocaml comme langage fonctionnel, dans lequel, toutes les variables et valeurs étaient de type non mutable (non modifiable).
<h1> I)<u>Référence </u></h1>
Définition : 
	Une référence en OCaml est l'analogue d'un pointeur ne C, elle correspond à une adresse en mémoire.

Pour chaque type de valeur que l'on connaît, on peut définir des références vers des valeurs de ce type.

````OCaml
#let s  = ref 0;
si int ref = {content = 0}
`````

Pour accéder à la valeur référencée par s :
````OCaml
#!s  (*Analogue de *p en C *)
int = 0
`````

Pour changer la valeur référencée :
````OCaml
#s := 2
-: unit = ()    (* instruction de type unit*)
`````

<b><u>Attention</u></b> : deux opérateurs de comparaisons nouveaux :
	== et != 
	 qui compare les adresses en mémoire (alors que = et <> comparent les valeurs référencées)

````OCaml
#let s = ref 0 and r = ref 0
`````

On aura : 
	s = r        qui vaut true
	s == r     qui vaut false
	(mêmes valeurs référencées mais adresse différentes)

- <u><b>Utilisation de références dans les enregistrements</b></u>
Les types enregistrements rencontré précédemment n'était pas mutables, mais on peut "forcer la mutabilité" en précédent le nom d'un champ du mot clé mutable

<u>exemple</u>: implémentation de pile mutables

Rappel : On a vu une implémentation avec des piles non mutables (par des liste OCaml) où la fonction dépiler renvoyais le sommet de la pile et la pile modifiée (càd avec le nouveau sommet en tête de liste).

On doit se donner un nouveau type.
````OCaml
type 'a maillon = {valeur : 'a; mutable suivant : 'a maillon option}
`````
(sur tout type déjà défini on peut définir un type option associé qui est un type somme de la forme : )
````OCaml
type None | Some of .... [type de base]
`````

````OCaml
type 'a pile = {mutable sommet : 'a maillon option};
		(* Nous permettra de représenter une pile vide *)
let est_vide p = (p.sommet = None);
let empile e p = p.sommet <- Some{valeur = e; suivant = p.sommet}
`````

<u>Représentation en machine</u>:
````OCaml
let m = {valeur = 2; suivant = Some {valeur = 1; suivant =None}}
let p = {sommet = Some m}
`````
<u>Ajout</u>:
````OCaml
p.sommet <- Some{valeur = 3; suivant = some m}
`````

La fonction empile a en sortie le type unit. Elle <u>agit par effet</u> et ne renvoie rien.

````OCaml
let depile p = match p.sommet with
	|None -> failwith "pile vide"
	|Some{valeur; suivant} -> p.sommet <- suivant; valeur
`````
On continuera de s'assurer avant appel à dépiler que la pile n'est pas vide, cependant on garde le motif None dans le filtrage pour qu'il soit jugé exhaustif.

**-> C'est la dernière expression qui donne le type de la séquence**

Il existe aussi deux modules : Queue et Stack qui implémentent, respectivement des files mutables et des piles muables.
A l'aide des fonctions :
	Stack.create()
	Stack.push e p  // empiler     (renvoie  () )
	Stack.pop p      // dépiler      (renvoie l'élément dépilé)

Pour les files, 
	Queue.create
	Queue.add
	Queue.take

<h1> II)<u>Tableau </u></h1>

## 1. <u>Syntaxe et création</u>


````OCaml
let tab = [|1;2;3|]
	(*délimieteurs: [|  |]
	  sépratauers: ;       *)
`````
Pour créer un tableau : 
````OCaml
Array.make taille valeur
(* ou bien *)
Array.init taille fonction

Array.init n f 
	(* créer u  tableau de taille n dont les éléments sont f0,f1,...,f(n-1) *)
`````
## 2.<u>Tableau à deux dimensions (ou plus)</u>

Seront implémentés sans forme de tableau de tableau, par exemple de type int array array


#### ✦<u>Numérotation d'un tableau à une dimension</u> :
		0 à Array.lenght - 1
	avec accès aux éléments par tab.(i) {Pour les tableau de tableau : tab.(i).(j)}
⚠︎ pas de numérotation négative des positions

### ✦les tableaux sont de type mutable : modification :
	tab.(i) <- nouvelle valeur
	
#### ✦<u>Copie de tableau</u> :
Pour des tableau dont les éléments sont de type non mutable on peut faire une copie à l'aide de la fonction ``Array.copy``
Possible donc pour les tableaux d'entiers, ou de flottants, etc, mais pas pour les tableaux de tableaux.

<h1> III)<u>Boucle </u></h1>

## 1.<u>Syntaxe et création</u>


````OCaml
for i = deb to fin do
	/* type unit ! */
done
`````
->deb et fin inclus, incrément de 1 à chaque itération
``downto`` au lieu de ``to`` permet de décrément de 1 à chaque itération

⚠︎ <u>L'indice de boucle est de type int (et non int ref ) et donc non modifiable</u>

<u>Remarque </u>: sa valeur au de la boucle est ``fin``

⚠︎ Il n'existe pas d'instruction ``break`` ou ``continue`` comme en C

``break``: interrompt l'itération en cours et la boucle 
``continue``: interrompt en cours et passe à l'itération suivante

On verra une alternative au ``break`` (et au return dans une boucle) grâce aux "exception" et à leur gestion.

## 2.<u>Boucle While</u>
````OCaml
while e1 do
	/* type unit ! */
done
`````
``e1``: type bool

<u>Exercice</u> : écrire cette boucle avec une boucle while
```OCaml
for i = 0 to n do
	print_int i;
	print_newline();
done
```
``incr`` et ``decr`` permettent d'incrémenter ou  décrémenter de 1 une référence d'entier.

````OCaml
let i = ref 0;
while i <= n do
	print_int !i;
	print_newline();
	incr i;
done
`````

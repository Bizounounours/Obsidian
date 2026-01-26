













































II \ Implémentation

1 ) en Ocaml

```OCaml
Type 'a arbre = Vide|noeud of 'a arbre* arbre

let a = Noeud(0,
	Noeud(1,
		Noeud(2, Vide, Vide),
		Noeud(3,
			Noeud(4, Vide, Vide),
			Vide)
			),
			Noeud(5,
				Noeud(6, Vide, Vide)
				Noeud(7, Vide, Vide)
			)
```

- Fonction hauteur et taille
```OCaml
  let rec taille a = match a with
```
































Taille d'un arbre binaire



proprietenninininznnn





par













i = q = j/2



Avantage de la représentation 
	l'acces a la valeur dans un noeud est en O(1) si on connait son numero

on aura 







































































Une "exeption" est un mécanisme qui cause l'arrêt de l'éxecution d'un programme.

<u>Par exemple</u> :
```Ocaml
let x = 1/0;;
Exeption: Division_by_zero
```

>[!warning] Distinguer exception et erreur de synthaxe
><u>Exception</u> : erreur à l'éxecution
><u>Erreur de synthaxe</u> : erreur a la compilation

## I) Définir et lever une exception 

Les exceptions ont un type propre `exn` et on peut en créer avec la synthaxe 

```Ocaml
(*définition de nouvelles exception / A,B,C, D constructeurs*)
exception A
exception B
exception C of int 
exception D of string 
etc...
```

Une fois un type d'exception définie, on peut déclencher avec le mot-clé `raise` 
```Ocaml
# raise (D, "toto")
(*causera l'arret avec l'affichage*)
Exception : D toto
```

<u>cf</u> : `failwith "liste vide"` qui correspond à `raise(Failure "liste vide")`

## II) Rattraper une exception : 

Le rattrapage d'une exception permet d'éxecuter un code alternatif si l'exception est levée 
Le mécanisme de rattrapage fonctionnne comme le filtrage : lorsqu'une exception advient on pourra dresser une liste des causes (exeptions prédéfinies) possibles et adapter la réponse à l'xception observée 

>[!warning] Cependant le filtrage n'a pas besoin d'être exhaustif 

#### <u>synthaxe du rattrapage</u> : 

```Ocaml
try e with 
  |m1 -> e1
  |m2 -> e2 
```

`e` est une exception si `e` déclenche une exception correspondant au motif `m1` 
on remplacera `e` (en echec) par l'expression `e1`

<u>Exemple</u> : 
```Ocaml
let safe_dir x y = 
	try x/y with
		|Division_by_zero -> 0 (*on renvoie 0 si x/y n'est pas possible*)
```

## III) Sortie prématurée d'une boucle 

<u>Exemple</u> : 
```Ocaml
let contient_zero t = 
	let n = Array.lenght in
	try 
		for i=0 to n-1 do 
			if t.(i) = 0 then raise Exit; 
		done;
		false
	with
		Exit -> true 
```
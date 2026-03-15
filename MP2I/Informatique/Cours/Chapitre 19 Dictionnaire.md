
## I)


Une association est un lieu entre une clé et une valeur



interface pour la structure de









## II) Réalisation avec un ABR : (structure de donné concrète)

On  stockera dans les noeuds la clé et la valeur associé mais les comparaisons ne se ferait que sur la valeur des clés

```Ocaml {pre}
(*Exmple*)
type noeud= V | N of int(*clé*)*string(*valeur*)
```

- <u>Cas particulier</u> : lorsque les clé sont des entiers positifs.
  on pourrait représenter le dictionnaire à l'aide d'un tableau 

Si on connait la valeur maximale possible pour les clés alors, la création du dictionnaire (via celle du tableau) se ferait en temps linéaire ($O(taille\ max)$) et les opérations se feraient en temps constant 

Il faudrait convenir que si une clé n'existe pas, on lui associe dans le tableau une valeur non ambigue, différentes des valeurs autorisées ou alors définir un second tableau dans lequel on indique par un booléen, par exemple que la clé existe ou non.

<u>Exemple</u> : dictionnaire associant aux codes ASCII les lettres de l'alphabet latin, la lettre (caractère) correspondant de : 
- $65$ à $65+25-1$ : A ; B ; ..... ; Z
- $95$ à $122$ : a ; ..... ; z

<u>sous forme d'un tableau</u> : on aurait par principe la valeur maximale des entiers 127 








- supression d'une clé i (et par suite des valeurs associé)


inconvénient :
1) les clés doivent etre entieres
2) Complexité spatiale potentiellement 





une table


on s'efforcera d'avoir $\frac{\alpha}{N}$ proche de $1$ quel que soient $n$ et $N$ et donc










cad un agrégat









































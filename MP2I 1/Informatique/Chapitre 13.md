
<mark style="background: #ABF7F7A6;">I \ Tests fonctionnels (tests en boîte noire)</mark>

Boite Noire: 
- on ne s'interesse qu'aux résultats d'execution 
- on examine pas le code

On vérifie que le programme produit la sortie attendu sur divers entrées à l'aide de *assert* ( fonction en C et instruction en OCaml )

1 . <mark style="background: #D2B3FFA6;">Choix des entrées</mark> :

- <mark style="background: #FFF3A3A6;">Test exhaustifs</mark> : on teste toutes les entrées possibles 
  **RQ**: c'est généralement impossible en raison d'un trop grand nombre d'entrées à tester

- <mark style="background: #FFF3A3A6;">Tests aléatoire </mark> : on teste certaines entrées possible en en choisissant au hasard ( loi uniforme )

- partitionnement du domaine d'entrées :
  On peut proposer un partitionnement :
  - qui distingue des entrées de façon à créer des problèmes potentiels
    **Par exemple**: entiers positifs, négatifs ou nul
    **Ou encore**: listes d'entiers tous positif || listes d'entiers tous négatifs || listes d'entier qui ne sont pas tous de meme signe
    - ex : recherche du max : /!\ ne pas initialiser le max à 0

2 . Détermination de la sortie correcte :

Trois façon de faire :
- 1 ) Générer un jeux de tests à la main 
- 2 ) calculer la sortie avec un autre algoritme que l'on sait correct
- 3 ) ne pas calculer la sortie mais vérifier que l'algorithme à tester renvoie une sortie qui convient 
Exemple : la recherche du PGCD par l'algo d'Euclide 
1) a = 3x5x5x7
   b = 5x7x11
   PGCD(a,b)= 5x7 
   assert 































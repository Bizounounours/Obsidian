
> [!abstract] Sommaire
> 1. Dictionnaires & Hachage (Ch. 19)
> 2. Complexité Avancée & Analyse Amortie (Ch. 20)
> 3. Système & Entrées-Sorties (Ch. 21)
> 4. Récursivité & Induction (Ch. 22)
> 5. Stratégies Algorithmiques (Ch. 23)
> 6. Bases de Données & SQL (Ch. 24)

---

## I. Dictionnaires et Tables de Hachage (Ch. 19)

### 1. Concepts Fondamentaux
- **Dictionnaire** : Structure stockant des couples `(clé, valeur)`. Clés uniques.
- **Table de hachage** : Utilise une fonction $h$ pour transformer une clé en un indice de tableau $i \in [|0, N-1|]$.
- **Collision** : $h(k_1) = h(k_2)$.
    - **Chaînage** : Tableau de listes. Complexité moyenne $O(1+\alpha)$ avec $\alpha = n/N$ (facteur de charge).
    - **Adressage ouvert** : On cherche une case vide selon une séquence $h(k)+i \pmod N$. 

### 2. Syntaxe OCaml (`Hashtbl`)
```ocaml
let t = Hashtbl.create 16 in (* 16 = capacité initiale *)
Hashtbl.add t "Pomme" 2;    (* Ajout *)
let v = Hashtbl.find t "Pomme" in (* Recherche, lève Not_found si absent *)
let opt = Hashtbl.find_opt t "Poire" in (* Renvoie None ou Some v *)
Hashtbl.remove t "Pomme";   (* Suppression *)
if Hashtbl.mem t "Banane" then ... (* Test d'existence *)
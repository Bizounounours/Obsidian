# 💻 ARCHIVE INTÉGRALE : INFORMATIQUE (MP2I)

> [!abstract] Sommaire
> 1. Dictionnaires & Hachage (Ch. 19)
> 2. Complexité Avancée & Analyse Amortie (Ch. 20)
> 3. Système & Entrées-Sorties (Ch. 21)
> 4. Récursivité & Induction (Ch. 22)
> 5. Stratégies Algorithmiques (Ch. 23)
> 6. Bases de Données & SQL (Ch. 24)

---

## I. Dictionnaires et Tables de Hachage (Ch. 19)

> [!rappel] Interface de Dictionnaire
> Un dictionnaire (ou tableau associatif) permet de manipuler un ensemble d'associations **Clé (unique) $\to$ Valeur**.
> - **Opérations** : Insertion, recherche, suppression, modification.
> - **Contraintes** : Clés de même type, valeurs de même type.

### 1. Table de Hachage
Principe : Transformer une clé en indice dans un tableau de taille $N$ via une fonction de hachage $h(k)$.
- **Collisions** : Quand $h(k_1) = h(k_2)$.
    - **Chaînage** : Chaque case contient une liste. Complexité moyenne en $O(1 + \alpha)$ avec $\alpha = n/N$.
    - **Adressage ouvert** : Recherche d'une case vide dans le tableau.
        - *Sondage linéaire* : On teste les cases suivantes une par une.
        - *Double hachage* : On utilise une seconde fonction pour définir le pas de saut.

### 2. Syntaxe OCaml (`Hashtbl`)
```ocaml
let t = Hashtbl.create 16 in
Hashtbl.add t "cle" 42;
match Hashtbl.find_opt t "cle" with
| Some v -> print_int v
| None   -> print_string "Absent";
Hashtbl.remove t "cle"
```

---

## II. Complexité Avancée (Ch. 20)

### 1. Complexité en moyenne ($C_m$)
- **Définition** : Moyenne des temps d'exécution pondérée par la probabilité de chaque instance.
- **Formule** : $C_m(n) = \sum_{e \in E_n} P(e) \cdot c(e)$.
- **Exemple** : Recherche séquentielle dans un tableau de booléens. Si la probabilité d'avoir `true` est $P = 1/2$, la complexité moyenne est $O(1)$.

### 2. Analyse Amortie (Méthode du Potentiel)
On définit une fonction de potentiel $\Phi(D) \geq 0$ qui évalue "l'énergie" stockée.
- **Coût amorti** : $c'_i = c_i + \Phi(D_i) - \Phi(D_{i-1})$.
- **Propriété** : Le coût total réel est majoré par le coût total amorti si $\Phi(D_n) \geq \Phi(D_0)$.

> [!rappel] File à deux piles ($in$ et $out$)
> En posant $\Phi = 2|in|$, on montre que l'ajout et le retrait sont en **$O(1)$ amorti**. Le coût potentiellement élevé du transfert des éléments (quand $out$ est vide) est compensé par le potentiel accumulé lors des insertions.

---

## III. Système et Entrées / Sorties (Ch. 21)

### 1. Inodes et Fichiers
- **Inode** : Identifiant unique. Contient les **métadonnées** (droits, taille, adresses physiques) mais **pas le nom**.
- **Répertoire** : Fichier associant des noms à des inodes via des couples `(nom, inode)`.
- **Lien physique** (`ln`) : Création d'un nouveau nom pointant vers le même inode.

### 2. Programmation C (Fichiers)
```c
FILE *f = fopen("data.txt", "r"); // "r": read, "w": write (écrase), "a": append
if (f == NULL) { perror("Erreur"); exit(1); } // Test obligatoire

int val;
while (fscanf(f, "%d", &val) == 1) { // Renvoie le nb d'items lus
    printf("Valeur : %d\n", val);
}
fclose(f); // Libère la ressource et vide les tampons
```

---

## IV. Récursivité et Induction (Ch. 22)

### 1. Ensembles Inductifs
Définis par une **Base** (cas triviaux) et des **Règles d'inférence** (hérédité).
- *Exemple (Parenthésage)* : $\epsilon \in \mathcal{P}$ ; si $u \in \mathcal{P}$ alors $(u) \in \mathcal{P}$ ; si $u,v \in \mathcal{P}$ alors $uv \in \mathcal{P}$.

### 2. Preuves
- **Terminaison** : Trouver un **variant** (entier strictement positif et strictement décroissant à chaque appel).
- **Correction** : Par **induction structurelle** (analogue à la récurrence classique).

---

## V. Stratégies Algorithmiques (Ch. 23)

### 1. Backtracking (Retour sur trace)
Construction d'une solution de proche en proche avec abandon des branches qui mènent à une impasse (**élagage**).
- *Exemple* : Problème des N-Reines ou résolution de Sudoku.

### 2. Programmation Dynamique
Optimisation pour les sous-problèmes qui se chevauchent.
- **Top-Down (Mémoïzation)** : Récursion + stockage (dictionnaire/tableau).
- **Bottom-Up (Tabulation)** : Remplissage d'un tableau des petits cas vers le haut.

```c
// Fibonacci Tabulation (O(n) temps, O(1) espace)
int fibo(int n) {
    if (n <= 1) return n;
    int a = 0, b = 1, res;
    for (int i = 2; i <= n; i++) {
        res = a + b;
        a = b; b = res;
    }
    return res;
}
```

---

## VI. Bases de Données et SQL (Ch. 24)

### 1. Modèle Relationnel
- **Table** : Ensemble d'enregistrements (nuplets).
- **Clé primaire** : Identifiant unique de la ligne.
- **Clé étrangère** : Référence à une clé primaire d'une autre table (jointure).

### 2. Requêtes SQL
```sql
SELECT continent, COUNT(*) as nb, AVG(pib)
FROM pays
WHERE population > 1000000        -- Filtre avant regroupement
GROUP BY continent                -- Regroupe
HAVING AVG(pib) > 5000            -- Filtre après calcul d'agrégat
ORDER BY nb DESC
LIMIT 10;
```

---

# 💡 Points de Vigilance
- **Hachage** : Complexité $O(1)$ en moyenne, mais $O(n)$ si la fonction est mauvaise (pire cas).
- **C** : Ne jamais oublier `fclose(f)` pour libérer la mémoire et le descripteur.
- **SQL** : `WHERE` filtre les lignes, `HAVING` filtre les groupes.

#Informatique  #Fiches 
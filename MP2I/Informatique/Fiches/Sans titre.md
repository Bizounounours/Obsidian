# 💻 FICHE DE RÉVISION : SEMAINE DU 25/05 (MP2I)

> [!abstract] Sommaire
> 1. Algorithmique du texte (Ch. 25)
> 2. Bases de données & SQL (Ch. 24)
> 3. Stratégies algorithmiques (Ch. 23)
> 4. Pratique Machine & Tris (Annexes)

---

## I. Algorithmique du Texte (Ch. 25)

### 1. Recherche de motif
* **Recherche Naïve** : On teste chaque position possible du texte une par une. Complexité pire cas : $O(n \times m)$.
* **Boyer-Moore-Horspol (BMH)** : Utilise une **table de décalage** basée sur le dernier caractère du motif aligné. Si la comparaison échoue, on décale selon une valeur pré-calculée plutôt que d'avancer d'une seule case.

```c
// Pré-traitement BMH : calcul des décalages
void calculer_decalages(char *motif, int m, int d[256]) {
    for (int i = 0; i < 256; i++) d[i] = m;
    for (int i = 0; i < m - 1; i++) d[(unsigned char)motif[i]] = m - 1 - i;
}
```

### 2. Compression
* **Huffman** : Construction d'un arbre binaire basé sur la fréquence des caractères (algorithme glouton). Les caractères fréquents ont un code court.
* **LZW (Lempel-Ziv-Welch)** : Compression par dictionnaire. On construit le dictionnaire de motifs dynamiquement pendant la lecture du texte.



---

## II. Bases de Données (Ch. 24)

### 1. Modélisation
* **Modèle Entité-Association (E-A)** : Représentation graphique des entités et de leurs liens.
* **Modèle Relationnel** :
    * **Clé primaire** : Identifiant unique d'un enregistrement.
    * **Clé étrangère** : Attribut pointant vers la clé primaire d'une autre table.
* **Passage E-A $\to$ Relationnel** : Traduction des associations en relations ou en clés étrangères selon les cardinalités ($1\text{--}*$ ou $1\text{--}1$).

### 2. SQL Avancé (Norme SQL99)
* **Jointures** :
    * `JOIN ... ON` : Jointure interne (garde uniquement les correspondances).
    * `LEFT JOIN ... ON` : Jointure externe (
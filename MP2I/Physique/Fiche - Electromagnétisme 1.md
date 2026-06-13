

> [!formule] Constantes Fondamentales
> - Vitesse de la lumière : $c = 3,00 \times 10^8 \text{ m.s}^{-1}$
> - Permittivité du vide : $\epsilon_0 \approx 8,85 \times 10^{-12} \text{ F.m}^{-1}$
> - Perméabilité du vide : $\mu_0 \approx 1,26 \times 10^{-6} \text{ H.m}^{-1}$
> - Relation fondamentale : $c^2 \mu_0 \epsilon_0 = 1$

---

## I. Le Champ Magnétique $\vec{B}$

### 1. Définition et Force de Lorentz
Le champ magnétique décrit les interactions entre charges en mouvement.

> [!formule] Force de Lorentz magnétique
> Une charge $q$ au point $M$ avec une vitesse $\vec{v}$ dans un champ $\vec{B}(M,t)$ subit :
> $$\vec{F}_m = q \vec{v} \wedge \vec{B}(M,t)$$

> [!rappel] Propriétés du produit vectoriel
> - $\vec{A} \wedge \vec{B} = - \vec{B} \wedge \vec{A}$ (Anticommutativité)
> - $\vec{A} \wedge \vec{A} = \vec{0}$
> - Le vecteur résultat est orthogonal aux deux vecteurs.
> - Norme : $|Vect{A} \wedge Vec{B}| = AB \sin(	\eta)$.

### 2. Sources et Cartes de Champ
- **Sources** : Mouvement de charges (courants macroscopiques ou microscopiques).
- **Superposition** : Les champs magnétiques s'ajoutent vectoriellement : $\vec{B}_{tot} = \sum \vec{B}_i$.
- **Lignes de champ** : Courbes tangentes à $\vec{B}$ en tout point, elles sont toujours **fermées**.
- **Aimant droit** : À l'extérieur, $\vec{B}$ sort par le pôle Nord et entre par le pôle Sud.

### 3. Champs usuels créés par des courants

> [!formule] Spire circulaire (sur l'axe Oz)
> Pour une spire de rayon $R$ parcourue par un courant $i$ :
> $$\vec{B}(z) = \frac{\mu_0 i R^2}{2(R^2 + z^2)^{3/2}} \vec{u}_z$$
> Au centre ($z=0$) : $B(0) = \frac{\mu_0 i}{2R}$.

> [!formule] Solénoïde (Bobine longue $L \gg R$)
> À l'intérieur du solénoïde, le champ est considéré comme uniforme :
> $$\vec{B}_{int} = \mu_0 n i \vec{u}_z \quad (n = N/L)$$

> [!formule] Bobines de Helmholtz
> Deux bobines identiques de rayon $R$ séparées d'une distance $R$ :
> $$\vec{B} \approx \frac{\mu_0 N i}{R} \left(\frac{4}{5}\right)^{3/2} \vec{u}_z$$

---

## II. Moment Magnétique $\vec{m}$

> [!formule] Moment magnétique d'une spire
> $$\vec{m} = i S \vec{n} = i \vec{S}$$
> - $i$ : intensité du courant (A).
> - $S$ : surface de la spire ($m^2$).
> - $\vec{n}$ : vecteur unitaire normal (règle de la main droite).

> [!example] Moment magnétique de l'électron
> Le magnéton de Bohr $\mu_B$ est le moment magnétique associé à l'électron : $\mu_B = \frac{e \hbar}{2 m_e}$.

---

## III. Actions d'un Champ Magnétique

### 1. Force de Laplace
S'exerce sur un conducteur parcouru par un courant $I$ dans un champ extérieur $\vec{B}$.

> [!formule] Loi de Laplace
> Un élément de courant $I d\vec{\ell}$ subit :
> $$d\vec{F}_L = I d\vec{\ell} \wedge \vec{B}$$

### 2. Couple et Énergie
Un dipôle magnétique placé dans un champ $\vec{B}$ uniforme subit des actions mécaniques qui tendent à l'orienter.

> [!formule] Moment du couple (Torque)
> $$\vec{\Gamma}_L = \vec{m} \wedge \vec{B}$$

> [!formule] Puissance de l'action de Laplace
> $$\mathcal{P}_L = \vec{\Omega} \cdot \vec{\Gamma}_L$$

> [!remarque] Équilibre
> - **Stable** : $\vec{m}$ est aligné avec $\vec{B}$ (même sens).
> - **Instable** : $\vec{m}$ et $\vec{B}$ sont de sens opposés.

---

## IV. Rappels Transverses

### 1. Mécanique
> [!rappel] Dynamique et Travail
> - **PFD** : $\sum \vec{F} = m \vec{a}$.
> - **Moment Cinétique** : $\frac{d\vec{L}_O}{dt} = \sum \vec{\Gamma}_O$.
> - **Puissance d'une force** : $\mathcal{P} = \vec{F} \cdot \vec{v}$.
> - **Théorème de l'Énergie Cinétique** : $\Delta E_c = W_{tot}$.

### 2. Électrocinétique
> [!rappel] Loi d'Ohm et Courant
> - **Loi d'Ohm** : $U = RI$.
> - **Puissance Joule** : $P_J = RI^2$.
> - **Vitesse de dérive** : $I = n q v S$.

> [!remarque] Unité de champ
> $1 \text{ Tesla (T)} = 10^{4} \text{ Gauss (G)}$.

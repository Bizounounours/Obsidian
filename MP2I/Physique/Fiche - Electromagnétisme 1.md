

> [!formule] Constantes Fondamentales
> - Vitesse de la lumière : $c = 3,00 \times 10^8 \text{ m.s}^{-1}$ [cite: 558]
> - Permittivité du vide : $\epsilon_0 \approx 8,85 \times 10^{-12} \text{ F.m}^{-1}$ [cite: 559]
> - Perméabilité du vide : $\mu_0 \approx 1,26 \times 10^{-6} \text{ H.m}^{-1}$ [cite: 560]
> - Relation fondamentale : $c^2 \mu_0 \epsilon_0 = 1$ [cite: 558]

---

## I. Le Champ Magnétique $\vec{B}$

### 1. Définition et Force de Lorentz
Le champ magnétique décrit les interactions entre charges en mouvement [cite: 552].

> [!formule] Force de Lorentz magnétique
> Une charge $q$ au point $M$ avec une vitesse $\vec{v}$ dans un champ $\vec{B}(M,t)$ subit :
> $$\vec{F}_m = q \vec{v} \wedge \vec{B}(M,t)$$ [cite: 553]

> [!rappel] Propriétés du produit vectoriel
> - $\vec{A} \wedge \vec{B} = - \vec{B} \wedge \vec{A}$ (Anticommutativité)
> - $\vec{A} \wedge \vec{A} = \vec{0}$
> - Le vecteur résultat est orthogonal aux deux vecteurs.
> - Norme : $\|ec{A} \wedge ec{B}\| = AB \sin(	heta)$.

### 2. Sources et Cartes de Champ
- **Sources** : Mouvement de charges (courants macroscopiques ou microscopiques dans les aimants) [cite: 564, 567].
- **Superposition** : Les champs magnétiques s'ajoutent vectoriellement [cite: 571].
- **Lignes de champ** : Courbes tangentes à $\vec{B}$, toujours **fermées** [cite: 575, 579].
- **Aimant droit** : À l'extérieur, $\vec{B}$ sort par le pôle Nord et entre par le pôle Sud [cite: 583, 593].

### 3. Champs usuels créés par des courants

> [!formule] Spire circulaire (sur l'axe Oz)
> Pour une spire de rayon $R$ parcourue par un courant $i$ :
> $$\vec{B}(z) = \frac{\mu_0 i R^2}{2(R^2 + z^2)^{3/2}} \vec{u}_z$$ [cite: 364]
> Au centre ($z=0$) : $B(0) = \frac{\mu_0 i}{2R}$.

> [!formule] Solénoïde (Bobine longue $L \gg R$)
> À l'intérieur d'un solénoïde comportant $n = N/L$ spires par unité de longueur :
> $$\vec{B}_{int} = \mu_0 n i \vec{u}_z$$ [cite: 368, 380]
> Le champ à l'extérieur est nul [cite: 368, 380].

> [!formule] Bobines de Helmholtz
> Deux bobines de rayon $R$ séparées d'une distance $R$ créent un champ quasi-uniforme au centre :
> $$\vec{B} = \frac{\mu_0 N i}{R} \left(\frac{4}{5}\right)^{3/2} \vec{u}_z$$ [cite: 383, 384]

---

## II. Moment Magnétique $\vec{m}$

Toute source magnétique se comporte comme un dipôle magnétique [cite: 389]. Il n'existe pas de monopôle magnétique [cite: 390].

> [!formule] Moment magnétique d'une spire
> $$\vec{m} = i S \vec{n} = i \vec{S}$$ [cite: 406, 407]
> - $i$ : intensité du courant (A).
> - $S$ : surface de la spire ($m^2$).
> - $\vec{n}$ : vecteur unitaire normal orienté par la main droite [cite: 406].

> [!example] Magnéton de Bohr
> Moment magnétique de l'électron dans son état fondamental : $\mu_B = \frac{e \hbar}{2 m_e}$ [cite: 413].

---

## III. Actions d'un Champ Magnétique

### 1. Force de Laplace
S'exerce sur un circuit filiforme parcouru par un courant $I$ placé dans un champ extérieur $\vec{B}$ [cite: 464].

> [!formule] Loi de Laplace
> Un élément infinitésimal $d\vec{\ell}$ subit :
> $$d\vec{F}_L = I d\vec{\ell} \wedge \vec{B}$$ [cite: 465]
> Force totale sur un fil MN : $\vec{F}_L = \int_M^N I d\vec{\ell} \wedge \vec{B}$ [cite: 466].

### 2. Couple et Énergie
Un dipôle magnétique dans un champ $\vec{B}$ extérieur uniforme subit un couple d'actions mécaniques [cite: 494].

> [!formule] Moment du couple (Torque)
> $$\vec{\Gamma}_L = \vec{m} \wedge \vec{B}$$ [cite: 494]

> [!formule] Puissance de l'action de Laplace
> $$\mathcal{P}_L = \vec{\Omega} \cdot \vec{\Gamma}_L$$ [cite: 495]
> Où $\vec{\Omega}$ est le vecteur rotation [cite: 494].

> [!remarque] Stabilité de l'équilibre
> - **Stable** : $\vec{m}$ et $\vec{B}$ sont de **même sens** [cite: 509].
> - **Instable** : $\vec{m}$ et $\vec{B}$ sont de sens opposés [cite: 509].
> Le moment magnétique a tendance à s'aligner sur le champ extérieur [cite: 510].

---

## IV. Rappels Transverses

### 1. Mécanique
> [!rappel] Dynamique et Énergie
> - **PFD (2ème loi de Newton)** : $\sum \vec{F} = m \vec{a}$.
> - **Théorème du Moment Cinétique** : $\frac{d\vec{L}_O}{dt} = \sum \vec{\Gamma}_O(\vec{F})$.
> - **Travail d'une force** : $W = \int \vec{F} \cdot d\vec{r}$.
> - **Puissance** : $\mathcal{P} = \vec{F} \cdot \vec{v}$ (translation) ou $\mathcal{P} = \vec{\Gamma} \cdot \vec{\Omega}$ (rotation).

### 2. Électrocinétique
> [!rappel] Courant et Loi d'Ohm
> - **Loi d'Ohm** : $U = RI$.
> - **Puissance dissipée (Effet Joule)** : $P_J = RI^2$.
> - **Lien courant - vitesse microscopique** : $I = n q v S$ (où $n$ est la densité de porteurs, $q$ leur charge, $v$ la vitesse moyenne et $S$ la section) [cite: 434, 437].

> [!remarque] Unité Gauss
> $1 \text{ Gauss (G)} = 10^{-4} \text{ Tesla (T)}$ [cite: 384].

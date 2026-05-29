
> [!abstract] Sommaire
> 1. [[#I. Rappels Mathématiques & Cinématiques|Outils Mathématiques (Produit vectoriel & Polaires)]]
> 2. [[#II. Moment Cinétique et Moments de Force|Moment Cinétique du Point Matériel]]
> 3. [[#III. Théorème du Moment Cinétique (TMC)]]
> 4. [[#IV. Gravitation et Lois de Kepler]]
> 5. [[#V. Dynamique du Solide (Axe fixe $ Delta$)|Dynamique du Solide (Axe fixe)]]
> 6. [[#VI. Énergies du Solide|Bilans Énergétiques du Solide]]

---

## I. Rappels Mathématiques & Cinématiques

> [!rappel] Le Produit Vectoriel ($\wedge$)
> Indispensable pour calculer les moments.
> - **Définition** : $\vec{C} = \vec{A} \wedge \vec{B}$ est un vecteur orthogonal au plan $(\vec{A}, \vec{B})$.
> - **Norme** : $||\vec{C}|| = ||\vec{A}|| \cdot ||\vec{B}|| \cdot |\sin(\theta)|$
> - **Propriété** : $\vec{A} \wedge \vec{B} = \vec{0}$ si les vecteurs sont colinéaires.
> - **Calcul du bras de levier** : $\|\vec{AM} \wedge \vec{F}\| = d \cdot F$ où $d$ est la distance projetée.

> [!rappel] Coordonnées Polaires $(r, \theta)$
> Utilisé pour les mouvements centraux (Kepler) :
> - **Vitesse** : $\vec{v} = \dot{r}\vec{u_r} + r\dot{\theta}\vec{u_\theta}$
> - **Accélération** : $\vec{a} = (\ddot{r} - r\dot{\theta}^2)\vec{u_r} + (r\ddot{\theta} + 2\dot{r}\dot{\theta})\vec{u_\theta}$

---

## II. Moment Cinétique et Moments de Force

> [!definition] Moment Cinétique d'un point $M$ / $A$
> $$\vec{L_A}(M) = \vec{AM} \wedge m\vec{v}$$
> - **Relation de transport (BABAR)** : $\vec{L_B} = \vec{L_A} + \vec{BA} \wedge m\vec{v}$ (avec $\vec{p} = m\vec{v}$)

> [!definition] Moment d'une force $\vec{F}$ / $A$
> $$\vec{\mathcal{M}_A}(\vec{F}) = \vec{AM} \wedge \vec{F}$$
> - Si $\vec{F}$ est colinéaire à $\vec{AM}$, le moment est nul (cas des forces centrales).

---

## III. Théorème du Moment Cinétique (TMC)

> [!formule] TMC (Référentiel Galiléen)
> Pour un point $A$ fixe dans le référentiel :
> $$\frac{d\vec{L_A}(M)}{dt} = \sum \vec{\mathcal{M}_A}(\vec{F}_{ext})$$

---

## IV. Gravitation et Lois de Kepler

> [!rappel] Conservation du moment cinétique
> Pour une **force centrale** (direction vers $O$) :
> $\vec{\mathcal{M}_O}(\vec{F}) = \vec{0} \implies \vec{L_O} = \text{cste}$.
> Le mouvement est donc **plan** et la **Loi des Aires** s'applique.

> [!formule] Constante des Aires ($C$)
> $$C = r^2\dot{\theta} = \frac{L_O}{m} = \text{constante}$$
> - La vitesse aréolaire est $\frac{dS}{dt} = \frac{1}{2}C$.

> [!formule] Lois de Kepler
> 1. **Loi des orbites** : Les trajectoires sont des coniques (ellipses pour les planètes) dont l'astre attracteur est un foyer.
> 2. **Loi des aires** : $\vec{L_O} = \text{cste} \implies$ des aires égales sont balayées en des temps égaux.
> 3. **Loi des périodes** : $\frac{T^2}{a^3} = \frac{4\pi^2}{\mathcal{G}M_{astre}}$

---

## V. Dynamique du Solide (Axe fixe $\Delta$)

> [!definition] Moment d'Inertie $J_\Delta$
> Résistance du solide à la mise en rotation (analogue de la masse).
> - **Point matériel à distance $R$** : $J_\Delta = mR^2$
> - **Cylindre plein / Disque** : $J_\Delta = \frac{1}{2}mR^2$
> - **Cylindre creux / Anneau** : $J_\Delta = mR^2$

> [!formule] TMC Scalaire (Rotation)
> $$J_\Delta \frac{d\omega}{dt} = \sum \mathcal{M}_\Delta(\vec{F}_{ext})$$
> Avec le moment cinétique scalaire $L_\Delta = J_\Delta \omega$ et $\omega = \dot{\theta}$.

---

## VI. Énergies du Solide

> [!formule] Énergie Cinétique de Rotation
> $$E_c = \frac{1}{2} J_\Delta \omega^2$$

> [!rappel] Puissance en Rotation
> - **Force** : $\mathcal{P} = \mathcal{M}_\Delta(\vec{F}) \cdot \omega$
> - **Couple** : $\mathcal{P} = \Gamma \cdot \omega$

> [!formule] Théorème de l'Énergie Cinétique (TEC)
> Pour un solide indéformable en rotation :
> $$\Delta E_c = W_{ext}$$
> *(Les forces intérieures ne travaillent pas : $W_{int} = 0$)*

---

## 💡 Tableau des Analogies

| Translation (Point) | Rotation (Axe $\Delta$) |
| :--- | :--- |
| Masse $m$ | Moment d'inertie $J_\Delta$ |
| Vitesse $v$ | Vitesse angulaire $\omega$ |
| Force $F$ | Moment de force $\mathcal{M}_\Delta$ |
| PFD : $ma = F$ | TMC : $J_\Delta \dot{\omega} = \mathcal{M}_\Delta$ |
| $E_c = \frac{1}{2}mv^2$ | $E_c = \frac{1}{2}J_\Delta \omega^2$ |

---
#Mécanique #Physique #Fiches 
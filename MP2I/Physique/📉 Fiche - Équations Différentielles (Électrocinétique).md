
> [!abstract] Sommaire
> Cette fiche regroupe les formes temporelles des équations du 2nd ordre issues des chapitres RSF et Filtrage.

---

## I. Le Circuit RLC Série (Référence)

L'équation différentielle fondamentale est obtenue par la loi des mailles appliquée au circuit RLC série.

> [!formule] Équation Différentielle Canonique (Ordre 2)
> Toute grandeur $s(t)$ d'un circuit du second ordre suit une équation de la forme :
> $$\frac{d^2s(t)}{dt^2} + \frac{\omega_0}{Q}\frac{ds(t)}{dt} + \omega_0^2 s(t) = \text{Excitation}(t)$$
> 
> Avec les paramètres caractéristiques :
> - **Pulsation propre** : $\omega_0 = \frac{1}{\sqrt{LC}}$
> - **Facteur de qualité** : $Q = \frac{L\omega_0}{R} = \frac{1}{R}\sqrt{\frac{L}{C}}$
> - **Amortissement** : $\sigma = \frac{1}{2Q}$

---

## II. Formes selon la Nature du Filtre

Le second membre (l'excitation) de l'équation différentielle définit la nature du filtrage effectué par le circuit :

> [!formule] Passe-bas (Sortie aux bornes de C)
> Si $s(t) = u_C(t)$ :
> $$\frac{d^2u_C(t)}{dt^2} + \frac{\omega_0}{Q}\frac{du_C(t)}{dt} + \omega_0^2 u_C(t) = \omega_0^2 e(t)$$

> [!formule] Passe-bande (Sortie aux bornes de R)
> Si $s(t) = u_R(t)$ :
> $$\frac{d^2u_R(t)}{dt^2} + \frac{\omega_0}{Q}\frac{du_R(t)}{dt} + \omega_0^2 u_R(t) = \frac{\omega_0}{Q}\frac{de(t)}{dt}$$

> [!formule] Passe-haut (Sortie aux bornes de L)
> Si $s(t) = u_L(t)$ :
> $$\frac{d^2u_L(t)}{dt^2} + \frac{\omega_0}{Q}\frac{du_L(t)}{dt} + \omega_0^2 u_L(t) = \frac{d^2e(t)}{dt^2}$$

---

## III. Passage au Régime Sinusoïdal Forcé (RSF)

Pour résoudre ces équations en RSF, on remplace les opérateurs de dérivation par leurs équivalents complexes.

> [!definition] Correspondance Temporel ↔ Complexe
> - $s(t) \longrightarrow \underline{s}$
> - $\frac{ds(t)}{dt} \longrightarrow j\omega \underline{s}$
> - $\frac{d^2s(t)}{dt^2} \longrightarrow (j\omega)^2 \underline{s} = -\omega^2 \underline{s}$

---

#Physique #Electrocinétique #Fiches 
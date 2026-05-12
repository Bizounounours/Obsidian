

> [!abstract] Informations Générales
> **Source :** Cours de V. Canel (Lycée Claude Bernard)
> **Sujet :** Premier & Second Principes, Corps Pur, Machines Thermiques.

## 1. Description de la Matière
### Modèle du Gaz Parfait (GP)

>[!formule] Equation d'état des gaz parfaits 
>$$P \cdot V = n \cdot R \cdot T$$
>- $R = 8,314 \text{ J.K}^{-1}\text{.mol}^{-1}$
>- Valable pour des pressions faibles (interactions négligeables).

### Phases condensées idéales

- **Modèle :** Incompressible et indilatable ($V = \text{cste}$).
- **Énergie interne :** $U$ ne dépend que de $T$ ($dU = C \cdot dT$).

---

## 2. Premier Principe & Énergie

> [!formule] Bilan d'énergie (Système fermé)
> $$\Delta U + \Delta E_{c,macro} + \Delta E_{p,ext} = W + Q$$
> En l'absence de variation d'énergie mécanique : $\Delta U = W + Q$

### Travail des forces de pression

> [!formule] 
> $$W = \int_{V_i}^{V_f} -P_{ext} \, dV$$
>- **Isochore ($V=const$) :** $W = 0$
>- **Monobare ($P_{ext}=const$) :** $W = -P_{ext}(V_f - V_i)$

### Enthalpie ($H$)

>[!formule] Définition : 
>$$H = U + PV$$
>- **Transformation monobare :** $\Delta H = Q_p$ (chaleur échangée à pression constante).
### Lois de Joule (Gaz Parfait)

1. **$U$ ne dépend que de $T$ :** $dU = C_v dT$
2. **$H$ ne dépend que de $T$ :** $dH = C_p dT$
- **Relation de Mayer :** $C_p - C_v = nR$

---

## 3. Second Principe & Entropie

> [!formule] Bilan entropique
> $$\Delta S = S_e + S_c$$
> - $S_e = \int \frac{\delta Q}{T_{ext}}$ (Entropie échangée)
> - $S_c \ge 0$ (Entropie créée, nulle si réversible)

### Lois de Laplace

*Condition : Gaz parfait, transformation adiabatique réversible (isentropique), $\gamma = C_p/C_v$ constant.*
- $P \cdot V^\gamma = \text{const}$
- $T \cdot V^{\gamma-1} = \text{const}$
- $P^{1-\gamma} \cdot T^\gamma = \text{const}$

---

## 4. Changements d'État (Corps Pur)
### Grandeurs de transition

Pour une transition de la phase 1 vers la phase 2 :
- **Enthalpie de changement d'état :** $\Delta_{1 \to 2} H = L_{12}$ (Chaleur latente).
- **Entropie de changement d'état :** $\Delta_{1 \to 2} S = \frac{L_{12}}{T_{eq}}$

---

## 5. Machines Thermiques
### Bilans sur un cycle ($\Delta U = 0, \Delta S = 0$)
- **1er Principe :** $W + Q_C + Q_F = 0$
- **Inégalité de Clausius :** $\frac{Q_C}{T_C} + \frac{Q_F}{T_F} \le 0$

### Performances de Carnot (Max théorique)
| Machine | Objectif | Efficacité / Rendement ($\le$) |
| :--- | :--- | :--- |
| **Moteur** | Produire $W < 0$ | $\eta = 1 - \frac{T_F}{T_C}$ |
| **Frigo** | Extraire $Q_F > 0$ | $e_f = \frac{T_F}{T_C - T_F}$ |
| **PAC** | Fournir $Q_C < 0$ | $e_c = \frac{T_C}{T_C - T_F}$ |

---
#Thermodynamique #Physique 
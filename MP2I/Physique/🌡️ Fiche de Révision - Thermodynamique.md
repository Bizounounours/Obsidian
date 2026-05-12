
> [!abstract] Sommaire
> 1. [[#I. Description du Système et Équilibre|Systèmes et Équations d'État]]
> 2. [[#II. Premier Principe Énergie et Enthalpie|Énergie & Premier Principe]]
> 3. [[#III. Second Principe Entropie et Évolution|Entropie & Second Principe]]
> 4. [[#IV. Transitions de Phase du Corps Pur|Équilibre du Corps Pur (Transitions)]]
> 5. [[#V. Machines Thermiques|Machines Thermiques (Cycles & Flux)]]

---

## I. Description du Système et Équilibre

> [!definition] Variables et État
> - **Système** : Ouvert (matière + énergie), Fermé (énergie seule), Isolé (rien).
> - **Variables Extensives** : Proportionnelles à $n$ ($V, m, U, S, H$). Additives.
> - **Variables Intensives** : Indépendantes de $n$ ($P, T, x, \text{masse volumique}$). Non additives.
> - **Équilibre Thermodynamique** : Implique l'équilibre mécanique ($P$ uniforme), thermique ($T$ uniforme) et chimique.

> [!formule] Modèle du Gaz Parfait (GP)
> Équation d'état : $$P \cdot V = n \cdot R \cdot T$$
> - $R = 8,314 \text{ J.K}^{-1}\text{.mol}^{-1}$.
> - Limite des gaz réels à basse pression ($P \to 0$).
> - Volume molaire aux CNTP ($0^\circ\text{C}, 1\text{ bar}$) : $V_m \approx 22,7 \text{ L.mol}^{-1}$.

> [!formule] Modèle de la Phase Condensée Idéale
> - **Incompressible** ($\chi_T = 0$) et **indilatable** ($\alpha = 0$).
> - Équation d'état : $V = \text{cste} = n \cdot V_m$.
> - L'énergie interne $U$ et l'enthalpie $H$ ne dépendent que de $T$.

---

## II. Premier Principe : Énergie et Enthalpie

### 1. Travail et Chaleur

> [!formule] Travail des forces de pression ($W$)
> $$\delta W = -P_{ext} \, dV$$
> - **Isochore ($V=const$)** : $W = 0$.
> - **Monobare ($P_{ext}=const$)** : $W = -P_{ext}(V_f - V_i)$.
> - **Isotherme quasi-statique (GP)** : $W = -nRT \ln(V_f/V_i)$.

> [!formule] Transfert thermique ($Q$)
> - **Sans changement d'état** : $\delta Q = C \cdot dT$ (avec $C = m \cdot c$ ou $n \cdot C_m$).
> - **Capacité thermique massique de l'eau** : $c_{eau} \approx 4,18 \text{ kJ.K}^{-1}\text{.kg}^{-1}$.
> - **Changement d'état** : $Q = m \cdot L$ (où $L$ est l'enthalpie massique de transition).

### 2. Bilans Énergétiques

> [!formule] Premier Principe (Système fermé)
> $$\Delta U + \Delta E_c + \Delta E_p = W + Q$$
> Au repos macroscopique : $\Delta U = W + Q$.

> [!definition] Enthalpie ($H$)
> Définition : $H = U + PV$.
> **Propriété capitale** : Pour une transformation **monobare** ($P_i = P_f = P_{ext}$), $\Delta H = Q_p$.

### 3. Lois de Joule et Capacités

> [!formule] Gaz Parfait et Joule
> - **1ère loi** : $dU = C_v dT$ (L'énergie interne ne dépend que de $T$).
> - **2ème loi** : $dH = C_p dT$ (L'enthalpie ne dépend que de $T$).
> - **Relation de Mayer** : $C_p - C_v = nR$.
> - **Coefficients** : $C_v = \frac{nR}{\gamma - 1}$ et $C_p = \frac{\gamma nR}{\gamma - 1}$ (avec $\gamma = C_p/C_v$).

---

## III. Second Principe : Entropie et Évolution

> [!definition] Le Second Principe
> Toute transformation crée de l'entropie : $$\Delta S = S_e + S_c$$
> - **Entropie échangée** : $S_e = \int \frac{\delta Q}{T_{ext}}$ (Si thermostat : $S_e = \frac{Q}{T_{source}}$).
> - **Entropie créée** : $S_c \ge 0$. ($S_c = 0$ si réversible, $S_c > 0$ si irréversible).

> [!formule] Identités Thermodynamiques
> 1. $dU = T \, dS - P \, dV$
> 2. $dH = T \, dS + V \, dP$

> [!formule] Variation d'Entropie (Gaz Parfait)
> - $\Delta S = n C_{v,m} \ln\left(\frac{T_f}{T_i}\right) + nR \ln\left(\frac{V_f}{V_i}\right)$
> - $\Delta S = n C_{p,m} \ln\left(\frac{T_f}{T_i}\right) - nR \ln\left(\frac{P_f}{P_i}\right)$

> [!formule] Lois de Laplace
> *Conditions : GP + Adiabatique + Réversible (Isentropique) + $\gamma$ constant.*
> 1. $P \cdot V^\gamma = \text{const}$
> 2. $T \cdot V^{\gamma-1} = \text{const}$
> 3. $P^{1-\gamma} \cdot T^\gamma = \text{const}$

---

## IV. Transitions de Phase du Corps Pur

> [!definition] Diagrammes et Points Critiques
> - **Point Triple** : Coexistence S, L et V.
> - **Point Critique** : Fin de la courbe de vaporisation. Au-delà : fluide supercritique.
> - **Pression de vapeur saturante $P_{sat}(T)$** : Pression d'équilibre liquide-vapeur.

> [!formule] Règle des Moments (ou du Levier)
> Pour un mélange Liquide + Vapeur de volume massique $v$ :
> $$x_v = \frac{m_{vap}}{m_{tot}} = \frac{v - v_{liq}}{v_{vap} - v_{liq}} = \frac{ML}{LV}$$
> *Où M est le point du système, L le point liquide saturé et V le point vapeur saturée.*

> [!formule] Grandeurs de Changement d'État
> - **Enthalpie massique** : $\Delta_{1 \to 2} h = L_{12}$ (ex: $L_{vap}$ pour Liq $\to$ Vap).
> - **Entropie massique** : $\Delta_{1 \to 2} s = \frac{L_{12}}{T_{eq}}$.

---

## V. Machines Thermiques

### 1. Bilans Cycliques (Dithermes)

> [!formule] Théorème de Clausius
> Sur un cycle ($\Delta U = 0, \Delta S = 0$) entre deux sources $T_C$ (chaude) et $T_F$ (froide) :
> 1. $W + Q_C + Q_F = 0$
> 2. $\frac{Q_C}{T_C} + \frac{Q_F}{T_F} \le 0$ (Inégalité de Clausius)

### 2. Performances de Carnot (Maximales)

| Machine | Objectif | Efficacité / Rendement | Carnot ($\le$) |
| :--- | :--- | :--- | :--- |
| **Moteur** | Travail $W < 0$ | $\eta = -W / Q_C$ | $1 - T_F/T_C$ |
| **Frigo** | Froid $Q_F > 0$ | $e_f = Q_F / W$ | $T_F / (T_C - T_F)$ |
| **PAC** | Chaud $Q_C < 0$ | $e_c = -Q_C / W$ | $T_C / (T_C - T_F)$ |

### 3. Thermodynamique Industrielle (Flux)

> [!formule] Premier Principe Industriel
> Pour un fluide en écoulement permanent dans une machine (turbine, compresseur) :
> $$\Delta (h + \frac{1}{2}c^2 + gz) = w_u + q$$
> - $w_u$ : Travail utile reçu (par kg de fluide).
> - $q$ : Transfert thermique reçu (par kg de fluide).

---
#Thermodynamique #Physique #Fiches 
# Compte Rendu

KEBICHE Ayrton
CHEVREL Jacob

## Observation initiale 

On a dans un premier temps effectué un balayage en fréquence, cela nous a permit d'observer que le montage se comporte comme un **passe-bas** à la difference que on observe un pic d'amplitude de sortie autour de 5 kHz où se trouve le maximum d'amplitude.

## Calculs et Diagramme de Bode 

On mesure par rapport au pic d'amplitude les fréquences de coupure

$f_{max}=5\text{ kHz}$

$f_{c^-}=4,08 \text{ Hz}$

$f_{c^+}=5,4 \text{ kHz}$

On a aussi une autre fréquence de coupure celle que l'on considere par rapport à la caractéristique de passe_bas, c'est à dire celle qui nous donne :

$G_{dB}(f)=-3$.

On obtient :

$f_{c}' = 7,4$ kHz 

![[Pasted image 20260317114959.png]]

Pour la phase on a $\phi$ à 1 kHz qui vaut $\pi$ 

Puis à 5 kHz qui est proche de $\frac{\pi}{2}$

Enfin à 15 kHz qui vaut 0 

## Application 1

On veut que les fréquences plus élévées du créneau soient très fortement atténuées. Ainsi comme nous avons un passe-bas il suffit de prendre comme fréquence dans le GBF un fréquence proche / légerement inférieur à $f_{c}'$ ce qui permet de ne pas atténuer ou d'amplifier la fréquence fondamentale du créneau. Ce qui nous laisse uniquement un sinus de fréquence fondamentale 

## Application 2

On veut obtenir la composante continue du signal. Pour cela on ajoute un offset au GBF et comme on a un passe-bas il nous suffit de mettre une fréquence d'entrée très élevée par rapport à $f_{c}'$ ce qui va atténuer très fortement les composantes sinusoïdales.


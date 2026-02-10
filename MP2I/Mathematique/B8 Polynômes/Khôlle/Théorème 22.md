
>[!question] Formule de Taylor pour un Polynôme
>Soit $\mathbb{K}$ un corps de caractéristique nulle, $n \in \mathbb{N}\ P \in \mathbb{K}_n[X] \iff \deg(P) \leq n$ et $\alpha \in \mathbb{K}$. Alors : 
>$$
>P(X) = \sum^{n}_{k=0} \frac{P^{(k)(\alpha)}}{k!}(X-\alpha)^k
>$$

>[!tip]+ Démonstration
><u>1er cas </u> : $\alpha = 0$
>
>Si $m=\deg(P)$, on a $m \leq n$ car $P \in \mathbb{K}_n[X]$. On peut écrire :
>$$
>P = \sum^{m}_{k=0}a_k X^k \text{où} a_m \not = 0
>$$
>On a :
>$$\begin{align}
>P' &= \sum^{m}_{k=1}k a_k X^{k-1} \\
>P'' &= \sum^{m}_{k=2}k (k-1) a_k X^{k-2} \\
>p^{(3)} &= \sum^{m}_{k=3}k (k-1) (k-2) a_k X^{k-3}
>\end{align}$$
>
>On conjecture que pour tout $i \in [\![1;m]\!]$
>$$\begin{align}
>P^{(i)} = \sum^{m}_{k=i}(k(k-1)\dots)
>\end{align}$$

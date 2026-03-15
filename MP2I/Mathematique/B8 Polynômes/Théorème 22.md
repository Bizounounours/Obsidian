
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
>P^{(i)} &= \sum^{m}_{k=i}\underbrace{(k(k-1)\dots(k-i+1))}_{\frac{k!}{(k-i)!}}a_kX^{k-i} \\
>&=\sum^{m}_{k=i}\frac{k!}{(kk-i)!}a_kXk^{k-i} \\
>&= \sum^{m-i}_{j=0}\frac{(j+i)!}{j!}a_{j+i}X^j \ \ \ \ \ \ \ \ j=k-i \\
>\end{align}$$
>
>Donc $P^(i)(0)=\frac{(0+i)!}{O!}a_{0+i}+0=i! \times a_i$ 
>
>Ainsi $\frac{P^{(i)}(0)}{i!}=a_i \ \ \ \ \ \heartsuit$
>
>Donc : $$P=\sum^{m}_{i=0}\frac{P^{(0)}(0)}{k!}X^k = \sum^{m}_{i=0}\frac{P^{(0)}(0)}{k!}(X-0)^k$$
>
>Or si $k>m$ on a $P^{(0)}=0$ donc $P^{(0)}(0)=0$ 
>On peut donc prolonger la somme jusqu'a $n \geq m$
>
>
><u>2eme cas</u> : $\alpha \in \mathbb{K}^*$
>
>Posons $Q(X) =P_0(X+\alpha) = P(X+\alpha)$
>On a $\deg Q = \deg P$, donc $Q \in \mathbb{K}_n[X]$
>On applique la formule précédente à $Q$
>$$
>Q=\sum^{n}_{k=0}\frac{Q^{(k)}(0)}{k!}(X-0)^k
>$$
>Or $Q(X)=P(X+\alpha)$ donc $Q(0)=P(\alpha)$
>$Q'(X)=(P_0(X+\alpha))'=P_0(X+\alpha)+(X+\alpha)'=P'(X+\alpha)$
>Donc $Q'(0)=P'(\alpha)$
>Par récurrence on prouverait $Q^{(k)}=P^{(k)}(\alpha)$ pour tout $k \in \mathbb{N}$
>
>Donc :
>$$
>Q=\sum^{n}_{k=0}\frac{P^{(k)}(\alpha)}{k!}X^k
>$$
>Or
>$$\begin{align}
>P(X) &= P(X-\alpha+\alpha)\\ \\
>&=Q(X-\alpha)\\ \\
>&= Q \circ (X-\alpha)\\ \\
>&=\left(\sum^{n}_{k=0}\frac{P^{(k)}(\alpha)}{k!}X^k\right) \circ (X-\alpha)\\ \\
>&=\sum^{n}_{k=0}\frac{P^{(k)}(\alpha)}{k!}(X-\alpha)^k
>\end{align}$$
>
>D'où le résultat.



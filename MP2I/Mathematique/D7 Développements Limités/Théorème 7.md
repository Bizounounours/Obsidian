### Développements limités des fonctions usuels en 0 :



Toutes les fonctions considérés ici sont de classe $C^{\infty}$ en $0$
Pour tout $n \in \mathbb{N}$, on peut donc leur appliquer la formule de Taylor-Young :
$$
f(x) \underset{x \to 0} {=} \sum^{n}_{k=0} \frac{f^{k}(0)}{k!} \times x^k + o(x^n)
$$
Il suffit donc de calculer $f^{(k)}(0)$ pour $k \in \mathbb{N}$

> [!colles]+ $e^{x}$
> $$\begin{align}
> \exp^{k}(0)=\exp(0)=1 \ \ \text{Donc : } \\
> \exp(x)=\sum^{n}_{k=0} \frac{1}{k!}+o(x^n)\\
> \end{align}
> $$

> [!colles]+ $\cos(x)$
> $$
> \left.
> \begin{align}
> &\cos^{(0)}=\cos \\
> &\cos^{(1)}=-\sin \\
> &\cos^{(2)}=-\cos \\
> &\cos^{(3)}=\sin  \\
> &\cos^{(4)}= \cos 
> \end{align}
> \right\} \text{La suite }(\cos^{(k)})_{k \in \mathbb{N}} \text{ est périodique de période 4}
> $$
> Ainsi 
> $$\begin{align}
> \forall k \in \mathbb{N}, \cos^{(k)} &= \begin{cases} \cos  & \text{si } k \equiv 0 \ [4] \\ -\sin & \text{si } k \equiv 1 \ [4] \\ -\cos & \text{si } k \equiv 2 \ [4] \\ \sin  & \text{si } k \equiv 3 \ [4] \end{cases} \\ \\
> \implies \forall k \in \mathbb{N}, \quad \cos^{(k)}(0) &= 
>\begin{cases} 
>\left.
>\begin{aligned}
>1   \text{   si } k \equiv 0 \ [4] \\
>-1  \text{   si } k \equiv 2 \ [4]
>\end{aligned}
>\right\} k \text{ est pair} \\
>0  \text{   sinon}
>\end{cases}
> \end{align}
> $$


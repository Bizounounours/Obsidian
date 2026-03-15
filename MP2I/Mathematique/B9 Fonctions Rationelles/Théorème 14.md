### Décomposition Polaire

![[Enonce14.png]]

> [!colles]+ Démonstration
> 
> $F ∈ \mathbb{K}(X)$ donc on peut écrire $F=\frac{P}{T}$ où $P,T ∈ \mathbb{K}[X]$ tels que $P ∧ T=1$
> Si $\alpha$ est un pôle de $F$ de multiplicité $k$ alors comme $P ∧ T=1$ on a que $\alpha$ est une racine de $T$ de multiplicité $k$
> 
> Par théorème il existe $Q ∈ \mathbb{K}[X]$ tel que 
> $$T=(X-\alpha)^k.Q \ \ \ \ \text{où} \ Q(\alpha)=0$$ 
> On a ainsi $F= \frac{P}{(X-\alpha)^k.Q}$ où $Q(\alpha)=0$ et $P(\alpha)\neq 0$ car $P ∧ T=1$ avec $T(\alpha)=0$
> 
> 
> #### Existence :
> 
> Comme les diviseurs $(X-\alpha)^k$ sont les polynômes de la forme $\lambda(X-\alpha)^k$ où $\lambda ∈ \mathbb{K}^*$ et $i ∈[\![0,k]\!]$ et comme $Q(\alpha)\neq \implies(X-\alpha)\nmid Q$, on en déduit $(X-\alpha)^k ∧ Q=1$
> 
> Par Bézout, il existe $U,V ∈ \mathbb{K}[X]$ tel que 
> $$
> \begin{align}
> &U × (X-\alpha)^k + V × Q = 1 \\ \\
> \implies &P×U(X-\alpha)^k+PV×Q=P \\ \\
> \implies &\frac{P}{(X-\alpha)^k×Q}= \frac{PU(X-\alpha)^k + PVQ}{(X-\alpha)^k×Q} \\ \\
> \implies &F=\frac{PU}{Q}+\frac{PV}{(X-\alpha)^k}\\
> \end{align}
> $$
> 
> Par division euclidienne on a : 
> $$
> PV=(X-\alpha)^k × T + R \ \ \ \ \text{où}\ \deg R<k
> $$
> Ainsi :
> $$
> \begin{align}
> F&=\frac{PU}{Q}+T+\frac{R}{(X-\alpha)^k} \\ \\
> &=\frac{PU+TQ}{Q}+\frac{R}{(X-\alpha)^k×Q}
> \end{align}
> $$
> Ainsi $A=R$ et $B=PU+TQ$ conviennent 
> 
> 
> #### Unicité
> 
> Supposons avoir 
> $$
> F=\frac{A_{1}}{(X-\alpha)^k}+\frac{B_{1}}{Q}=\frac{A_{2}}{(X-\alpha)^k}+\frac{B_{2}}{Q}
> $$
> où $A_{1},A_{2},B_{1},B_{2} ∈ \mathbb{K}[X]$ tels que $\deg A_{1},\deg A_{2} <k$
> D'où 
> $$\begin{align}
> &\frac{A_{1}-A_{2}}{(X-\alpha)^k}=\frac{B_{2}-B_{1}}{Q} \\ \\
> \implies &(A_{1}-A_{2})Q=(B_{2}-B_{1})(X-\alpha)^k \ \ \ \ \bigstar
> \end{align}$$
> Ainsi $(X-\alpha)^k ∣(A_{1}-A_{2})Q$, or $(X-\alpha)^k∧Q=1$ donc $(X-\alpha)^k ∣A_{1}-A_{2}$
> Or $\deg(A_{1}-A_{2})<k=\deg (X-\alpha)^k$ car $\deg A_{1},\deg A_{2}<k$
> Donc $A_{1}-A_{2}=0$, et ainsi $A_{1}=A_{2}$
> En injectant cette relation dans $\bigstar$ il vient $B_{1}=B_{2}$


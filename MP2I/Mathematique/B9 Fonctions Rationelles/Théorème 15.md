### Partie polaire d’un pôle simple. Résidu associé.

![[Enonce15.png]]

> [!colles]+ Démonstration
> 
> ##### i)
> 
> Comme $\alpha$ est un pôle de $F$ de multiplicité $1$, le [[Théorème 14]] permet d'écrire 
> $$
> \begin{align}
> F &= \frac{P}{(X-\alpha)^k×\hat{Q}} \ \ \ \ \ \text{où}\  P(\alpha)\neq 0,\hat{Q}(\alpha)\neq 0 \\  \\
> &=\frac{A(X)}{X-\alpha}+\frac{B(X)}{\hat{Q}} \ \ \ \ \ \text{où}\ A,B ∈ \mathbb{K}[X] 
> \end{align}
> $$
> De plus $\deg A < \deg(X-\alpha)=1$ donc $A=\lambda ∈ \mathbb{K}$
> On a donc
> $$
> F=\frac{\lambda}{X-\alpha}+\frac{B(X)}{\hat{Q}(X)}
> $$
> Si $\lambda=0$, il vient $F=\frac{B(X)}{\hat{Q}(X)}$ où $\hat{Q}(\alpha)neq 0$ ce qui contredit le fait que $\alpha$ est un pôle de F.
> Donc $\lambda ∈ \mathbb{K}^*$
> 
> 
> ##### ii)
> 
> On en déduit 
> $$
> \begin{align}
> &F(X).(x-\alpha)=\lambda+(X-\alpha)\frac{B(X)}{\hat{Q}(X)} \\ \\
> \implies &\left. F(X).(X-\alpha)\right|_{X = \alpha}=\lambda(\alpha-\alpha) \frac{B(\alpha)}{\hat{Q}(\alpha)}=\lambda
> \end{align}
> $$
> 
> 
> ##### iii)
> 
> On a 
> $$
> \begin{align}
> &F=\frac{P}{Q}=\frac{P}{(X-\alpha).\hat{Q}} \\ \\
> \implies &\left. F(X)(X-\alpha)\right|_{X=\alpha}=\frac{P(\alpha)}{\hat{Q}(\alpha)} \\ \\
> \implies &\lambda=\frac{P(\alpha)}{\hat{Q}(\alpha)}
> \end{align}
> $$
> Il reste à prouver $\hat{Q}(\alpha)=Q'(\alpha)$
> Or on a 
> $$
> \begin{align}
> &Q(X)=(X-\alpha).\hat{Q}(X) \\
> \implies &Q'(X)=\hat{Q}(X)+(X-\alpha)\hat{Q}'(X) \\
> \implies &Q'(\alpha)= \hat{Q}(\alpha) \\
> \end{align}
> $$
> D'où le résultat


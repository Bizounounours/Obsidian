### $F$ s’écrit de manière unique $F = E + G$

![[B9.png]]

> [!colles]+ Démonstration
> #### Existence:
> 
> La division euclidienne de $P$ par $Q$ donne 
> $$P =B \times Q + R$$
> où $\deg R < \deg Q$
> Donc :
> $$F=\frac{P}{Q}=\frac{BQ+R}{Q}=B+\frac{R}{Q}$$
> Or $B \in \mathbb{K}[X]$ et $\deg\left( \frac{R}{Q} \right)=\deg R-\deg Q <0$
> D'où l'éxistence 
> 
> 
> #### Unicité
> 
> Supposons avoir :
> $$F=E_1+g_{1}=E_{2}+G_{2}$$
> où $E_{1},E_{2} \in \mathbb{K}[X], G_{1},G_{2} \in \mathbb{K}(X)$ tels que $\deg G_{1}, \deg G_{2} < 0$
> 
> On en déduit $E_{1}-E_{2}=G_{1}-G_{2} \ \ \ \star$
> Donc $\deg E_{1}-E_{2}= \deg G_{1}-G_{2}\leq \max\{\deg G_{1}, \deg G_{2}\}<0$
> Or $E_{1}-E_{2} \in \mathbb{K}[X]$ donc $E_{1}-E_{2}=0$
> 
> Ainsi $E_{1}=E_{2}$, et il reste $G_{1}=G_{2}$ dans $\star$



### Décomposition en éléments simples de $\frac{P′}{P}$ avec $P ∈ \mathbb{C}[X]$

![[Enonce20.png]]

>[!colles]+ Démonstration
>
>Comme $\alpha$ est une racine de $P$ de multiplicité $\mu$, on a $\nu_{\alpha_{i}}(P)=\mu_{i}$ et $\nu_{\alpha_{i}}(P')=\mu_{i}-1$
>Donc $\nu_{\alpha_{i}}\left( \frac{P'}{P} \right)=\nu_{\alpha_{i}}(P')-\nu_{\alpha_{i}}(P)=-1$
>
>$P$ n'ayant pas d'autre racine que $\alpha_{1},\dots,\alpha_{r}$; on en déduit que les pôles de $\frac{P'}{P}$ sont $\alpha_{1},\dots,\alpha_{r}$ et ils sont de multiplicité $1$
>
>Soit $dln : \cases{\mathbb{C}[X] \backslash \lbrace 0 \rbrace \longrightarrow \mathbb{C}[X]\\ P \longmapsto \frac{P'}{P}}$
>$dln$ est un morphisme de groupe de $(\mathbb{C}[X] \backslash \{0\},X)$ vers $(\mathbb{C}[X],+)$
>
>En effet
>$$
>\begin{align}
>dln(P×Q)&=\frac{(P×Q)'}{P×Q} \\ \\
>&=\frac{P'Q+PQ'}{P×Q} \\ \\
>&=\frac{P'}{P}+\frac{Q'}{Q} \\ \\
>&=dln(P)+dln(Q)
>\end{align}
>$$
>On a alors, considérant que $P$ s'écrit : 
>$$
>P=\lambda \prod^{r}_{i=1}(X-\alpha_{i})^{\mu_{i}} \ \ \ \ \ \\text{où} \ \lambda ∈ \mathbb{C}^*
>$$
>On a :
>$$
>\begin{align}
>\frac{P'}{P}&=dln(P) \\ \\
>&= dln(\lambda \prod^{r}_{i=1}(X-\alpha_{i})^{\mu_{i}}) \\
>&=dln(\lambda)+\sum^{r}_{i=1}dln((X-\alpha_{i})^{\mu_{i}})
>\end{align}
>$$
>Or $dln(\lambda)=\frac{\lambda'}{\lambda}=0$ et 
>$$
>\begin{align}
>dln((X-\alpha_{i})^{\mu_{i}})&= \frac{((X-\alpha_{i})^{\mu_{i}})'}{(X-\alpha_{i})^{\mu_{i}}} \\ \\ \\
>&=\frac{\mu_{i}(X-\alpha_{i})^{\mu_{i}-1}}{(X-\alpha_{i})^{\mu_{i}}}\\  \\
>&=\frac{\mu_{i}}{X-\alpha_{i}}
>\end{align}
>$$
>Ainsi
>$$\frac{P'}{P}=\sum^{r}_{i=1}\frac{\mu_{i}}{X-\alpha_{i}}$$




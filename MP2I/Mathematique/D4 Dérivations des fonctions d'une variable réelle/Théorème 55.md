
>[!question] Inégalité de Taylor-Lagrange
>
>Soient $n ∈ N$ et $f : [a, b] → R$ une fonction de classe $C^{n+1}$. On a : 
>$$
> \left|f(b) −\sum_{k=0}^n \frac{f^{(k)}(a)}{k!} (b − a)^k \right| \leq \frac{(b − a)^{n+1}}{(n + 1)!} \sup_{x∈[a,b]}\left|f^{(n+1)}(x)\right|
>$$

>[!tip]+ Démonstration
>La formule de Taylor avec reste intégral donne :
>$$
>f(b)-\sum^{n}_{k=0}\frac{f^{(n+1)}(a)}{k!}(b-a)^k=R_n
>$$
>Or 
>$$
>|R_n|=\left|\int^{b}_{a}\frac{f^{(n+1)}}{n!}\underbrace{(b-t)^n}_\text{$\geq 0$ car $t \in [a,b]$} dt \right| \leq \int^{b}_{a}\frac{\left|f^{(n+1)}\right|}{n!}(b-t)^n dt
>$$
>
>Or $g:t \longmapsto \left| f^{(n+1)}(t) \right|$ est continue par composé de fonctions continues 
>($f^{(n+1)}$ est continue car f est de classe $C^{n+1}$)
>
>Par le théorème des bornes atteintes, comme $g$ est $C^0$ sur $[a,b]$, il existe donc $\alpha \in [a,b]$ tel que 
>$$
>\sup_{x \in [a,b]}g(x)=g(\alpha)
>$$
>
>En particulier $M=\sup_{x \in [a,b]}\left|f^{n+1}(x)\right|$ est fini et on a :
>$$\begin{aligned}
>& \forall t \in [a,b], \left|f^{(n+1)}(x)\right| \leq M\\\\
>\implies & \forall t \in [a,b],\frac{\left|f^{(n+1)}(x)\right|}{n!}(b-t)^n \leq M \times \frac{(b-t)^n }{n!}\\\\
>\implies & \int^{b}_{a}\frac{\left|f^{(n+1)}(x)\right|}{n!}(b-t)^n dt \leq \int^{b}_{a}M \times \frac{(b-t)^n }{n!}dt\\\\
>\implies & \left|R_n\right| \leq M \times \int^{b}_{a}\frac{(b-t)^n }{n!}dt
>\end{aligned}$$
>
>Or $\int^{b}_{a}\frac{(b-t)^n}{n!}dt=\left[\frac{(b-t)^{n+1}}{n!}dt \right]^{b}_{a} = 0 + \frac{(b-a)^{n+1}}{(n+1)!}$
>
>D'où   $\left|R_n \right| \leq M \times \frac{(b-t)^{n+1}}{(n+1)!}$


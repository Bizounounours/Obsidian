
## Théorème 48

>[!question] Limites de dérivée
>Soient $f : I → R$ une fonction, $x_0 ∈ I$ et $ℓ_2 ∈ R$. On suppose que : 
>
>i) $f$ est continue sur $I$. 
>
>ii) $f$ est dérivable sur $I \ \textbackslash \ \{x_0\}$. 
>
>iii) $lim_{\substack{x→x_0 \\ x \neq x0}} \ f'(x) = \ell_2$

>[!tip] Démonstration
>Pour $x \neq x_0$, considérons:
>$$\tau_{x_0}(x) = \frac{f(x) - f(x_0)}{x-x_0} $$
>
>==<u>1er cas</u>== : si $x>x_0$
>$f$ est continue sur $[x_0,x]$, et dérivable sur $]x_0,x[$ donc par le théorème des acroissements finis, il existe $c_x \in ]x_0,x[$ tel que 
>$$(\star)\ \ \frac{f(x)-f(x_0)}{x-x_0}=f'(c_x)$$
>Or on a :
>$$x_0 < c_x < x \implies \lim_{x\to x_0^+}\ x_0  = x_0 < \lim_{x\to x_0^+}\ c_x < \lim_{x \to x_0^+}\ x=x_0$$
>Le lemme des gendarmes donne : 
>$$\lim_{x\to x_0^+}\ c_x=x_0$$
>Par composition on a en faisant tendre $x$ vers $x_0^+$ dans ($\star$) :
>$$\lim_{x \to x_0^+}\ \tau_{x_0}=\lim_{x \to x_0^+}\ f'(c_x)=\ell_2$$
>
>
>==<u>2eme cas</u>== : si $x<x_0$
>On prouve de même 
>$$\lim_{x \to x_0^-}\ \tau_{x_0}(x)=\ell_2$$
>
>Finalement on obtient 
>$$\lim_{x \to x_0}\ \tau{x_0}(x)=\ell_2$$
>D'où le résultat

--------------------------------------------------------------------
--------------------------------------------------------------------
## Théorème 53

>[!question] Formule de Taylor
>Soient $n ∈ N, f : I → R$ et $x_0 ∈ I$. Si $f$ est de classe $C^{n+1}$ sur $I$, alors pour tout $x ∈ I$ : 
>$$f (x) = \sum^{n}_{k=0} \frac{ f^{(k)}(x_0)}{k!} (x−x_0)^k + \int^{x}_{x_0} \frac{f^{(n+1)}(t)}{n!} (x − t)^n dt$$ 
>Et si on considère une fonction $f : [a, b] → R$ de classe $C^{n+1}$ on a : 
>$$f (b) = \sum^{n}_{k=0} \frac{ f^{(k)}(a)}{k!} (b−a)^k + \int^{b}_{a} \frac{f^{(n+1)}(t)}{n!} (b − t)^n dt$$

>[!tip] Démonstration 
>
>Prouvons la formule par récurrence sur $n \in \mathbb{N}$ :
>
><u>Initialisation</u> : En $n=0$ on a pour $f$ de classe $C^{0+1}=C^1$
>
>$$\begin{aligned} 
>\sum^{0}_{k=0} \frac{f^{(k)}(a)}{k!}(b-a)^k + \int^{b}_{a}\frac{f^{(1)}(t)}{0!}(b-t)^0dt  &= f(a) + \int^{b}_{a}f'(t)dt \\ 
>&= f(a) + [f(t)]^{b}_{a} \\ 
>&= f(a) + f(b) - f(a) \\ 
>&= f(b) 
>\end{aligned}$$
>
><u>Hérédité</u> : Supposons la propriété vérifiée au rang $n\in \mathbb{N}$
>Soit $f$ de classe $C^{n+2}$. En particulier $f$ est de classe $C^{n+1}$, donc par hypothèse de récurrence 
>$$f(b) = \sum^{n}_{k=0}\frac{f^{(t)}(a)}{k!}(b-a)^k+R_n$$
>où
>$$\begin{aligned}
>R_n &= \int^{b}_{a}\frac{f^{(n+1)}}{n!}(b-t)^n dt\\
>&=\int^{b}_{a} f^{n+1}(t) \times \frac{d}{dt}(\frac{-(b-t)^{n+1}}{(n+1)!})dt
\end{aligned}$$
>
>Or $f$ est de classe $C^{(n+1)}$ , donc $f^{(n+1)}$ est de classe $C^1$
>De même $t\longmapsto \frac{(b-t)^{n+1}}{(n+1)!}$ est $C^1$
>
>D'où en integrant par parties
>$$\begin{aligned}
>R_n &= \left[f^{(n+1)}(t)\times \frac{-(b-t)^{n+1}}{(n+1)!} \right]^b_a - \int^{b}_{a} \frac{d}{dt}(f^{(n+1)}(t)) \times \frac{-(b-t)^{n+1}}{(n+1)!}dt\\ \\
>&=f^{(n+1)}(a)\times \frac{-(b-a)^{n+1}}{(n+1)!} + \int^{b}_{a} f^{(n+2)}(t) \times \frac{(b-t)^{n+1}}{(n+1)!}dt\\ \\
>&=f^{(n+1)}(a)\times \frac{-(b-a)^{n+1}}{(n+1)!} + R_{n+1}
\end{aligned}$$

____________________________________________________________________
____________________________________________________________________
## Théorème 55

>[!question] Inégalité de Taylor-Lagrange
>
>Soient $n ∈ N$ et $f : [a, b] → R$ une fonction de classe $C^{n+1}$. On a : 
>$$
> \left|f(b) −\sum_{k=0}^n \frac{f^{(k)}(a)}{k!} (b − a)^k \right| \leq \frac{(b − a)^{n+1}}{(n + 1)!} \sup_{x∈[a,b]}\left|f^{(n+1)}(x)\right|
>$$

>[!tip] Démonstartion
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
>Par le théorème des bornes atteintes, comme $g$ est $C^0$ sur $[a,b]$, il existe donc $d \in [a,b]$ tel que 
>$$
>\sup_{x \in [a,b]}g(x)=g(\alpha)
>$$
>
>En particulier $M=\sup_{x \in [a,b]}\left|f^{n+1}(x)\right|$ est fini et on a :
>$$\begin{aligned}
>& \forall t \in [a,b], \left|f^{(n+1)}(x)\right| \leq M\\\\
>\implies & \forall t \in [a,b],\frac{\left|f^{(n+1)}(x)\right|}{n!}(b-t)^n \leq M \times \frac{(b-t)^n }{n!}\\\\
>\implies & \int^{b}_{a}\frac{\left|f^{(n+1)}(x)\right|}{n!}(b-t)^n dt \leq \int^{b}_{a}M \times \frac{(b-t)^n }{n!}dt\\\\
>\implies & \left|R_n\right| \leq m \times \int^{b}_{a}\frac{(b-t)^n }{n!}dt
>\end{aligned}$$
>
>Or $\int^{b}_{a}\frac{(b-t)^n}{n!}dt=\left[\frac{(b-t)^{n+1}}{n!}dt \right]^{b}_{a} = 0 + \frac{(b-a)^{n+1}}{(n+1)!}$
>
>D'où   $\left|R_n \right| \leq M \times \frac{(b-t)^{n+1}}{(n+1)!}$

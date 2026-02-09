
>[!question] Formule de Taylor
>Soient $n ∈ N, f : I → R$ et $x_0 ∈ I$. Si $f$ est de classe $C^{n+1}$ sur $I$, alors pour tout $x ∈ I$ : 
>$$f (x) = \sum^{n}_{k=0} \frac{ f^{(k)}(x_0)}{k!} (x−x_0)^k + \int^{x}_{x_0} \frac{f^{(n+1)}(t)}{n!} (x − t)^n dt$$ 
>Et si on considère une fonction $f : [a, b] → R$ de classe $C^{n+1}$ on a : 
>$$f (b) = \sum^{n}_{k=0} \frac{ f^{(k)}(a)}{k!} (b−a)^k + \int^{b}_{a} \frac{f^{(n+1)}(t)}{n!} (b − t)^n dt$$

>[!tip]+ Démonstration 
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


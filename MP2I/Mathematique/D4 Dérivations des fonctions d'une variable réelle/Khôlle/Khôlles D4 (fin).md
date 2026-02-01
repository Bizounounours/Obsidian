

>[!question] Théorème 48 (Limites de dérivée)
>Soient $f : I → R$ une fonction, $x_0 ∈ I$ et $ℓ_2 ∈ R$. On suppose que : 
>
>i) $f$ est continue sur $I$. 
>
>ii) $f$ est dérivable sur $I \ \textbackslash \ \{x_0\}$. 
>
>iii) $lim_{\substack{x→x_0 \\ x \neq x0}} \ f'(x) = \ell_2$

^ffaf6e

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


>[!question] Théorème 53 (Formule de Taylor)
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
>&=\int^{b}_{a}
\end{aligned}$$
>





>[!info] Théorème 48 (Limites de dérivée)
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


### Toute permutation d’un ensemble fini de cardinal $n$ est le produit d’au plus $n − 1$ transpositions.

![[B10.pdf#page=4&rect=11,706,585,755|B10, p.4]]


> [!colles]- Démonstration
> 
> On raisonne par récurrence sur $n\in \mathbb{N}^*$
> Il suffit de prouver le résultat si $E\in[\![1,n]\!]$
> 
> <mark style="background: #FFB8EBA6;"><u>Initialistation</u> : </mark>
> En $n=1$, on a $E=\{1\}$ donc $S_{1}=\{id\}$. Or $id$ est le produit de $0$ transposition
> $$
> \prod_{\mathscr{T}\in \varnothing}\mathscr{T}=id \ \ \text{ par convention}
> $$
> En $n=2$, on a $E=\{1,2\}$ donc $S_{2}=\{id,(1,2)\}$. Or $id$ et $(1,2)$ sont les produit d'au plus $2-1=1$ transposition 
> 
> <mark style="background: #FFB8EBA6;"><u>Hérédité</u></mark> : Supposons la propriété vérifié au rang $n \in \mathbb{N}$
> Soit $\sigma \in S_{n+1}$
> 
> <font color= "cyan">1er cas</font> : si $\sigma(n+1)=n+1$
> ![[Théoréme 19.png|250]]
> On a donc $\sigma([\![1,n]\!])=[\![1,n]\!]$
> Soit $\sigma'$ la restriction à la source et au but de $\sigma$ à $[\![1,n]\!]$
> On a donc $\sigma'\in S_{n}$
> Par hypothèse de récurrence il existe des transpositions $\mathscr{T_{1}},\dots,\mathscr{T_{p}}\in S_{n}$ où $p\leq n-1$ telles que $\sigma'=\mathscr{T_{1}}\dots\mathscr{T_{p}}$
> On prolonge alors $\mathscr{T_{i}}(n+1)=n+1$
> On a alors $\sigma=\tilde{\mathscr{T_{1}}} \dots \tilde{\mathscr{T}_{p}}$ où $p\leq n-1<(n+1)-1$
> 
> <font color= "cyan">2e cas</font> : $\sigma(n+1)=i\neq n+1$
> On considère $\sigma'(i \ \ \ \  n+1)\sigma$
> On a $\sigma'\in S_{n+1}$ et posons $\mathscr{T}_{i,n+1}=(i \ \ \ \  n+1)$
> On a 
> $$
> \begin{align}
> \sigma'(n+1)&=\mathscr{T}_{i,n+1}\sigma(n+1)
> &=\mathscr{T}_{i,n+1}(i)
> &=n+1
> \end{align}
> $$
> Par le 1er cas, il existe des transpositions $\mathscr{T_{1}},\dots,\mathscr{T_{p}}$ où $p\leq n-1$ telles que :
> $$
> \begin{align}
> &\sigma'=\mathscr{T_{1}}\dots\mathscr{T_{p}} \\
> \implies &\mathscr{T}_{i,n+1}\sigma=\mathscr{T_{1}}\dots\mathscr{T_{p}} \\
> \implies &\sigma=\mathscr{T}_{i,n+1}^{-1}\mathscr{T_{1}}\dots\mathscr{T_{p}}
> \end{align}
> $$
> Or $\mathscr{T}_{i,n+1}^{-1}=\mathscr{T}_{i,n+1}$ donc $\sigma$ est le produit de $p+1\leq(n-1)+1=(n+1)-1$ transpositions

---
#Maths #B10_Groupe_Symétrique
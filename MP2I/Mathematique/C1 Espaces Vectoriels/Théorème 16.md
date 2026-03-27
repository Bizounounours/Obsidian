
### Une famille finie est liée si et seulement si l’un de ses vecteurs est combinaison linéaire des autres

![[enonce23.png]]


> [!colles]+ Démonstration
> 
> ##### i)
> 
> Soit $\mathscr{F}=(u_{i})_{1\leq I\leq p}$ une famille de vecteurs de $E$
> 
> $\underline{\impliedby}:$ Supposons qu'il existe $i_{0}∈[\![1,p]\!]$ tel que $u_{i_{0}}$ soit de la forme :
> $$
> \begin{align}
> &u_{i_{0}} = \sum^{p}_{\substack{i=1\\ i\neq i_{0}}} \lambda_{i}.u_{i} \\
> \implies &1.u_{i_{0}}- \sum^{p}_{\substack{i=1\\ i \neq 0}}\lambda_{i}.u_{i}=0_{E} 
> \end{align}
> $$
> En posant $\mu_{i}=\cases{1 \text{ si }i=0 \\ -\lambda_{i} \text{ si }i \neq i_{0}}$ on obtient: 
> $$
> \sum^{p}_{i=1} \mu_{i.u_{i}} = 0_{E} \text{ et } \mu_{i_{0}}\neq O_{\mathbb{K}}
> $$
> Donc la famille est liée.
> 
> $\underline{\implies}$: Supposons que $\mathscr{F}$ est liée.
> Il existe alors $(\lambda_{i})_{1\leq i \leq p} ∈ \mathbb{K}^p$ tels que :
> $$
> \sum^{p}_{i=1} \lambda_{i}.u_{i} = 0_{E} \ \ \ \ \ \bigstar
> $$ 
> De plus les $\lambda_{i}$ sont non tous nuls donc il existe $i_{0} ∈ [\![1;p]\!]$ tel que $\lambda_{i_{0}} \neq 0_{\mathbb{K}}$
> On a alors :
> $$
> \begin{align}
> \star &\implies \lambda_{i_{0}}.u_{i_{0}} + \sum^{p}_{\substack{i=1\\i \neq i_{0}}} \lambda_{i}.u_{i}=0_{E} \\
> &\implies u_{i_{0}}= \sum^{p}_{\substack{i=1\\ i \neq i_{0}}} \underbrace{\frac{\lambda_{i}}{\lambda_{i_{0}}}}_{∈ \mathbb{K}}.u_{i} \ \ \ \ \text{car } \lambda_{i_{0}} \neq 0_{\mathbb{K}}
> \end{align}
> $$
> D'où le résultat
> 
> 
> ##### ii)
> 
> $\underline{\impliedby}$: Si $u_{p+i}$ est une combinaison linéaire de $u_{1},\dots,u_{p}$, alors $(u_{i})_{1 \leq i \leq p+1}$ est liée par <mark style="background: #ABF7F7A6;">i)</mark>
> 
> $\underline{\implies}$: Supposons $(u_{i})_{1\leq i\leq p+1}$ est liée
> Il existe $\lambda_{1},\dots,\lambda_{p+1}$ non tous nuls tels que 
> $$
> \sum^{p+1}_{i=1} \lambda_{i}.u_{i}=0_{E} \ \ \ \star
> $$
> Supposons $\lambda_{p+1}=0$ alors : 
> $$
> \begin{align}
> \star &\implies \sum^{p}_{i=1} \lambda_{i}+u_{i}+0_{E}=0_{E}  \\
> &\implies \lambda_{1}=\dots=\lambda_{p}=0_{\mathbb{K}}
> \end{align}
> $$
> Cela contredit "$\lambda_{1},\dots,\lambda_{p+1}$ non tous nuls"
>  On a donc $\lambda_{p+1}\neq 0_{\mathbb{K}}$
>  $$
>  \begin{align}
>  \star &\implies \sum^{p}_{i=1}\lambda_{i}.u_{i}+\lambda_{p+1}.u_{p+1}=0_{E} \ \ \ \ \text{car } \lambda_{p+1}\neq 0_{\mathbb{K}} \\
>  &\implies u_{p+1}= \sum^{p}_{i=1} - \frac{\lambda_{i}}{\lambda_{p+1}}.u_{i}
>  \end{align}
>  $$
>  D'où le résultat

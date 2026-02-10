
>[!question] Théorème de Bézout
>Soient $n \in \mathbb{N}$ et $A_1, \dots, A_n \in \mathbb{K}[X]$. Il existe $U_1, \dots, U_n \in \mathbb{K}[X]$ tels que : 
>$$
>\sum^{n}_{i=1}A_{i}U_{i} = \bigwedge^{n}_{i=1}A_i
>$$

>[!tip]+ Démonstartion 
>- Si $\forall i \in [\![ 1;n ]\!], \ A_i=0$, alors $\bigwedge^{n}_{i=1}A_i=0$ par convention. Il suffit alors de prendre $U_i=0$ pour tout $i \in [\![1,n]\!]$
>  >
>- S'il existe $i_0 \in [\![1;n]\!]$ tel que $A_{i_0} \neq 0$
>  On pose :
>  $$
> I = \left\lbrace \sum^{n}_{i=1}A_i U_i, \ (U_1, \dots, U_n)\in \mathbb{K}[X]^n \right\rbrace \\
> $$
> $$
> J= \lbrace deg(P), P \in I \ \backslash \lbrace0\rbrace \rbrace
> $$
> $J \subset \mathbb{N}$, de plus $J \neq \varnothing$ car $A_{i_0} \in I \ \backslash \lbrace0\rbrace$
> En effet on a :
> $$
> A_{i_0}= \sum^{n}_{i=0}A_iU_i \ \ \text{où} \ \ U_i = \cases{0 \ \text{si} \ i \neq i_0 \\ 1 \ \text{si} \ i=i_0}
> $$
> 
> Donc $\deg(A_{i_0}) \in J$
> $J$ est une partie non vide de $\mathbb{N}$, elle admet donc un plus petit élément $p=\min J$
> 
> Soit ensuite $D \in I \ \backslash \ \cases{0}$ tel que $\deg D = p$
> Il existe donc $V_1, \dots, V_n \in \mathbb{K}[X]$ tels que 
> $$D =  \sum^{n}_{i=1}A_i \times V_i$$
> 
> Montrons $D= \bigwedge^{n}_{i=1}$, ce qui terminera la démonstration
> 
> Soit $P \in \mathbb{K}[X]$. Si on a $P | A_i$ pour tout $i \in [\![1;n]\!]$, alors $P|\sum^{n}_{i=1}A_iV_i$ et $P|D$
> Ainsi $\deg P \leq deg D$
> 
> Il suffit de prouver que $D|A$ pour tout $i \in [\![1;n]\!]$
> Soit $i_1 \in [\![1;n]\!]$. On effectue la division euclidienne :
> $$\begin{align}
> &A_{i_1} = D \times Q+R \ \ \text{où} \ \ \deg R < \deg D \\
> \implies &R=A_{i_0}-D \times Q
>\end{align}$$
>
>On a $A_{i_1} \in I$ et $D \in I$. Pour en déduire $R \in I$ il suffit de prouver que $I$ est un sous-groupe de $(\mathbb{K}[X], +)$ et que I est absorbant pour le produit .
>$$(M \in I \ \text{et}\ P \in \mathbb{K}[X])\implies M \times P \in I$$
>
>Une fois que l'on aura ces propriété on en déduira $R \in I$, or $\deg D$ est minimal dans $I \ \backslash \cases{0}$ donc $R=0$ car $\deg R < deg D$
>
>- <u>$I$ sous-groupe</u>
>
>On a $0 \in I$ car $0= \sum^{n}_{i=1}A_i \times 0$
>
>Ensuite soit $P,Q \in I$ : Montrons $P-Q \in I$
>$$\begin{align}
>P \in I \ \text{donc il s'écrit} \ P=\sum^{n}_{i=1}A_i \times U_i \\
>Q \in I \ \text{donc il s'écrit} \ Q=\sum^{n}_{i=1}A_i \times \overset{\textasciitilde}{U_i}
>\end{align}$$
>Donc 
>$$
>P-Q = \sum^{n}_{i=1}A_i(U_i- \overset{\textasciitilde}{U_i}) \in I
>$$
>
>- <u>$I$ absorbant pour $X$</u>
>
>Soit $M= \sum^{n}_{i=1}A_iU_i \in I$ et $P \in \mathbb{K}[X]$. On a :
>$$M \times P = \sum^{n}_{i=1} A_i(U_i \times P) \in I$$
>
>D'où le resultats




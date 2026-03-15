
>[!question] Théorème 26 (Associativité du produit). 
>Soient $n, p, q, r ∈ \mathbb{N}^*, A ∈ \mathcal{M}_{n,p} (\mathbb{K}),\ B ∈ \mathcal{M}_{p,q} (\mathbb{K})$ et $C ∈ \mathcal{M}_{q,r} (\mathbb{K})$. Alors : 
>
>$$A × (B × C) = (A × B) × C$$


>[!tip]+ Démonstration 
>
>$B \in \mathcal{M}_{p,q}(\mathbb{K})$ et $C \in \mathcal{M}_{p,r}(\mathbb{K})$ donc $B \times C \in \mathcal{M}_{p,r}(\mathbb{K})$
>Ensuite $A ∈ \mathcal{M}_{n,p} (\mathbb{K})$ donc $A \times (B \times C)\in \mathcal{M}_{n,r}(\mathbb{K})$
>En effet ces matrices ont la même taille : $A ∈ \mathcal{M}_{n,p} (\mathbb{K})$ et $B ∈ \mathcal{M}_{p,q} (\mathbb{K})$ donc $A \times B \in \mathcal{M}_{n,q}(\mathbb{K})$, puis $C ∈ \mathcal{M}_{q,r} (\mathbb{K})$ donc $(A \times B) \times C \in \mathcal{M}_{n,r}(\mathbb{K})$
>
>Soit $(i,j)\in[\![1,n]\!] \times [\![1,q]\!]$ : On a :
>$$\begin{align} 
>[A \times (B \times C)]_{i,j}&= \sum^{p}_{k=1}[A]_{i,k} \times [B \times C]_{k,j} \\
>&=\sum^{p}_{k=1}[A]_{i,k} \times \sum^{q}_{l=1}[B]_{k,l} \times [C]_{l,j} \\
>&=\sum^{p}_{k=1}\sum^{q}_{l=1}[A]_{i,k} \times [B]_{k,l} \times [C]_{l,j} \\
>&=
>\end{align}$$

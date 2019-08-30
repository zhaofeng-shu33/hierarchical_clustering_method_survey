## Maximizing the mutual information between samples and cluster labels

Abbreviated as MIC. Do not use KL-divergence because of computational difficulty.

Suppose there are $N$ samples and $n$ clusters.
$$
MI(C,x) = \sum_{p=1}^n\sum_{X} (P(C_p,x) - P(C_p)P(x))^2
$$
Estimating $P(C_p)​$ from sample distribution directly. 

Use Mixture Gaussian model to describe $P(x), P((C_p,x))​$. 
$$
\begin{align*}
P(x) &= \frac{1}{N} \sum_{i=1}^N G(x-x_i, \sigma^2) \\
P(C_p, x) &= \frac{1}{N} \sum_{k=1}^{N_p} G(x-x_{p,k}, \sigma^2)
\end{align*}
$$
Use agglomerative hierarchical clustering to increase $MI(C,x)$ in each step. [ICIP 2007]

That is, to compute $\Delta MI(C,x)$ when two clusters $C_a, C_b$ are merged to $C_p$.

Ours: Minimizing the multivariate mutual information between different clusters.

## Bayesian Hierarchical Clustering

Abbreviated as BHC.

Use Bayesian posterior probability to determine which two clusters to merge in the framework of agglomerative clustering.

Suppose there are $D_1, \dots, D_r ​$ clusters, each cluster consists of several points $D_k = \{x_{k_1},\dots x_{k_r}\}​$

For any two clusters $D_i, D_j$, we can compute the posterior probability to merge them. Let $H^{k}_1$ be the prior probability that $D_i, D_j$

should be merged: $D_k = D_i \cup D_j$. $H_2^{k}$ is the counterpart. Let $\alpha_k = \Pr(H_1^{k})$. Then 

$$
r_k = \Pr(H_1^k | D_k) = \frac{\alpha_k \Pr(D_k | H_1^k)}{\alpha_k \Pr(D_k | H_1^k) + (1-\alpha_k)\Pr(D_k | H_2^k)}
$$


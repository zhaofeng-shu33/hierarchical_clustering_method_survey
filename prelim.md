## Conjugate Bayesian analysis for the Gaussian distribution

Suppose the data conforms the univariate Gaussian distribution. If the variance $\sigma^2$ is known ( a given constant) but the mean $\mu$ is unknown, which is the quantity to be estimated. In Bayesian inference, the mean is a random variable. To do Bayesian inference, we need to choose a prior. Using conjugate prior makes the problem simpler because the posterior can be written in close form and we do not need to do (numerical) calculus. 

For the known variance case, if we choose the prior as Gaussian distribution $N(\mu_0, \sigma_0)$, which is the distribution of $\mu$. Then the posterior is also Gaussian with mean 
$$
\begin{align}
\mu_n & = \frac{\sigma^2 \mu_0 + n \sigma_0^2 \bar{x}}{n\sigma_0^2 + \sigma^2} \\
\sigma_n^2 &= \frac{\sigma^2 \sigma_0^2}{n \sigma_0^2 + \sigma^2}
\end{align}
$$

## EM GMM

In Expectation Maximization for Gaussian Mixture Model, we further assume there are $n$ hidden random variables $Z_i$. $X_i | Z_i \sim N(\mu_i, \Sigma_i)$ and each $Z_i$ is multinomial distributed  with parameter ($\pi_1, \dots, \pi_K$). for each data point $x_i$, the probability it belongs to $k$ cluster is $P(Z_i = k | X_i = x_i)$ which can be computed by Bayesian posterior law. This is E Step task. For M Step, we should update the old hyper-parameter $\theta = \cup_{i=1}^K\{\pi_i, \mu_i, \Sigma_i\}$ by maximization the expectation of log likelihood:
$$
\int \log p(x,z | \theta) p(z | x, \theta_{\textrm{old}}) dz
$$
This maximization problem has close form solution. Therefore we can update $\theta$ from $\theta_{\textrm{old}}$ , $P(Z_i = k | X_i = x_i)$ and observation $x$. 

## Variational Inference for Dirichlet process mixtures

### Finite Case

![graphical model](./graphical_model.png)

Like EM GMM, we assume a pre-determined number of cluster $K$.  And we have a bunch of hyper-parameters  $\alpha, \beta, m, W, v $.  $\alpha$ is the parameter of the Dirichlet prior. For $\beta, m, W, v$, these four are parameters of Normal-Inverse Wishart prior $p(\mu, \Sigma) = N(\mu | m, \beta^{-1} \Sigma)W(\Sigma^{-1}| W, v)$. We assume $X_i | Z_i \sim N(\mu_i, \Sigma_i)$ as EM GMM. But $(\mu_i, \Sigma_i)$ are random vectors sampled from Normal-Inverse Wishart distribution. Also $Z_i$ is a multinomial distributed random variable but its parameter $\pi = (\pi_1, \dots, \pi_K)$ is a random vector sampled from symmetric Dirichlet distribution with parameter $\alpha_0$.  What we should do is the same as above, in E step, we estimate $P(Z_i = k | X_i = x_i)$ from old hyper-parameters. In M step, we update the hyper-parameters.  The theory behind these update rules are variational inference, which is different from non-Bayesian EM foundation.

Notice that in later update the Dirichlet distribution is not symmetric any more and we use $D(\alpha_1, \dots, \alpha_K)$ to represent the updated parameter. To make notation concise we use $r_{ik} = P(Z_i=k | X_i = x_i)$. The M step parameter update rule is:
$$
\alpha_k = \sum_{i=1}^n r_{ik} + \alpha_0
$$

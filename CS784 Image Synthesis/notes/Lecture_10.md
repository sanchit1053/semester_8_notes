# lecture 10 <div style="text-align"> 09/02/2024 </div>

## Estimator efficiency

Efficience of the estimator is defined as 
$$\epsilon[F_N] = \frac{1}{V[F_N]T[F_n]}$$

Here $V[F_N]$ is variance and $T[F_N]$ is time required to compute its value

Noise decrease slowly with number of samples

$$
\begin{align}
\int_\Omega f(x)dx =& \frac{1}{N}\sum_{i = 1}^NY_i \\
Y_i =& \frac{f(x_i)}{p(x_i)} 
\end{align}
$$


## Importance sampling
- Given the MC estimator $F_N = \frac{1}{N}\sum_{i=1}^N\frac{f(x_i)}{p(x_i)}$
- if we know $c =\frac{1}{\int f(x) dx}$
- then $\frac{f(x_i)}{p(x_i)} = \frac{1}{c} = \int f(x)d(x)$
- choose p(x_i) over 
- read montecarlo reference on webpage A.5

## Sampling efficiency

### Russian Roulette
- The interfrand is not evaluated for a particular sample with some probability q and a constant value c is used
- Integrand is evaluated with probability $1-q$ and weighteed by $1/1-q$
- $$F' =\large{\{}\begin{matrix}\frac{F-qc}{1-q} & \text{ if } \zeta > q \\ c & otherwise \end{matrix}$$
- Expected value $E[F'] = (1 - q)\frac{E[F]-qc}{1-q} + qc$

## Method of rejection
- If we want to sample some $f(x)$
- But instead can sample from some PDF $p(x) : f(x) < cp(x)$
- Sample X from p(x)
- if for some $\zeta$, $\zeta < f(X) / (cp(x))$ then return X else resample
- eg: to sample from a disk, sample from a bounding square if $x^2 + y^2 < r^2$ then allow else reject

# lecture 9 <div style="text-align"> 06/02/2024 </div>


## Monte carlo simulation
- See Slides

$$
\begin{align*}
    E[F_n] &= E[\frac{b - a}{N}\sum_{i=1}^{N}f(x_i)] \\
     &= \frac{b - a}{N}\sum_{i=1}^{N}E[f(x_i)] \\
     &= \frac{b - a}{N}\sum_{i=1}^{N}\int_a^bf(x_i)p(x_i)dx \\
     &= \frac{1}{N}\sum_{i=1}^{N}\int_a^bf(x)dx \\
     &= \int_a^bf(x_1)dx \\
\end{align*}
$$


- monte carlo never gives the same image twice, that is if we analyse pixel by pixel there always will be some diff

#### Las Vegas simulation
- Randomized algorithms that always give the same result

## Bias estimator
- Faster

## Efficiency

# Variational Inference
***
Main idea: use a prior distribution that is not so complicated like p(x) to approximate p(x). Using KL divergence to measure the difference between p(x) and q(x).
#### Kullback Leibler divergence
KL divergence is used to measure the distance or dis-similarity of two distribution.  
$$
KL(q(x)|p(x))=\int\log(\frac{q(x)}{p(x)})q(x)dx=\big\langle\log(q)\big\rangle_q-\big\langle \log(p)\big\rangle_q\ge0
$$
  
****
#####For the normalisation constant $$p(x)=\frac{1}{Z}e^{\phi(x)}$$
$$
KL(q(x)|p(x))=\big\langle\log(q)\big\rangle_q-\big\langle \log(p)\big\rangle_q=\big\langle\log(q)\big\rangle_q-\big\langle\phi(x)\big\rangle_q+\log(Z)
$$
Then,
$$
\log(Z)\ge-\big\langle\log(q)\big\rangle_q+\big\langle\phi(x)\big\rangle_q
$$
The first part in the above equation is the entropy of $$q(\theta)$$, which will increase as the $$\sigma(\theta)$$ increase.

#####For the marginal likelihood $$p(D|M)=\int_\theta p(D|\theta,M)p(\theta|M)$$

$$
p(\theta|D,M)=\frac{p(D|\theta,M)p(\theta|M)}{p(D|M)}
$$

Use KL,
$$
\begin{aligned}
KL(q(x)|p(\theta|D,M))&=\big\langle\log(q)\big\rangle_q-\big\langle \log(p(\theta|D,M))\big\rangle_q\\ 
&=\big\langle\log(q)\big\rangle_q-\big\langle \log p(D|\theta,M)p(\theta|M)\big\rangle_q+\log(p(D|M))
\end{aligned}
$$
Similarly, we have,
$$
\begin{aligned}
\log(p(D|M))&\ge-\big\langle\log(q)\big\rangle_q + \big\langle \log p(D|\theta,M)\big\rangle_q + \big\langle \log p(\theta|M)\big\rangle_q\\
&=\big\langle \log p(D|\theta,M)\big\rangle_q - KL(q|p(\theta|M))
\end{aligned}
$$

For this equation, we have a upper bound $$\log(p(D|M))$$, and a lower bound $$\big\langle\log p(D|\theta,M)\big\rangle_q$$.  
Then if we increase this lower bound, we can meanwhile minimize $$KL(q(\theta)|p(\theta|M))$$. When it is equal, the KL divergence achive to 0, which means $$q(\theta)$$ is equal to $$p(\theta|M)$$ now.
****

####General mean-field equations
Consider a factorised approximation $$q(x)=\Pi_i q(x_i)$$  
****
This how we can use a simpiler distribution to approximate a complicated distribtion. We assume the parameters are independent, than track these parameter separately.
****
$$
KL(q|p)=\sum_i\big\langle\log q(x_i)\big\rangle_{q(x_i)} - \big\langle \log p(x)\big\rangle_{\Pi_i q(x_i)}
$$
$$p(x_i)$$ is the marginal probability  
For $$x_i$$ we have,
$$
\big\langle \log q(x_i)\big\rangle_{q(x_i)} - \big\langle\big\langle\log(p(x_j))\big\rangle_{\Pi_i\neq j q(x_j)}\big\rangle_{q(x_i)}
$$
To get the optimal $$q(x_i)$$, we need to let
$$
q(x_i)\propto exp(\big\langle\log p(x)\big\rangle_{\Pi_{i\neq j q(x_j)}})
$$
So every variable, we update it in this way:
$$
q(x_i)=\frac{1}{Z}exp(\big\langle\log p(x)\big\rangle_{\Pi_{i\neq j q(x_j)^old}})
$$



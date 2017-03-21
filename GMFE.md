##General mean-field equations
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

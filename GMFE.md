#General mean-field equations
The main idea of General mean-field is the facorise the joint probabilty of q, and compute them one by one instead compute the at one time.
***
For the equation from the last part.
$$
\log p(x)=\mathbb{E}_{q(z)}\Big[\log\frac{p(z,x)}{q(z)}\Big]-KL(q(z)|p(z|x))
$$
Define
$$
\mathcal{L}=\mathbb{E}_{q(z)}\Big[\log\frac{p(z,x)}{q(z)}\Big]
$$
The target here is to maximize the $$\mathcal{L}$$(ELOB).
Now let $$z$$ be a vector, then $$q(\bar{z})$$ becomes a joint probabilty and it maybe very hard to compute.  
So instead, we assume each $$z_i$$ is independent to each other and consider a factorised approximation $$q(\bar z)=\Pi_i q(z_i)$$  
Now,
$$
\begin{aligned}
\mathcal{L} &=\mathbb{E}_{q(\bar z)}[\log p(\bar z,x)-\log q(\bar z)]\\
            &=\int_{z_1}...\int_{z_n}\prod_i^n q(z_i) [\log p(z,x)-\sum_i^n\log q(z_i)]
\end{aligned}
$$
But still, the $$argmax_{\bar z}\mathcal{L}$$ is very hard to compute.  
So, instead of computing them at once, we compute them one by one and treat others as constants.
Let's considering $$z_i$$ now, rewrite the $$\mathcal{L}$$ as
$$
\begin{aligned}
\mathcal{L} &=\int_{z_1}q(z_i) \Big(\int...\int\prod_{j\neq i} q(z_j) \big(\log p(\bar z,x)-\sum_{j=1}^n\log q(z_j)\big)\prod_{j\neq i} dx_j\Big)dx_i\\
            &=\int_{z_1}q(z_i) \Big(\mathbb{E}_{q z_{j\neq i}}[\log p(\bar z,x)]-\mathbb{E}_{q(z_{j\neq i})}[\log q(z_i)]-\mathbb{E}_{q(z_{j\neq i})}\Big[\sum_{j\neq i}^n\log q(z_j)\Big]\Big)dx_i\\
            &=\int_{z_1}q(z_i) \Big(\mathbb{E}_{q(z_{j\neq i})}[\log p(\bar z,x)]-\log q(z_i)\Big)dx_i+C
\end{aligned}
$$
Here we separate the constant C into $$C_1,C_2$$, such that $$E_{z_{j\neq i}}[\frac{\log p(\bar z,x)}{C_1}]=\log\tilde{p}(x,z)$$, and $$\tilde{p}(x,z)$$ will be a distribution.\\
Plug this into the equation,
$$
\begin{aligned}
\mathcal{L} &=\int_{z_1}q(z_i) \Big(\mathbb{E}_{q(z_{j\neq i})}[\log p(\bar z,x)]-\log q(z_i)\Big)dx_i+C_2\\
            &=\int_{z_1}q(z_i)\Big( \log \tilde{p}(\bar z,x)-\log q(z_i)\Big)dx_i+C_2\\
            &=\int_{z_1}q(z_i)\log \frac{\tilde{p}(\bar z,x)}{q(z_i)}dx_i+C_2\\
            &=-KL(q(z_i)|\tilde{p}(x,z))+C_2
\end{aligned}
$$
Now, in order to maximize $$\mathcal{L}$$, we need to minimize $$KL(q(z_i)|\tilde{p}(x,z))$$, which achive to its minimum when 
$$
q(z_i)=\tilde{p}(x,z)=\frac1Z\exp(\mathbb{E}_{q_{j\neq i}}[\log p(x,z)])
$$  
Apply this on every z_i, and each time we use newly updated q(z_j).  
There is a proof of that by doing this, $$\mathcal{L}$$ is guarantee to increase in each iteration.

<!---
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
--->

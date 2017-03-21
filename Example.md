#Example
***
#### Joint Posterior
We need to approximate a posterior $$p(\bar{z}|x)$$, and $$\bar{z}=[z_1,z_2,z_3]$$, by using $$q(\bar z)=q(z_1)q(z_2)q(z_3)$$ to approximate this posterior.  
  
Write down the KL divergence,
$$
KL(q(\bar z)|p(\bar z|x)) =\int_{\bar z}q(\bar z)\log\frac{q(\bar z)}{p(\bar z|x)}dz
$$
According to the last section, the ELBO function is
$$
\begin{aligned}
\mathcal{L} &=\mathbb{E}_{\bar z}[\log p(\bar z,x)]-\mathbb{E}_{\bar z}[\log q(\bar z)]\\
            &=\mathbb{E}_{\bar z}[\log p(z_1,z_2,z_3,x)]-\log q(z_1)-\log q(z_2)-\log q(z_3)]\\
\end{aligned}
$$
For $$z_1$$,
$$
\begin{aligned}
\mathcal{L} &=\mathbb{E}_{z_1}\Big[\mathbb{E}_{z_2,z_3}[\log p(z_1,z_2,z_3,x)]-\log q(z_1)-\log q(z_2)-\log q(z_3)]\Big]\\
            &=\mathbb{E}_{z_1}\Big[\mathbb{E}_{z_2,z_3}[\log p(z_1,z_2,z_3,x)]-\mathbb{E}_{z_2,z_3}[\log q(z_2)q(z_3)]-\log q(z_1)\Big]\\
            &=\mathbb{E}_{z_1}\Big[\mathbb{E}_{z_2,z_3}[p(z_1,z_2,z_3,x)]-\log q(z_1)\Big]+C\\
            &=\mathbb{E}_{z_1}\Big[\log\tilde{p}(z_1,z_2,z_3,x)-\log q(z_1)\Big]+C_2\\
            &=\mathbb{E}_{z_1}\Big[\log\frac{\tilde{p}(z_1,z_2,z_3,x)}{q(z_1)}\Big]+C_2\\
            &=-KL(q(z_1)|\tilde{p(z_1,z_2,z_3,x)})+C_2\\
\end{aligned}
$$
Thus, for $$z_1$$ and similarly for $$z_2,z_3$$
$$
\begin{aligned}
p(z_1)&=\frac1Ze^{\mathbb{E}_{z_2,z_3}[\log p(z_1,z_2,z_3,x)]}\\
\\
p(z_2)&=\frac1Ze^{\mathbb{E}_{z_1,z_3}[\log p(z_1,z_2,z_3,x)]}\\
\\
p(z_3)&=\frac1Ze^{\mathbb{E}_{z_1,z_2}[\log p(z_1,z_2,z_3,x)]}
\end{aligned}
$$
***
#### Multivariable Gaussian Distribution

***
#### Gaussian Mixture Model

***
#### Posterior of parameters

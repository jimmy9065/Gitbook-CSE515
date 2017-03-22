#Example
***
#### Joint Posterior
We need to approximate a posterior $$p(\bar{z}|x)$$, and $$\bar{z}=[z_1,z_2,z_3]$$, by using $$q(\bar z)=q(z_1)q(z_2)q(z_3)$$.  
  
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
Given a multivariable gaussian distribution $$p(\bar x=[x_1,x_2])=\mathcal{N}(\bar x;\bar \mu,\Sigma)$$, in which, $$\mu=[1,-1],\Sigma=[2,-0.2;-0.2,1]$$ and define $$\Lambda=\Sigma^{-1}$$.  
For $$x_1$$ 
$$
\begin{aligned}
\log q(x_1)&=\mathbb{E_{2}}
\Big[
-\frac12
(\begin{array}{c}
x_1-\mu_{1}\\
x_2-\mu_{2}
\end{array})
(\begin{array}{c c}
\Lambda_{11}&\Lambda_{12}\\
\Lambda_{21}&\Lambda_{22}
\end{array})
(\begin{array}{c}
x_1-\mu_{1}\\
x_2-\mu_{2}
\end{array})
\Big]+C\\
      &=-\frac12\mathbb{E_{2}}
\Big[
(x_1-\mu_1)^2\Lambda_{11}+
2(x_1-\mu_1)(x_2-\mu_2)\Lambda_{12}+
(x_2-\mu_2)^2\Lambda_{22}
\Big]+C\\
      &=-\frac1 2 \Lambda_{11}\mathbb{E_{2}}
\Big[
(x_1-\mu_1)^2+
2(x_1-\mu_1)(x_2-\mu_2) \frac{\Lambda_{12}}{\Lambda_{11}}+C
\Big]+C\\
      &=-\frac1 2 \Lambda_{11}
\Big(
x_1^2-2x_1\mu_1+\mu_1^2+
\frac{2\mathbb{E_{2}[x_{2}]}{\Lambda_{22}}}{\Lambda_{11}}x_1-
\frac{2\mu_{2}\Lambda_{22}}{\Lambda_{11}}x_1
\Big)+C\\
      &=-\frac1 2 \Lambda_{11}
\Big(
x_1^2-
2x_1(\mu_1-
\frac{\Lambda_{22}}{\Lambda_{11}}(\mathbb{E_{2}[x_{2}]}-\mu_{2})
)+C
\Big)+C\\
      &=-\frac1 2 \Lambda_{11}
\Big(
x_1-
(\mu_1-
\frac{\Lambda_{22}}{\Lambda_{11}}(\mathbb{E_{2}[x_{2}]}-\mu_{2})
)
\Big)^2+C
\end{aligned}
$$
Thus we update $$q(x_1)$$
$$
\begin{aligned}
q(x_1)&=\frac1Zexp(
-\frac 
{\Big(
x_1-
(\mu_1-\frac{\Lambda_{22}}{\Lambda_{11}}(\mathbb{E_{2}[x_{2}]}-\mu_{2})
)\Big)}
{2\Lambda_{11}^{-1}})\\
      &=\mathcal{N}(x_1,(\mu_1-\frac{\Lambda_{22}}{\Lambda_{11}}(\mathbb{E_{2}[x_{2}]}-\mu_{2})),\Lambda_{12}^{-1})
\end{aligned}
$$
Since $$x_2$$ is symmetric, we can derive it similarly
$$
q(x_2)=\mathcal{N}(x_2,(\mu_2-\frac{\Lambda_{11}}{\Lambda_{22}}(\mathbb{E_{1}[x_{1}]}-\mu_{1})),\Lambda_{12}^{-1})
$$
Initialize $$x_1=3,x_2=4$$, after 4 iterations, we have  

| Times | x1 | x2 |
|--|--|--|
|0 |3 |4 |
|1 |0 |-0.9|
|2 |0.98|-0.998|
|3 |0.996|-1.0|
|4 |0.1|-1.0|

And here is the plot
<img src=https://raw.githubusercontent.com/jimmy9065/Gitbook-CSE515/master/pic/mvn_approx.jpg width = 800 height = 400 />  
Notice only the mean and the $$\sigma(x_1)$$,$$\sigma(x_2)$$ are matched.  
This is because we assumed that $$x_1,x_2$$ are independent.
***
#### Gaussian Mixture Model

***
#### Posterior of parameters

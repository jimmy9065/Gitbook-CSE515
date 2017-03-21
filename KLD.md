#Kullback Leibler divergence
***
###Definition:
$$
KL(q(x)|p(x))=\int\log(\frac{q(x)}{p(x)})q(x)dx=\big\langle\log(q)\big\rangle_q-\big\langle \log(p)\big\rangle_q\ge0
$$
&ensp;KL divergence is used to measure the distance or dis-similarity of two distribution. if $$p(x)==q(x)$$, it will be 0.

###Application:
* #####Approximation of a prior 
Assume,
$$
p(x)=\frac{1}{Z}e^{\phi(x)}
$$
Use q(x) to approximate p(x), using KL divergence
$$
KL(q(x)|p(x))=\big\langle\log(q)\big\rangle_q-\big\langle \log(p)\big\rangle_q=\big\langle\log(q)\big\rangle_q-\big\langle\phi(x)\big\rangle_q+\log(Z)
$$
Rearrange the equation, we have
$$
\log(Z)\ge-\big\langle\log(q)\big\rangle_q+\big\langle\phi(x)\big\rangle_q
$$
The first part in the equation is the entropy of $$q(\theta)$$, which increase as the $$\sigma(\theta)$$ increase.
***
* #####Approximation of a posterior
Given a posterior $$p(z|x)$$, apply Bayes' rule,
$$
p(z|x)=\frac{p(z.x)}{\int_{z}p(z,x)}=\frac{p(z|x)}{p(x)}
$$
Use $$q(z)$$ to approximate $$p(z|x)$$, and apply KL divergence
$$
\begin{aligned}
KL(q(z)|p(z|x)) &=\int_{z}q(z)\log\frac{\frac{p(z,x)}{p(x)}}{q(z)}dz\\
                &=\int_{z}q(z)\log{p(z,x)}dz-\int_{z}q(z)\log{q(z)}dz-\log p(x)\\
                &=\mathbb{E}_{q(z)}[\log{p(z,x)}]-\mathbb{E}_{q(z)}[\log{q(z)}]-\log p(x)\\
\end{aligned}
$$
Rearrange the equation,
$$
\begin{aligned}
\log p(x) &=\mathbb{E}_{q(z)}[\log{p(z,x)}]-\mathbb{E}_{q(z)}[\log{q(z)}]-KL(q(z)|p(z|x))\\
          &=\mathbb{E}_{q(z)}\Big[\log\frac{p(z,x)}{q(z)}\Big]-KL(q(z)|p(z|x))\\
\end{aligned}
$$
The first part on the right is called evidence lower bound(ELOB).  
Notice $$p(x)$$ is a constant to z, and KL divergence is non-negative. so the ELOB is the lower bound of $$p(x)$$.  
Thus we can minimize the KL divergence by maxmizing the ELBO. And this is what variational infernce do.

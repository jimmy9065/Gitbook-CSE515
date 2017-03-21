#Example
We need to calculate a posterior $$p(\bar{z}|x)$$, Note $$\bar{z}$$ is a vector here.  
Firstly, we know 
$$
p(\bar{z}|x)=\frac{p(z.x)}{\int_{\bar{z}}p(\bar{z},x)}=\frac{p(\bar z|x)}{p(x)}
$$
But sometimes $$\int_{\bar z}(\bar z,x)$$ is very hard to integral. So instead, we use a simpler distribution $$q(\bar z)$$ to approximate $$p(\bar z|x)$$.  
By KL divergence, we have
$$
KL(q(\bar z)|p(\bar z|x))=\int_{\bar z}q(\bar z)\log\frac{p(\bar z|x)}{q(\bar z)}
$$


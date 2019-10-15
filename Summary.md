### [Support Vector Machines with a Reject Option](https://arxiv.org/pdf/1201.1140.pdf) 
<p align="right"> Oct. 12, 2019 </p>



### [Multicategory Support Vector Machines](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.129.3020&rep=rep1&type=pdf) 
<p align="right"> Oct. 13, 2019 </p>

Two general strategies are used to tacke multicategory classification problems with SVMS: 1) Construct pairwise (1-versus-1) binary SVMs. So there are ${C_k^2}=k(k-1)/2$ binary SVMs. However, this approach will potentially increase the variance since it use less observations in each SVM. Moreover, the total number of binary classifiers gets more and more with increasing $k$. 2) Combing the rest classes as another a new class and then constrcut binary SVMs, where there are $k$ binary SVMs. If there is no dominate class ($P(Y=j|X=x)<\frac{1}{2}$ for all $j=1, 2, \cdots, k$), then the output will obscure since $f_j(x)$ are close to $-1$ for all $j=1, 2, \cdots, k$. So this paper construct MSVM to treating all the class simutaneously, which means for each observation the outpout is a vector $\mathbf{f}(\mathbf{x})=(f_1(\mathbf{x}), f_2(\mathbf{x}), \cdots, f_k(\mathbf{x}))$  

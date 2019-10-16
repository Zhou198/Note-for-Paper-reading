### [Support Vector Machines with a Reject Option](https://arxiv.org/pdf/1201.1140.pdf) 
<p align="right"> Oct. 12, 2019 </p>



### [Multicategory Support Vector Machines](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.129.3020&rep=rep1&type=pdf) 
<p align="right"> Oct. 13, 2019 </p>

Two general strategies are used to tacke multicategory classification problems with SVMS: 1) Construct pairwise (1-versus-1) binary SVMs. So there are ${C_k^2}=k(k-1)/2$ binary SVMs. However, this approach will potentially increase the variance since it use less observations in each SVM. Moreover, the total number of binary classifiers gets more and more with increasing $k$. 2) Combing the rest classes as another a new class and then constrcut binary SVMs, where there are $k$ binary SVMs. If there is no dominate class ($P(Y=j|X=x)<\frac{1}{2}$ for all $j=1, 2, \cdots, k$), then the output will obscure since $f_j(x)$ are close to $-1$ for all $j=1, 2, \cdots, k$. So this paper constructs the MSVM to treating all the class simutaneously, which means for each observation the outpout is a vector $\mathbf{f}(\mathbf{x})=(f_1(\mathbf{x}), f_2(\mathbf{x}), \cdots, f_k(\mathbf{x}))$ with the sum-to-0 constraint. This method can also target bayes rule in the same fashion in binary SVMs.

$$\min \frac{1}{n}\sum\limits_{i=1}^n \mathbf{L}(\mathbf{y_i}) \cdot(\mathbf{f}{(\mathbf{x_i})-\mathbf{y_i})\_{+}}+\frac{1}{2}\lambda\sum\limits_{j=1}^k\left\|\|h_j\|\right\|^2_{H_k}$$ 



This appraoch unifies both standard cases and unstandard cases. In standard cases, cost $c_{ij}$ of classfying label $i$ as $j$ are same for each $j=1, 2, \cdots, k$ and $j\neq i$, of course $c_{ii}=0$. Moreover, there is no bias in sampling, which means porpotion of each class in training data is same to that in whole data. In unstandard cases, $c_{ij}$ differs in $j$'s, and maybe there are biases in sampling. Whatever, the MSVM approach can present the unified form covering above cases in loss fucntiones.

Implenting SVMs or MSVM in an asymetotically efficient manner is dependent on choosing $\lambda$ for penalty. In this paper, it compares results of choosing $\lambda$ based on different criterions: 1) 10-folds crossvalidation, where it chooses $\lambda$ with minimum misclassification; 2) Generalized approximate crossvalidation (GACV), where it chooses optimal $lambda$ with minimum objective function (loss + penalty) not misclassification; 3) GCKL, where it choose optimal $\lambda$ only with minimum loss. In one numerical study, 10-folds crossvalidation and GCKL peformance better than GACV and are close to bayes rule.

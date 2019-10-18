### [Support Vector Machines with a Reject Option](https://arxiv.org/pdf/1201.1140.pdf) 
<p align="right"> Oct. 12, 2019 </p>



### [Multicategory Support Vector Machines](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.129.3020&rep=rep1&type=pdf) 
<p align="right"> Oct. 15, 2019 </p>

Two general strategies are used to tacke multicategory classification problems with SVMS: 1) Construct pairwise binary SVMs (1-versus-1). So there are ${C_k^2}=k(k-1)/2$ binary SVMs. However, this approach will potentially increase the variance since it use less observations in each SVM. Moreover, the total number of binary classifiers gets more and more with increasing $k$. 2) Combing the rest classes as another a new class and then constrcut binary SVMs (1-versus-rest), where there are $k$ binary SVMs. If there is no dominate class ($P(Y=j|X=x)<\frac{1}{2}$ for all $j=1, 2, \cdots, k$), then the output will obscure since $f_j(x)$ are close to $-1$ for all $j=1, 2, \cdots, k$. So this paper constructs the MSVM to treating all the class simutaneously, which means for each observation the outpout is a vector $\mathbf{f}(\mathbf{x})=(f_1(\mathbf{x}), f_2(\mathbf{x}), \cdots, f_k(\mathbf{x}))$ with the sum-to-0 constraint. This method can also target bayes rule in the same fashion in binary SVMs.

Our goal is to
$$\min \frac{1}{n}\sum\limits_{i=1}^n \mathbf{L}(\mathbf{y_i}) \cdot(\mathbf{f}{(\mathbf{x_i})-\mathbf{y_i})\_{+}}+\frac{1}{2}\lambda\sum\limits_{j=1}^k\left\|\|h_j\|\right\|^2_{H_k},$$ 
where $f_j(\mathbf{x_i})=h_j(\mathbf{x_i})+b_j$ and $\mathbf{L}(\mathbf{y_i})$ is a cost vector with each entrie a cost of classfying $y_i$ as label $j$'s. Note, $\mathbf{y_i}$ is a code vector, where $j$-th entry is $+1$ and remining are $-\frac{1}{k-1}$ if this observation $\mathbf{x_i}$ is labeled as class $j$. This implies $\sum\limits_{j=1}^k y_{ij}=0$.

This appraoch unifies both standard cases and unstandard cases. In standard cases, cost $c_{ij}$ of classfying label $i$ as $j$ are same for each $j=1, 2, \cdots, k$ and $j\neq i$, of course $c_{ii}=0$. Moreover, there is no bias in sampling, which means porpotion of each class in training data is same to that in whole data. In unstandard cases, $c_{ij}$ differs in $j$'s, and maybe there are biases in sampling. Whatever, the MSVM approach can present the unified form covering above cases in loss fucntiones.

Implenting SVMs or MSVM in an asymetotically efficient manner is dependent on choosing $\lambda$ for penalty. In this paper, it compares results of choosing $\lambda$ based on different criterions: 1) 10-folds crossvalidation, where it chooses $\lambda$ with minimum misclassification; 2) Generalized approximate crossvalidation (GACV), where it chooses optimal $\lambda$ with minimum objective function (loss + penalty) not misclassification; 3) GCKL, where it choose optimal $\lambda$ only with minimum loss. In one numerical study, 10-folds crossvalidation and GCKL peformance better than GACV and are close to bayes rule.




### [On Reject and Refine Options in Multicategoory Classification](https://arxiv.org/pdf/1701.02265.pdf) 
<p align="right"> Oct. 17, 2019 </p>

This paper proposed not only multicategory classification problem with reject option (like on binary SVM with reject option) but also with refine option. Assume there are $k$ classes in the dataset, for observations in the reject region, the classfier spits out the whole class set $\{1, 2, \cdots, k\}$. For those in refine regions, it outputs a subset of the whole class set. So, there is no refine option in binary classification cases. Moreover, compared with classification with only reject option, the proposed method has more cautious prediction on the boundries among several classes, rather than just giving a definite result for points adjacent to boundries.

































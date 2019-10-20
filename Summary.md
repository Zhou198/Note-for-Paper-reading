#
### [Support Vector Machines with a Reject Option](https://arxiv.org/pdf/1201.1140.pdf) 
<p align="right"> Oct. 12, 2019 </p>


#
### [Multicategory Support Vector Machines](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.129.3020&rep=rep1&type=pdf) 
<p align="right"> Oct. 15, 2019 </p>

Two general strategies are used to tacke multicategory classification problems with SVMS: 1) Construct pairwise binary SVMs (1-versus-1). So there are $\binom{k}{2}{C_k^2}=k(k-1)/2$ binary SVMs. However, this approach will potentially increase the variance since it use less observations in each SVM. Moreover, the total number of binary classifiers gets more and more with increasing $k$. 2) Combing the rest classes as another a new class and then constrcut binary SVMs (1-versus-rest), where there are $k$ binary SVMs. If there is no dominate class ($P(Y=j|X=x)<\frac{1}{2}$ for all $j=1, 2, \cdots, k$), then the output will obscure since $f_j(x)$ are close to $-1$ for all $j=1, 2, \cdots, k$. So this paper constructs the MSVM to treating all the class simutaneously, which means for each observation the outpout is a vector $\boldsymbol{f}(\mathbf{x})=(f_1(\mathbf{x}), f_2(\mathbf{x}), \cdots, f_k(\mathbf{x}))$ with the sum-to-0 constraint. This method can also target bayes rule in the same fashion in binary SVMs.

Our goal is to
$$\min \frac{1}{n}\sum\limits_{i=1}^n \mathbf{L}(\mathbf{y_i}) \cdot(\boldsymbol{f}{(\mathbf{x_i})-\mathbf{y_i})\_{+}}+\frac{1}{2}\lambda\sum\limits_{j=1}^k\left\|\|h_j\|\right\|^2_{H_k},$$ 
where $f_j(\mathbf{x_i})=h_j(\mathbf{x_i})+b_j$ and $\mathbf{L}(\mathbf{y_i})$ is a cost vector with each entrie a cost of classfying $y_i$ as label $j$'s. Note, $\mathbf{y_i}$ is a code vector, where $j$-th entry is $+1$ and remining are $-\frac{1}{k-1}$ if this observation $\mathbf{x_i}$ is labeled as class $j$. This implies $\sum\limits_{j=1}^k y_{ij}=0$.

This appraoch unifies both standard cases and unstandard cases. In standard cases, cost $c_{ij}$ of classfying label $i$ as $j$ are same for each $j=1, 2, \cdots, k$ and $j\neq i$, of course $c_{ii}=0$. Moreover, there is no bias in sampling, which means porpotion of each class in training data is same to that in whole data. In unstandard cases, $c_{ij}$ differs in $j$'s, and maybe there are biases in sampling. Whatever, the MSVM approach can present the unified form covering above cases in loss fucntiones.

Implenting SVMs or MSVM in an asymetotically efficient manner is dependent on choosing $\lambda$ for penalty. In this paper, it compares results of choosing $\lambda$ based on different criterions: 1) 10-folds crossvalidation, where it chooses $\lambda$ with minimum misclassification; 2) Generalized approximate crossvalidation (GACV), where it chooses optimal $\lambda$ with minimum objective function (loss + penalty) not misclassification; 3) GCKL, where it choose optimal $\lambda$ only with minimum loss. In one numerical study, 10-folds crossvalidation and GCKL peformance better than GACV and are close to bayes rule.



#
### [On Reject and Refine Options in Multicategoory Classification](https://arxiv.org/pdf/1701.02265.pdf) 
<p align="right"> Oct. 17, 2019 </p>

This paper proposed not only multicategory classification problem with reject option (like on binary SVM with reject option) but also with refine option. Assume there are $k$ classes in the dataset, for observations in the reject region, the classfier spits out the whole class set $\\{1, 2, \cdots, k\\}$. For those in refine regions, it outputs a subset of the whole class set. So, there is no refine option in binary classification cases. Moreover, compared with classification with only reject option, the proposed method has more cautious prediction on the boundries among several classes, rather than just giving a definite result for points adjacent to boundries.

Similiar to previous thesis, this approach also considers all classes simultaneously. However, it choose angle-based margin classification framework instead of margin-based ones because the prior is free of sum-to-0 constraint and advantageous in computation performance, especially for high-dimensional data.

Let $\mathcal{Y}=(\mathcal{Y}\_1, \mathcal{Y}\_2, \cdots, \mathcal{Y}\_k)$ be a centered simplex in $\mathbb{R}^{k-1}$, $\mathcal{Y}\_j$ be surrogate coding vector for class $j$ and $\boldsymbol{f}\in\mathbb{R}^{k-1}$ be the classification function. Then our goal is to $$\min\frac{1}{n}\sum\limits_{i=1}^n\sum\limits_{j\neq y_i}\ell\left(\left<\mathcal{Y}\_j, \boldsymbol{f}(x\_i)\right>\right), \text{ subject to } J(\boldsymbol{f})\leq s,$$
where $\ell$ is a monotonically increasing (Remark: in binary SVMs, this is decreasing since the label multiplied with classfication function is true, which is opposite to this setting.) loss function like

$$\ell_{\rm SVM}(\mu)\begin{cases}
  0, & \mbox{if}\ \mu<-1  \\\\
  1+\mu, & \mbox{if}\ -1\leq\mu<0  \\\\
  1+a\mu, & \mbox{otherwise}\\\\
\end{cases}, \qquad \text{or} \qquad 
\ell_{\rm DWD}(\mu)\begin{cases}
  -\frac{1}{4\mu}, & \mbox{if}\ \mu<-0.5  \\\\
  1+\mu, & \mbox{if}\ -0.5\leq\mu<0  \\\\
  1+a\mu, & \mbox{otherwise}\\\\
\end{cases}
$$

and $J(\boldsymbol{f})$ is the $L_2$ or $L_1$ penalty for function space. The induced classifier by $\boldsymbol{\hat f}$ with reject and refine option is defined as, $$\phi\_\boldsymbol{\hat{f}}=\begin{cases}
R \qquad \qquad \qquad \qquad \ \text{ if } \left|\left<\mathcal{Y}\_j, \boldsymbol{\hat f}\right>\right|\leq \delta, \forall j\\\\
\arg\max \left<\mathcal{Y}\_j, \boldsymbol{\hat f}\right> \qquad \text{ if } \left<\mathcal{Y}\_j, \boldsymbol{\hat f}\right> \geq \delta, \text{ for some } j\\\\
\left\\{j: \left|\left<\mathcal{Y}\_j, \boldsymbol{\hat f}\right>\right|\leq \delta \text{ for some but all } j\right\\}
\end{cases}$$

There are 3 tuning parameters we should search for, namely $a, s$ and $\delta$. Here $a$ can be determined as $\frac{d}{1-d}$ by a presetted cost $d$. Parameter $s$ restricts the function space and is searched from a grid of candidates by minimizing the $0$-$d$-$1$ loss (extension to misclassification rate) via validation set or crossvalidation. Note $\delta$ is also obtained to minimize $0$-$d$-$1$ loss only after inducing out a classifier from $\boldsymbol{\hat f}$. Therefore, we can set $\Lambda\times\Delta=\\{\lambda_1, \lambda_2, \cdots, \lambda_r\\}\times\\{\delta_1, \delta_2, \cdots, \delta_t\\} $ at first and then find a specific combindation with minimum $0$-$d$-$1$ loss via tuning procedure.   

Next part refers to convergence of the excess $\ell$-$$ risk in linear learning, which is define as $$e\left(\boldsymbol{f}, \boldsymbol{f}^{(p, k)}\right)=\mathbb{E}\left[\sum\limits_{j\neq Y}\ell\left\\{\left<\boldsymbol{f}(\boldsymbol{X}), \mathcal{Y}\_j\right>\right\\}\right]-\mathbb{E}\left[\sum\limits_{j\neq Y}\ell\left\\{\left<\boldsymbol{f}^{(p, k)}(\boldsymbol{X}), \mathcal{Y}\_j\right>\right\\}\right],$$ where $\boldsymbol{f}$ is any function restricted by $s$ and $\boldsymbol{f}^{(p, k)}$ is a minimizer (only to loss, here namely $\ell$-$$loss) with no restriction (which means $s\rightarrow\infty$). If $k$ is bounded and true classification signals are sparse, then we can choose a large $s$ such that approximate error in $e\left(\boldsymbol{\hat f}, \boldsymbol{f}^{(p, k)}\right)$ is $0$, then for $L_1$ penalty, $e\left(\boldsymbol{\hat f}, \boldsymbol{f}^{(p, k)}\right)=O\left(r\log(r^{-1})\right)$ (simlilar to $L_2$ penalty), almost surely under $\mathbb{P}$. If $k\rightarrow\infty$ as $n\rightarrow\infty$ and assume the signals for classification on subcollections of the whole class set are finite, then, under $L_1$ penalty, we can choose $s=O(k)$ such that approximation error is $0$ and $e\left(\boldsymbol{\hat f}, \boldsymbol{f}^{(p, k)}\right)=O\left(k^2r\log(r^{-1})\right)$, almost surely under $\mathbb{P}$.

In numerical studies, compared with regular classier (outputs definite label for each obseravtion) and classifier with only reject option, the classifier with reject and refine option performs quite well by introducing reject and refine regions. Note there is no misclassification in reject rejoin and we report the mis-refinement rate in refine regions, which is defined as the porpotion of observations whose true labels are not in the refine sets.

In conclusion, when the cost for misclassification is too high to bear, it may be wise to do cautiously, like, with reject and refine options. For those confusable observations in refine region, we need more information or index to give a more confident result. Moreover, many other loss functions and penalties can be incorperated into this framwork for further needs.






























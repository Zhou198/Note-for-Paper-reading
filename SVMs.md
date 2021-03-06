### Content
* [Support Vector Machines with a Reject Option](#SVMwRO)
* [Multicategory Support Vector Machines](#MSVM)
* [On Reject and Refine Options in Multicategory Classification](#ORaROiMC)
* [Multicategory Large-Margin Unified Machines](#MLMUM)
* [Learning Confidence Sets using Support Vector Machines](#LCSuSVM)
* [Least Ambiguous Set-Valued Classifiers with Bounded Error Levels](#LABEL)



<h2 id="SVMwRO">
 
### [Support Vector Machines with a Reject Option](https://arxiv.org/pdf/1201.1140.pdf) 
<p align="right"> Oct. 12, 2019 </p>

</h2>


<h2 id="MSVM"> 
 
### [Multicategory Support Vector Machines](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.129.3020&rep=rep1&type=pdf)
<p align="right"> Oct. 15, 2019 </p>

Two general strategies are used to tacke multicategory classification problems with SVMS: 1) Construct pairwise binary SVMs (1-versus-1). So there are $\binom{k}{2}=k(k-1)/2$ binary SVMs. However, this approach will potentially increase the variance since it use less observations in each SVM. Moreover, the total number of binary classifiers gets more and more with increasing $k$. 2) Combing the rest classes as another a new class and then constrcut binary SVMs (1-versus-rest), where there are $k$ binary SVMs. If there is no dominate class ($P(Y=j|X=x)<\frac{1}{2}$ for all $j=1, 2, \cdots, k$), then the output will obscure since $f_j(x)$ are close to $-1$ for all $j=1, 2, \cdots, k$. So this paper constructs the MSVM to treating all the class simutaneously, which means for each observation the outpout is a vector $\boldsymbol{f}(\mathbf{x})=(f_1(\mathbf{x}), f_2(\mathbf{x}), \cdots, f_k(\mathbf{x}))$ with the sum-to-0 constraint. This method can also target bayes rule in the same fashion in binary SVMs.

Our goal is to
$$\min \frac{1}{n}\sum\limits_{i=1}^n \mathbf{L}(\mathbf{y_i}) \cdot(\boldsymbol{f}{(\mathbf{x_i})-\mathbf{y_i})\_{+}}+\frac{1}{2}\lambda\sum\limits_{j=1}^k\left\|\|h_j\|\right\|^2_{H_k},$$ 
where $f_j(\mathbf{x_i})=h_j(\mathbf{x_i})+b_j$ and $\mathbf{L}(\mathbf{y_i})$ is a cost vector with each entrie a cost of classfying $y_i$ as label $j$'s. Note, $\mathbf{y_i}$ is a code vector, where $j$-th entry is $+1$ and remining are $-\frac{1}{k-1}$ if this observation $\mathbf{x_i}$ is labeled as class $j$. This implies $\sum\limits_{j=1}^k y_{ij}=0$.

This appraoch unifies both standard cases and unstandard cases. In standard cases, cost $c_{ij}$ of classfying label $i$ as $j$ are same for each $j=1, 2, \cdots, k$ and $j\neq i$, of course $c_{ii}=0$. Moreover, there is no bias in sampling, which means propotion of each class in training data is same to that in whole data. In unstandard cases, $c_{ij}$ differs in $j$'s, and maybe there are biases in sampling. Whatever, the MSVM approach can present the unified form covering above cases in loss fucntions.

Implenting SVMs or MSVM in an asymptotically efficient manner is dependent on choosing $\lambda$ for penalty. In this paper, it compares results of choosing $\lambda$ based on different criterions: 1) 10-folds crossvalidation, where it chooses $\lambda$ with minimum misclassification; 2) Generalized approximate crossvalidation (GACV), where it chooses optimal $\lambda$ with minimum objective function (loss + penalty) not misclassification; 3) GCKL, where it choose optimal $\lambda$ only with minimum loss. In one numerical study, 10-folds crossvalidation and GCKL peformance better than GACV and are close to bayes rule.
</h2>


<h2 id="ORaROiMC">
 
### [On Reject and Refine Options in Multicategory Classification](https://arxiv.org/pdf/1701.02265.pdf) 
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

Next part refers to convergence of the excess $\ell $-$ $risk in linear learning, which is define as $$e\left(\boldsymbol{f}, \boldsymbol{f}^{(p, k)}\right)=\mathbb{E}\left[\sum\limits_{j\neq Y}\ell\left\\{\left<\boldsymbol{f}(\boldsymbol{X}), \mathcal{Y}\_j\right>\right\\}\right]-\mathbb{E}\left[\sum\limits_{j\neq Y}\ell\left\\{\left<\boldsymbol{f}^{(p, k)}(\boldsymbol{X}), \mathcal{Y}\_j\right>\right\\}\right],$$ where $\boldsymbol{f}$ is any function restricted by $s$ and $\boldsymbol{f}^{(p, k)}$ is a minimizer (only to loss, here namely $\ell $-$ $loss) with no restriction (which means $s\rightarrow\infty$). If $k$ is bounded and true classification signals are sparse, then we can choose a large $s$ such that approximate error in $e\left(\boldsymbol{\hat f}, \boldsymbol{f}^{(p, k)}\right)$ is $0$, then for $L_1$ penalty, $e\left(\boldsymbol{\hat f}, \boldsymbol{f}^{(p, k)}\right)=O\left(r\log(r^{-1})\right)$ (simlilar to $L_2$ penalty), almost surely under $\mathbb{P}$. If $k\rightarrow\infty$ as $n\rightarrow\infty$ and assume the signals for classification on subcollections of the whole class set are finite, then, under $L_1$ penalty, we can choose $s=O(k)$ such that approximation error is $0$ and $e\left(\boldsymbol{\hat f}, \boldsymbol{f}^{(p, k)}\right)=O\left(k^2r\log(r^{-1})\right)$, almost surely under $\mathbb{P}$.

In numerical studies, compared with regular classier (outputs definite label for each obseravtion) and classifier with only reject option, the classifier with reject and refine option performs quite well by introducing reject and refine regions. Note there is no misclassification in reject rejoin and we report the mis-refinement rate in refine regions, which is defined as the porpotion of observations whose true labels are not in the refine sets.

In conclusion, when the cost for misclassification is too high to bear, it may be wise to do cautiously, like, with reject and refine options. For those confusable observations in refine region, we need more information or index to give a more confident result. Moreover, many other loss functions and penalties can be incorperated into this framwork for further needs.
</h2>

<h2 id="MLMUM">

### [Multicategory Large-Margin Unified Machines](http://www.jmlr.org/papers/volume14/liu13a/liu13a.pdf) 
<p align="right"> Oct. 22, 2019 </p>

Soft and hard classifiers are two important methods to do classification, where the prior one focuses on the estimation of conditional probibility while the later relies on decision boundries. It is unclear to choose which one given a practice problem. Therefore, this paper proposed a method extending binary classification to multicategory problem with Large-Margine Unified Machines (MLUM), which combines the soft and hard classifiers togethor by tuning the parameter in loss function. This method reveals the transition behaviors from soft to hard method in classification problems.

Because the drawback of some multicategory classification methods like, one-versus-on and one-versus-rest, this MLUM also deals with all classes simultaneously and the loss family given an observation is $$V\left(\boldsymbol{f}, y\right)=\gamma\ell\left(f\_y\left(\boldsymbol{x}\right)\right)+\left(1-\gamma\right)\sum\_{j\neq y}\ell\left(-f\_j\left(\boldsymbol{x}\right)\right),$$under sum-to-0 constraint, where $\ell\left(\mu\right)$ is loss function $$\ell(\mu)\begin{cases}
  1-\mu, & \mbox{if}\ \mu<\frac{c}{1+c}  \\\\
  \frac{1}{1+c}\left(\frac{a}{(1+c)a-c+a}\right)^a, & \mbox{if}\ \mu\geq \frac{c}{1+c}  \\\\
\end{cases},$$ where $c\geq 0$ and $a>0$. Moreover, $c=0$ represents a typical soft classifier and $c\rightarrow\infty$ represents a hard classifier, which is classical SVM. Distance Weighted Discriminant (DWD) is a sepecial case with $c=1$ and $c=1$.

A nice property of MLUM is Fisher consistent with $c\in[0, \infty)$, $a>0$ and $\gamma\in[0, 1]$. We denote conditional $V$$-$loss as $S\left(\boldsymbol{f}, \boldsymbol{x}\right)=\sum\limits\_{j=1}^kV\left(\boldsymbol{f}, j\right)P\_j\left(\boldsymbol{x}\right)$. Then fisher consistency means given any $\boldsymbol{P}\left(\boldsymbol{x}\right)$, the minimizer $\boldsymbol{f}^\ast(\boldsymbol{x})=\left(f^\ast\_1\left(\boldsymbol{x}\right), \cdots, f^\ast\_k\left(\boldsymbol{x}\right)\right)$ of $S\left(\boldsymbol{f}, \boldsymbol{x}\right)$ is such that $\mathop{\arg\max}\limits\_{j}P\_j\left(\boldsymbol{x}\right)=\mathop{\arg\max}\limits\_{j}f^\ast\_j\left(\boldsymbol{x}\right)$. Theorem 3 gives the probability estimation formula for MLUM with any finite $c$ and the strategies to scale probabilities, where they outsides the range $[0, 1]$ when $\gamma\neq 1$, such that the sum is $1$.

Denote excess risk ($0-1$ loss) as $R\left(f\right)-R^\ast$, where $f$ is theoretical minimizer to $0-1$ loss in function space (may be restricted by regularization), $R\left(f\right)$ is expected loss of $f$ and $R^\ast$ is Bayes error. Likewise, define $Q\left(\boldsymbol{f}\right)-Q^\ast$ as excess $V$-risk, where $Q^\ast=\inf Q\left(\boldsymbol{f}\right)$ (enlarge the function space until get the infimum or no restriction).
</h2>

<h2 id="LCSuSVM">
 
### [Learning Confidence Sets using Support Vector Machines](https://papers.nips.cc/paper/7741-learning-confidence-sets-using-support-vector-machines.pdf) 
<p align="right"> Oct. 31, 2019 </p>

This paper proposed a method to do set-valued multicategory classification with SVM. A little different from other set-valued prediction methods like, classification with reject and refine option, not only it gives coverage guarantee for classification (class-specific accuracy $-$ confidence), but also try to minimize the ambiguity $-$ efficiency, which refers the expected cardinality ($\geq 1$) of prediction set for a random observation.

We can convert non-coverage probability in constraint and expected cardinality into forms with $0$-$1$ loss function. However, we instead use certain surrogate loss upper bounding $0$-$1$ loss to do optimization. For minimizing the objective function, it use DC algorithm since the loss function is not convect. For the non-coverage constraint, they add some weights on loss to approximate $0$-$1$ loss.

Additionally, this kind of truncted hinge loss function is also FIsher consisitent. And the excess ambiguity measured under the surrogate loss can bound that measured under $0$-$1$ loss. For the former quantity, which can be decomposed into estimate error and approximate error, they prove the estimate error is $O(n^{-1/2})$ when the class number is fixed. Then the expected ambiugity under traning data will converge to the ambiguity induced by inifinite sample. Moreover, for the empirical non-coverage rate computed under weighted hige loss will also converge to the preset value $-$ class specific misclassification error.

In numerical study, they compare the empirical embiguity under proposed method with that under other soft and hard classifiers like, logistic regression with $\ell_2$ penalty, kernel logistic regression, kNN, rf, MSVM and k-binary-SVM, while tuning the non-coverage rate to be same. When non-coverage rate is low, the proposed method is better than plug-in methods and other hard classifiers. When non-coverage rate grows up, it still significantly dominates other hard classifiers or close to the best soft method. In high-dimensional data, this proposed approach outperforms than plug-in method since the density estimation is a problem in this situaution.

What I learned: The goal of classification with reject and refine option is minimizing the loss function by introducing reject and refine rejoin while that of confidence set learning is minimizing the ambiguity while controlling the misclassification. For non-convex loss in this paper, we can consider to utilize DC alogrithm ([Le Thi Hoai and Tao, 1997](https://s3.amazonaws.com/academia.edu.documents/49613176/a_3A100828841171020161015-29005-1cjqf12.pdf?response-content-disposition=inline%3B%20filename%3DSolving_a_class_of_linearly_constrained.pdf&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWOWYYGZ2Y53UL3A%2F20191101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20191101T040753Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=27323f75b624bb76b04b93894057b1670f926906563345bcfa2551ab2753af29); [Wu and Liu, 2007](https://stat-or.unc.edu/files/2016/04/07_11.pdf)).
</h2>

<h2 id="LABEL">

### [Least Ambiguous Set-Valued Classifiers with Bounded Error Levels](https://arxiv.org/pdf/1609.00451.pdf) 
<p align="right"> Nov. 3, 2019 </p>

Similar to Learning Confidence Set, LABEL method also minimizes the total ambiguity under controlling total or class-specific coverage probability. This proposed method constructed by conformal prediction, where the conformal score are obtained through estimating $p(y|x)$ (plug-in method). It outputs the desired prediction sets by increasing the class regions via decreasing thresholds. Moreover, it does not assume there is no null-region in feature space at first, although at the last step it will be covered by some methods if the null regions actually exists at first because of some reasons. However, for prior method, the default assumption at begining is the feature space is only covered by classes without null region because the setting in loss function already guarantees there definitely exists overlap. Also, it minimizes the ambiguity $-$ a surrogate loss function under the constraint $-$ non-coverage rate, which implemented with a hard classifier $-$ multicategory SVM.

Several approaches are mentioned when estimating $p(y|x)$, like regularized multinomial logistic regression, kNN, local polynomial estimator (covers kernel estimation). To reduce the computation expensiveness, it adopts splied-conformal inference, where data is splitted into $\mathcal{I}_1$ used to estimate formula of $\hat p(y|x)$ and $\mathcal{I}_2$ used to find conformal scores.

If there is a null region at first, it can be covered by asigning an arbitrary label for each observation in that region. However, this assumes automatically thereis no set-valued class, which sometimes is invalid. The accretive completion method remedies above defect, where we should notice the completion rates are not same for each class.

For the numerical study part, in order to compare LABEL and Classification with Regect Option (CWR), we should set the non-coverage rate as the misclassification error minimized from CWR and then observe the ambiguities in these methods. Satisfyingly, LABEL has smaller ambiguity while CWR has an ambiguous region with whole class. Actually, I think the ambiguous regions produced by LABEL can be viewed as refine option.  

What I understand: Several potential reasons cause null region: 1) non-coverage rate is too large; 2) data is sell-separated and 3) there exists outliers far away from classes. However, in my opinion, if we allow the null region exists, there is no step for minimizing ambiguity when using comformal scores to set coverage probability. Moreover, we can take Classification with Reject and Refine Option as a candidate in the comparison part.

</h2>





















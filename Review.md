### Review of confident predictions
For traditional classification in machine learning, the task is assigning one label for each observation. However, sometimes observations from different classes may share similiar features or they are fairly close, espectially when the number of class in a dataset is large. In this situation, single-label predition is less efficient and might give higher error. To tackle this kind of trouble, it is better to give a set of possible labels, particularly when missclassification will recur a high cost.

Based on above motovations, recently set-valued classifiers or confident predictions are developed. What I have learned up to now, totally, there are 3 different and related methods called Classification with Reject Option (CRO), Conformal Prediction (CP) and Confidence Sets Learning (CSL).


#### Classification with Reject Option
Herbei and Wegkamp 2006 studied binary classification equipped with reject option, where we do not give decision for those observations with conditional probability close to $\frac{1}{2}$. Different from traditional binary classification, now the risk is defined by misclassification error as well as rejection probability with a preset cost $d$. Moreover, they generalized theories for pulg-in rules and emprical risk minimizers. 

However, sometimes it is hard to estimate a probability like in a high dimensional feature space. Bartlett and Wegkamp 2008 used hard classifiers (with surrogate Hinge Loss) instead of soft classifiers (conditional probability estimation) to study CRO. One of most advatange is the modified risk involved with Hinge Loss can be efficiently minimized because the original risk is not convex. Also, the excess risk can be bounded by the excess $\phi$-risk. Additionally, they proved the classification result is (Fisher) consistent when sample size tends to infinity. Moreover, it was shown that the convergence rate is fast when $\eta(x)$ is far away from a threshold.

Without reject option, Hinge Loss in traditional binary classification is still fisher consistent. For CRO, Yuan and Wegkamp 2010 then extended Hinge Loss to some other convex loss functions (those should satisfy some conditons) and found they are also asymptotically consistent.

Although CRO can be extended for multicategory classifications, besides those observations in reject option, decsions on class-wise boundries may still be inefficient. Therefore, Zhang et al. 2017 proposed a new method called On Reject and Refine Options in Multicategory Classification. The basic idea is assigning the whole class to observations falling into a reject option, a subset of the whole class to those falling into refine options as well as a definite result for the remaining. Moreover, they utilized angle-based multicategory classification instead of regular SVMs to improve the computational efficiency. Not only the propsed one is much cautious and informative, but also has fast convergence rate of excess $\ell$-risk, theoretically.


#### Conformal Prediction

The research about conformal prediction resulted in a book, Algorithmic learning in a random world by Vovk, Gammerman and Shafer, published by Springer, New York, in 2005. This framework is constructed based on p-value equipped with hypothesis test under exchangebility assumption. The most important idea is to find a score function for each observation over all potential labels and then to assign those labels for this instance if corresponding scores are large enough. Two properties of this method are validity (converage probability $1-\varepsilon$)and efficiency (expected cardinality of the prediction set), where prior one is well-calibrated under the assumption and the latter depends on the score estimation (how much it is close to the Bayes rule).

Lei et al. 2011 introduced a nonparametric smoothing method, namely kernel density estimation, as a score function. Moreover, they proposed a method ($\lfloor n\varepsilon \rfloor$-th quantile among $n$ many observations) sandwitching estimated conformal sets ($\lfloor (n+1)\varepsilon \rfloor$-th quantile among $n+1$ many observations), where the inner set does not have a finite sample validity like an approach given by Chatterjee and Patra 1980, Zhao and Saligrama 2009. Although the outer set is a little bit larger than an estimated conformal set, it is less computational expensive and the finite sample validity is guaranteed. For another property, i.e., asymptotic efficiency (it is here defined as the excess risk $\mu(\hat{C^\varepsilon})-\mu(C^\varepsilon)$, where $\mu$ is a Lebesgue measure) can be achieved when the kenerl density is smooth, which depends on the bandwidth (They use cross-validation to select out an empirically optimal value).

Comment for sandwitch approximation: Different from general conformal prediction, when preserving the finite sample validity, this method also avoids data augmentation (we can see from the quantile) and then improve the computaional efficiency.

Later, Lei and Wasserman 2013 studied more cases about validity and efficiency, where densities are treated as scores. When simply applying a sandwitch approximation to $Z=(X, Y)$ from $Z=Y$, it is not efficient although the finite sample (joint) validity still holds. Another simliar notion is conditional validity. Unfortunately, we cannot gaurantee object conditional validity and asymptotic efficiency at the same time. However, if a datset is partationed into $\\{A_k\\}\_{k\in \mathbb{N}^+}$, each of which is used to estimate kernel density of potential $Y$ (or $(X, Y)$ or $Y|X$), for prediction sets obtained by above sandwitch approximation over all partations, thus finite sample local validity as well as asymptotic conditional validity can be achieved. when talking about convergence rate for asymptotic efficiency, besides the requriement of smoothness for density estimation, it is also related to the partation (of course we can treat it as a parameter to tune).

I think the procedure of constructing local validity is similar to Venn prediction and maybe we can use other scores from hard classifiers instead of plug-in method because probability estimation is difficult in the high dimensional setting.

Hechtlinger et al. 2018 argued the difference between label and object conditional densities and used the former as conformal scores in their work, which is better for outlier detection. Since this kind of score is class-independent to others, it may ignore the relations among classes. One potential modification is to redefine a label conditional density related to other classes. Similarly, 
Dümbgen et al. 2008 discussed the difference between above two conditional densities when choosing score functions. Object conditional density means we assume there is no outliers although the prediction could be a null region while label conditional density does not need to assume that. Therefore, considering outlier detection as well as interclass relationship, they introduced the weight for outliers to comprise above situations when using object conditional densities. Moreover, they talked something about the finite sample validity when using 3 different methods dealing with efficiency of p-value's computation. However, up to now, I think the data-splitting method Lei proposed is much more perfect.

Tibshirani et al. 2019 relaxed the exchangebility assumption to covariate shift (i.e., feature from testing data is differently distributed from training while the object conditional distribution remains unchanged) but add another constrain that we should know the covariate likelihood ratio or it can be estimated. Thus, scores are not uniformly distributed any longer and weights are related to the likelihood ratios.

We can predcit out a null region under no outlier assumption, under which, however, we may also assign a label for a genuine outlier from testing set (This means testing data is differently distributed from training due to outliers rather than covariate shift). By this motivation, like the work of Dümbgen et al. 2008, Guan and Tibshirani 2019 add a proportion of outliers to form a new distribution. By a trick similiar to that in Tibshirani et al. 2019, they instead estimated a related quantity to avoid giving the proportion of outliers.

#### Confidence Set Learning

This framework is related to conformal prediction and Lei 2014 proposed the notion of confidence, which exactly is label conditional validty and then conformal prediction is equivalent to confidence set learning when the former deals with class-specific validity instead of total validity (I will check this understanding with my professor). A little difference from conformal prediction is here we have an assumption that prediction regions form the whole feature space (there exists overlap but no null region).

Sometimes conditional probability $\hat\eta(x)$ from plug-in methods is not an accurate approxmation to the truth or not smooth, it will fail our inferences. Lei 2014 proposed a robust method, splitting conformal inference, to impove the robustness as well as computational efficiency frequently mentioned in futher reseraches. In this paper, he applied plug-in methods on a score function for binary classification. Certainly, the assumption of no null region can be guaranteed when setting thresholds by a trick. The potential extention is using other scores (or monoton functions of $\eta$).

Following that, Sadinle et al. 2017 generalized the work to a multicategory setting from above binary one. Moreover, they dropped the restrication of prediction region forming the whole space at first. However, in order to satisfying that requirement, some methods are applied for filling null regions, i.e., filling with baseline classifer and accretive completion. The former is easy but not optimal
while the latter can minimize the cardinality of the prediction set although the procedure is complicated.

Comment: Some optimal classifiers can also output empty prediction, i.e, null region, when the preset significan level is too low or the dataset is well-seperating.

Although plug-in method is straightforward intuitively, high dimensional setting makes it difficult and sometimes true bayes rule still cannot guarantee the prediction is not a null region. Therefore, Wang and Qiao 2018, 2019 extended above two works to counterparts with SVMs and solved the optimization with surrogate hinge losses. The loss functions they constructed satisfy the assumption of the whole feature space. Theoretically, it also shown the result is Fisher consistent.

Denis and Hebiri 2015, 2017 studied dual problems of Lei 2014 and Sadinle et al. 2017, i.e., minimizing the missclassification error while controling the size of the prediction set. In binary setting, the prediction set size is identical to rejection probability or to classifying probability. They used the estimation of function related $\eta$ to search the threshold under the controled classifying proportion, where it does not need the information of labels and hence makes it invovled with semi-supervised learning. In multicategory setting, they generalized $\eta$ to other score functions. In my understanding, there might exist a problem if we use the score function without label to define a prediction set.













### Review of confident predictions
For traditional classification in machine learning, the task is assigning one label for each observations. However, sometimes observations from different classes may share similiar features or they are fairly close, espectially when the number of class in a dataset is large. In this situation, single-label predition is less efficient and might give higher error. To tackle this kind of trouble, it is better to give a set of possible labels, particularly when missclassification will recur high cost.

Based on above motovations, recently set-valued classifiers or confident predictions are developed. What I have learned up to now, totally, there are 3 different and related methods called Classification with Reject Option (CRO), Conformal Prediction (CP) and $\varepsilon$-Confidence Sets Learning (CSL).

#### Classification with Reject Option
Herbei and Wegkamp 2006 studied binary classification equipped with reject option, where we do not give decision for those observations with conditional probability close to $\frac{1}{2}$. Different from traditional binary classification, now the risk is defined by misclassification error as well as rejection probability with preset cost $d$. Moreover, they generalized theories for pulg-in rules and emprical risk minimizers. 

However, sometimes it is hard to estimate a probability like in high dimensional feature space. Bartlett and Wegkamp 2008 used hard classifiers (with surrogate Hinge Loss ) instead of soft classifiers (conditional probability estimation) to study CRO. One of most advatange is the modified risk involved with Hinge Loss can be efficiently minimized because original risk is not convex. Also, the excess risk can be bounded by excess $\phi$-risk. Additionally, they proved the classification result is (Fisher) consistent when sample size tends to infinite. Moreover, it was shown that the convergence rate is fast when $\eta(x)$ is far away from a threshold.

Without reject option, Hinge Loss in traditional binary classification is fisher consistent. For CPO, Yuan and Wegkamp 2010 then extended Hinge Loss to some other convex loss functions (those should satisfy some conditons) and found they are also asymptotically consistent.

Although CRO can be extended for multicategory classifications, besises those observations in reject option, decsions on class-wise boundries may still inefficient. Therefore, Zhang, Wang and Qiao 2017 proposed a new method called On Reject and Refine Options in Multicategory Classification. The basic idea is assigning the whole classes to observations falling into reject option, a subset of the whole classses to those falling into refine options as well as a definite result for the remaining. Moreover, they utilized angle-based multicategory classification instead of regular SVMs to improve the computational efficiency. Not only the propsed one is much cautious and informative, but also has fast convergence rate of excess $\ell$-risk, theoretically.


#### Conformal Prediction

The research about conformal prediction resulted in a book, Algorithmic learning in a random world by Vovk, Gammerman and Shafer, published by Springer, New York, in 2005. This framework is constructed based on p-value equipped with hypothesis test under exchangebility assumption. The most important idea is to find a score function for each observation over all potential labels and then to assign those labels for this instance if corresponding scores are large enough. Two properties of this method are validity (converage probability $\varepsilon$)and efficiency (expected cardinality of the prediction set), where prior one is well-calibrated under the assumption and the latter depends on the score estimation (how much it is close to Bayes rule).

Lei, Robins and Wasserman 2013 introduced a nonparametric smoothing method, namely kernel density estimation, as a score function. Moreover, they proposed a method sanwitching estimated conformal sets, where the inner set does not have finite validity like an approach given by Chatterjee and Patra 1980, Zhao and Saligrama 2009. Although the outer set is a little bit larger than an estimated conformal set, the finite sample validity is guaranteed. For another property, i.e., asymptotic efficiency (it is defined as the excess risk $\mu(\hat{C^\varepsilon})-\mu(C^\varepsilon)$),  it can be reached when the kenerl density is smooth, which depends on the bandwidth (They use cross-validation to select out an empirically optimal value).

Comment for validity: Based on comformal prediction framework when assumption holds, the asymptotic validity is always guarantted. However, finite sample validity is only hold on-line comformal prediction setting which is originally provided. Later this framework is extened to off-line setting, where, generally, we cannot guarantte the finite sample validity (it is also mentioned in Algorithmic learning in a random world by Vovk, Page 111).




#### $\varepsilon$-Confidence Sets Learning

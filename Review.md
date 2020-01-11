### Review of confident predictions
For traditional classification in machine learning, the task is assigning one label for each observations. However, sometimes observations from different classes may share similiar features or they are fairly close, espectially when the number of class in a dataset is large. In this situation, single-label predition is less efficient and might give higher error. To tackle this kind of trouble, it is better to give a set of possible labels, particularly when missclassification will recur high cost.

Based on above motovations, recently set-valued classifiers or confident predictions are developed. What I have learned up to now, totally, there are 3 different and related methods called Classification with Reject Option (CRO), Conformal Prediction (CP) and $\varepsilon$-Confidence Sets Learning (CSL).

#### Classification with Reject Option
Herbei and Wegkamp 2006 studied binary classification equipped with reject option, where we do not give decision for those observations with conditional probability close to $\frac{1}{2}$. Different from traditional binary classification, now the risk is defined by misclassification error as well as rejection probability with preset cost $d$. Moreover, they generalized theories for pulg-in rules and emprical risk minimizers. 

However, sometimes it is hard to estimate a probability like in high dimensional feature space. Bartlett and Wegkamp 2008 used hard classifiers (with surrogate Hinge Loss ) instead of soft classifiers (conditional probability estimation) to study CRO. One of most advatange is the modified risk involved with Hinge Loss can be efficiently minimized because original risk is not convex. Also, the excess risk can be bounded by excess $\phi$-risk. Additionally, they proved the classification result is (Fisher) consistent when sample size tends to infinite. Moreover, it was shown that the convergence rate is fast when $\eta(x)$ is far away from a threshold.

Without reject option, Hinge Loss in traditional binary classification is fisher consistent. For CPO, Yuan and Wegkamp 2010 then extended Hinge Loss to some other convex loss functions (those should satisfy some conditons) and found they are also asymptotically consistent.

Although CRO can be extended for multicategory classifications, besises those observations in reject option, decsions on class-wise boundries may still inefficient. Therefore, Zhang, Wang and Qiao 2017 proposed a new method called On Reject and Refine Options in Multicategory Classification. The basic idea is assigning the whole classes to observations falling into reject option, a subset of the whole classses to those falling into refine options as well as a definite result for the remaining. Moreover, they utilized angle-based multicategory classification instead of regular SVMs to improve the computational efficiency. Not only the propsed one is much cautious and informative, but also has fast convergence rate of excess $\ell$-risk, theoretically.


#### Conformal Prediction






#### $\varepsilon$-Confidence Sets Learning

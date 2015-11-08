---
layout: post
title:  "A Wrapper Class of PU classification for scikit-learn's Probabilistic Classifiers"
date: 2015-11-07 17:23:19 +0900
image: assets/result_of_puclassification.png
categories: jekyll update
---
**Notations** :  
$$ \boldsymbol{x} \in \mathbb{R}^d $$: random vector drawn from $$ p(\boldsymbol{x}) $$   
$$ y \in \{-1,1\} $$: random variable which indicates positive (1) or negative (-1) drawn from $$ p(y) $$  
$$ s \in \{0,1\} $$: random variable which indicates labeled (1) or unlabeled (0) drawn from $$ p(s) $$  
$$ \{(\boldsymbol{x}_i,s_i)\}_{i=1}^n $$ i.i.d. sample drawn from $$ p(\boldsymbol{x},s) $$

PU classification is a framework for learning classifiers from positive and unlabeled data. This is firstly introduced by Elkan and Noto, "Learning Classifiers from Only Positive and Unlabeled Data" (ACM 2008). 
The goal of traditional classification problem is to estimate $$ p(y|\boldsymbol{x}) $$ from i.i.d. sample $$ \{(\boldsymbol{x}_i,y_i)\}_{i=1}^n $$. 
On the other hand, In the setting of PU classification, our goal is to estimate $$ p(y|\boldsymbol{x}) $$ from $$ \{(\boldsymbol{x}_i,s_i)\}_{i=1}^n $$. 

Elkan and Noto showed that under some assumptions, we can express
$$ p(y=1|\boldsymbol{x}) $$ as,

$$
p(y=1|\boldsymbol{x}) = \frac{p(s=1|\boldsymbol{x})}{p(s=1|y=1)}
$$

We can estimate $$ p(y=1|\boldsymbol{x}) $$
from
$$ \{(\boldsymbol{x}_i,s_i)\}_{i=1}^n $$, and $$ p(s=1|y=1) $$ can be estimated by cross-validation. 

In this article, I introduce a wrapper class of PU classification for scikit-learn's classifiers, [puwrapper.py][puwrapper.py]. We employ Elkan's method in this wrapper class. 

All we need to use this class is wrap the scikit-learn's probabilistic classifiers like this:

{% highlight python %}
from puwrapper import PUWrapper
from sklearn.linear_model import LogisticRegression
clf=PUWrapper(LogisticRegression())
{% endhighlight %}

Now let's see the demo.
The figure below is data with true labels.

![image name]({{nktmemo.github.io}}/assets/true_labeled.png)

Actually, we observe the following data:

![image name]({{nktmemo.github.io}}/assets/pu_data.png)

First let's apply ordinal Logistic Regression model (Note that we use positive's F1-value as score function of cross-validation since the data is highly imbalanced). The result is shown below.

![image name]({{nktmemo.github.io}}/assets/result_of_tradclf.png)

Finally we applied Elkan's method. The result is shown below.

![image name]({{nktmemo.github.io}}/assets/result_of_puclassification.png)

As you can see that, we could classify the data into positive and negative accurately.
The demo code is available here: [pu_demo.py][pu_demo.py]

[pu_demo.py]: https://gist.github.com/nkt1546789/e9421f06ea3a62bfbb8c
[puwrapper.py]: https://gist.github.com/nkt1546789/9fbbf2f450779bde60c3

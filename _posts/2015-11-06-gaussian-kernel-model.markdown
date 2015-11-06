---
layout: post
title:  "RBF (Gaussian) Kernel Model"
date:  2015-11-06 15:12:11 +0900
categories: jekyll update
---
#### Notations:
- $$\boldsymbol{x} \in \mathbb{R}^{d}$$: input vector
- $$\mathcal{X} = \{\boldsymbol{x}_i\}_{i=1}^n$$: training sample
- $$f$$: decision function

In classification problem, our goal is to estimate $$f$$ accurately. 
Sometimes we need to use nonliner function for $$f$$.
In such case, RBF (Gaussian) kernel model defined as,

$$
\begin{align*}
f(\boldsymbol{x}) &= \sum_{j=1}^b \theta_j k(\boldsymbol{x},\boldsymbol{c}_j) \\
k(\boldsymbol{x},\boldsymbol{x}') &= \exp\left(-\gamma\|\boldsymbol{x}-\boldsymbol{x}'\|^2\right).
\end{align*}
$$

where $$\{\boldsymbol{c}_j\}_{j=1}^b \subseteq \mathcal{X}$$ is reasonable and useful.

In this article, I introduce a wrapper class, [rbfmodel_wrapper.py][rbfmodel_wrapper.py], for some scikit-learn's classifiers to use Gaussian kernel model.
Using this class, we can easily make classifiers nonlinear.
For example, Logistic Regression is nonlinearized by,
{% highlight python %}
clf=RbfModelWrapper(LogisticRegression(),gamma=1.)
{% endhighlight %}

We can also use GridSearch for hyperparameter selection as,
{% highlight python %}
grid=GridSearchCV(RbfModelWrapper(LogisticRegression(),param_grid={"gamma":np.logspace(-2,0,9),"C":[1,10,100]}))
{% endhighlight %}

I show a demo code below.

{% highlight python %}
import numpy as np
from sklearn.linear_model import LogisticRegression
from sklearn import datasets
from sklearn.grid_search import GridSearchCV
import matplotlib.pyplot as plt
np.random.seed(1)

n=500
X,y=datasets.make_moons(n_samples=n,noise=.05)
idx=np.random.permutation(n)
ntr=np.int32(n*0.7)
itr=idx[:ntr]
ite=idx[ntr:]

param_grid={"gamma":np.logspace(-2,0,9)}
grid=GridSearchCV(RbfModelWrapper(LogisticRegression()),param_grid=param_grid)
grid.fit(X[itr],y[itr])
clf=grid.best_estimator_
print "accuracy:",clf.score(X[ite],y[ite])

offset=.5
xx,yy=np.meshgrid(np.linspace(X[:,0].min()-offset,X[:,0].max()+offset,300),
                  np.linspace(X[:,1].min()-offset,X[:,1].max()+offset,300))

Z=clf.predict(np.c_[xx.ravel(),yy.ravel()])
Z=Z.reshape(xx.shape)

a=plt.contour(xx, yy, Z, levels=[0.5], linewidths=2, colors='green')
b1=plt.scatter(X[y==1][:,0],X[y==1][:,1],color="blue",s=40)
b2=plt.scatter(X[y==0][:,0],X[y==0][:,1],color="red",s=40)
plt.axis("tight")
plt.xlim((X[:,0].min()-offset,X[:,0].max()+offset))
plt.ylim((X[:,1].min()-offset,X[:,1].max()+offset))
plt.legend([a.collections[0],b1,b2],
           [r"decision boundary","positive","unlabeled"],
           prop={"size":10},loc="lower right")
plt.tight_layout()
plt.show()

{% endhighlight %}


The result is like this:

```
accuracy: 1.0
```

![image name]({{nktmemo.github.io}}/assets/rbfmodel_demo.png)

[rbfmodel_wrapper.py]: https://gist.github.com/nkt1546789/e41199340f7a42c515be


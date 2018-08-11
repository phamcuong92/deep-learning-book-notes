# 8 Optimization for Training Deep Models

`page 268`

> We therefore optimize P only indirectly.

The optimization is indirect in two ways.

First, we optimize over the training (empirical) distribution, although we are actually concerned about the data-generating distribution. We typically take the training distribution as being approximately representative of the underlying data-generating distribution. Differences in performance then appears in the form of generalization error, which we try to mitigate with regularization measures.

Second, the quantity being optimized is frequently different from the quantity we are actually concerned about. This is usually because the latter is non-differentiable. For example, when training a classifier, we typically minimize the cross-entropy loss between the prediction and the label. But what we actually want is to maximize the accuracy. In particular, although the cross-entropy loss and accuracy are mostly aligned, they still have a non-monotonic relationship ie. an decrease in cross-entropy loss does not necessarily imply an increase (or decrease) in accuracy.

`page 272`

> Small batches can offer a regularizing effect

And on that note, large batches can give the opposite effect and lead to faster overfitting. As mentioned in the text, it is important to increase the nubmer of steps when using smaller batches, since it will take more steps to finish a single epoch (one run through the entire training set). Also mentioned, a smaller learning rate might also be needed due to the increase in noise for smaller batch sizes.

`page 273`

> Failing to ever shuffle the examples in any way can seriously reduce the effectiveness of the algorithm.

A similar problem was encountered in reinforcement learning, where the experiences used to the agent is highly correlated and chronological. A large improvement was achieved with *experience replay* - storing and randomly sampling from a set of experiences for learning - which has become a popular technique used in reinforcement learning.

`page 276` Ideally, when we arrive at the global or a local minimum of the loss function, the local gradient should be zero (actually it should be zero at any stationary point). However, Figure 8.1 shows that this does not actually happen in practice. Instead, the figure shows the gradient norm actually increasing. Yet, we see that the corresponding validation classification error does decrease to a low level.

`page 277` **Weight Space Symmetry.** This is also somewhat related to the problem of few-shot classification, where a typical task might be 5-way 1-shot (ie. 5 classes with 1 example each). Depending on the algorithm and approach, rearranging the classes for a certain task can be interpreted as a new task (eg. switching classes 1 and 2). The metalearner has to be invariant to these changes and adaptive measures have to be taken to allow the metalearner to be 'symmetrical'.

`page 277`

> Whether newtons of practical interest home many local minima of high cost [...]

I believe there is a typo here, where *newtons* should be corrected to *networks*. This errata is still present in the [web version](http://www.deeplearningbook.org/contents/optimization.html) (see page 282). 

`page 278`

> To understand the intuition behind this behavior, observe that the Hessian matrix at a local minimum has only positive eigenvalues. The Hessian matrix at a saddle point has a mixture of positive and negative values. Imagine that the sign of each eigenvalue is generated by flipping a coin.

A pretty good explanation of why saddle points are far more common in high-dimensional spaces, although I'm not sure if the coin-flipping analogy holds in a mathematical sense.

`page 281`

> The cliff can be dangerous whether we approach it from above or from below [...]

Approaching it from above, the huge gradient due to the cliff leads to the gradient descent algorithm taking an excessibly large step, which might 'reset' and learning done by the weights.

Approaching it from below, a small step taken towards the cliff (perhaps due to a downward slope just before the cliff) will cause a sudden sharp increase in the loss as we jump to the top of the cliff.

`page 281` **Gradient Clipping.** The text mentions it as a solution against excessively large gradient steps due to cliffs. Another way to think about it is to see that gradient clipping prevents overflows or underflows causing exploding or vanishing gradients.

`page 285`


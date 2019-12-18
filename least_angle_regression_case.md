

#### _The advantages of LARS are_

It is numerically efficient in contexts where p >> n (i.e., when the number of dimensions is significantly greater than the number of points)
It is computationally just as fast as forward selection and has the same order of complexity as an ordinary least squares.
It produces a full piecewise linear solution path, which is useful in cross-validation or similar attempts to tune the model.
If two variables are almost equally correlated with the response, then their coefficients should increase at approximately the same rate. The algorithm thus behaves as intuition would expect, and also is more stable.
It is easily modified to produce solutions for other estimators, like the Lasso.

#### _The disadvantages of the LARS method include_

Because LARS is based upon an iterative refitting of the residuals, it would appear to be especially sensitive to the effects of noise. 
This problem is discussed in detail by Weisberg in the discussion section of the Efron et al. (2004) Annals of Statistics article.
The LARS model can be used using estimator LARS, or its low-level implementation lars_path



LassoLars is a lasso model implemented using the LARS algorithm, and unlike the implementation based on coordinate_descent, 
this yields the exact solution, which is piecewise linear as a function of the norm of its coefficients.

# mpcmp 0.2.0

  * Added a `NEWS.md` file to track changes to the package. 
  * Added a draft logo to the package.
  * Ribeiro Jr et al. (2018) specification of the CMP model is utilised to provide a better initial estimate for the dispersion parameter. Added `comp_mu_loglik_log_nu_only()` to facilitate the optimisation. 
  * `Z()`, the normalizing constant function, approximates its true value via (a fixed) truncation. This means the approximation would fail if the mean is large. 
  The followings are implemented as a fix:
    - A new function `logZ()` is created, based on a similar function in the `cmpreg` package of Ribeiro Jr, Zeviani & Demétrio (2019), and will supercede `Z()` due to its superior numerical stability.
    - A Chebyshev's inequality type argument is now implemented to have a more flexible upper truncation point. 

    `glm.cmp()`, `dcomp()`, `pcomp()`, `qcomp()`, `rcomp()` and functions that calculate expected values are updated to take advantage of these changes. 

```R
sum(0:500*dcomp(0:500,100,1.2))
sum(0:500*dcomp(0:500,150,0.8))
qcomp(0.6, 150, 1.2)
```
* Added the `fish` dataset as a proof of concept that `glm.cmp()` can handle some larger count data. 
```R
data(fish)
M.fish <- glm.cmp(species~ 1+log(area), data=fish)
max(M.fish$fitted.values)
```
* `comp_lambdas()` now has the ability to scale up \& down `lambdaub` so that the correct $\lambda$s can be found even if they are outside the preset boundary.  

# mpcmp 0.1.4
* `model.matrix()` now retrieves the design matrix of the model properly. 
* `glm.cmp()` gains a few standard glm arguments: `start`, `contrasts`, `na.action`, `subset`.

# mpcmp 0.1.3

* First major release of the package. 
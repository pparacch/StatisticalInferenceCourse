# Exponential distribution analysis
Pier Lorenzo Paracchini  

##Overview
The Central Limit Theorem (CLT) states that _"the distribution of averages of indipendent and identically distributed (iid) variables becomes that of a standard normal as the sample size increase."_  so in this assignment it will be investigate the behaviour of the __exponential distribution__ when looking at the distribution of averages of 40 exponentials (and more).  

##Simulations 
Let<U+00B4>s simulate an experiment with a random variable $X$ with an __exponential distribution__ with the following characteristics

* __rate parameter__ $\lambda = 0.2$ 
    * __mean__ $\mu = E[X_i] = 1/\lambda = 5$ and  __standard deviation__ $\sigma = \sqrt[2]{xVar(X_i)} = 1/\lambda = 5$
    * __standard error__ (SE) $\sigma/\sqrt[2]{n}$

For building the distribution of averages we will run thousands of simulation and for each simulation the following steps are executed:

* run the experiment $n$ time where `n = 40, 80, 120, 160`,
    * be $X_i$ the outcome for the experiment $i =1..n$.
* calculate the mean $\bar X_n$ using $X_1, X_2, .., X_40$ 
* calculate $\frac{\bar X_n - \mu}{\sigma / \sqrt{n}}$

The following the code snippet can be used to generate the simulation data.


```r
no_of_simulation = 1000
n = 40
clt_func <- function(x, n) sqrt(n) * (mean(x) - 5) / 5

dat <- data.frame(
  x = c(
      apply(matrix(rexp(n * no_of_simulation, 0.2), nrow = no_of_simulation), MARGIN = 1, clt_func, n),
      apply(matrix(rexp((2*n) * no_of_simulation, 0.2), nrow = no_of_simulation), MARGIN = 1, clt_func, (2*n)),
      apply(matrix(rexp((3*n) * no_of_simulation, 0.2), nrow = no_of_simulation), MARGIN = 1, clt_func, (3*n)),
      apply(matrix(rexp((4*n) * no_of_simulation, 0.2), nrow = no_of_simulation), MARGIN = 1, clt_func, (4*n))
      ),
  size = factor(rep(c(n, 2*n, 3*n, 4*n), rep(no_of_simulation, 4)))
  )
```


##Sample Mean versus Theoretical Mean 
Based on the __CLT__ the __theoretical mean__ is $\mu=0$ and the value of the sample mean is __0.0506595__ for n = 40. The __sample mean__ is around the __theoretical mean__ for `n = 40` and it converges more and more to it increasing the size of n (`n = 80, 120, 160`). 

![](assignment_part1_files/figure-html/meanDetails-1.png) 

##Sample Variance versus Theoretical Variance
Based on the __CLT__ the __theoretical variance__ is $\sigma^2=1$ and the value of the sample variance is __1.0607617__ for n = 40. The __sample variance__ is around the __theoretical variance__ for `n = 40` and it converges more and more to it increasing the size of n (`n = 80, 120, 160`). 

![](assignment_part1_files/figure-html/varianceDetails-1.png) 

##Distribution
Let<U+00B4>s plot the distribution of the averages previously calculated over all of the simulations together with the standard normal distribution $N(0,1)$. We can see from the plot below, the distribution of averages ($\frac{\bar X_n - \mu}{\sigma / \sqrt{n}}$) is a good approximation of a standard normal distribution $N(0,1)$  (black curve) as expected from the Central Limit Theorem.

![](assignment_part1_files/figure-html/plotGeneration-1.png) 

##Appendixies

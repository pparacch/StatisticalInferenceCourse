Week 1
======

Probability Density Function
----------------------------

Let's imagine that the proportion of help calls that get addressed in a
random day by a help line is given by the PDF below

    x <- c(-0.5,0,1,1,1.5)
    y <- c(0,0,2,0,0)

    plot(x, y, lwd = 3, frame = TRUE, type="l")

![](Statistica_Inference_playground_files/figure-markdown_strict/pdf-1.png)

The PDF valid

-   values are equal or greater then 0
-   total area is 1

What is the probability that 75% or fewer of call get addressed? Such
propability can be calculated as the area of the triangle highlited in
the diagram below

    plot(x, y, lwd = 3, frame = TRUE, type="l")
    lines(c(0.0, 0.75), c(0, 0), col = "red")
    lines(c(0.75, 0.75), c(0.0, 1.5), col = "red")
    lines(c(0.0, 0.75), c(0.0, 1.5), col = "red")

![](Statistica_Inference_playground_files/figure-markdown_strict/unnamed-chunk-1-1.png)


    calc_prob <- (0.75 * 1.5) / 2
    calc_prob
    ## [1] 0.5625

The given PDF is a special case of a well-known probaility distibution,
the **BETA distribution**. The sameprobability can be calculated using
the **BETA distribution** as in the following code chunk

    pbeta(0.75,2,1)
    ## [1] 0.5625

Some more details about the **BETA** distribution

    x <- seq(0, 1, length = 100)
    d <- dbeta(x, 2, 1) #density
    p <- pbeta(x, 2, 1) #probability of being less than x
    plot(x, d, type = "l")
    lines(x, p, type= "l", col = "red")

![](Statistica_Inference_playground_files/figure-markdown_strict/unnamed-chunk-3-1.png)

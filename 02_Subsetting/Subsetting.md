a test
------

And example I lifted from ch 2.

    # Two scalar arguments to specify rows and columns
    a <- matrix(1:6, ncol = 3, nrow = 2)
    # One vector argument to describe all dimensions
    b <- array(1:12, c(2, 3, 2))

    # You can also modify an object in place by setting dim()
    c <- 1:6
    dim(c) <- c(3, 2)
    c

    ##      [,1] [,2]
    ## [1,]    1    4
    ## [2,]    2    5
    ## [3,]    3    6

    #>      [,1] [,2]
    #> [1,]    1    4
    #> [2,]    2    5
    #> [3,]    3    6
    dim(c) <- c(2, 3)
    c

    ##      [,1] [,2] [,3]
    ## [1,]    1    3    5
    ## [2,]    2    4    6

    #>      [,1] [,2] [,3]
    #> [1,]    1    3    5
    #> [2,]    2    4    6

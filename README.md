
<!-- README.md is generated from README.Rmd. Please edit that file -->

# geometries

<!-- badges: start -->

<!-- badges: end -->

Have you every wanted to generate geometric structures from data.frames,
but independant of any R classes, attributes or libraries?

No? Ok, this library isn’t for you.

But if you answered ‘yes’, this might be of interest.

``` r

library(Rcpp)

cppFunction(
  depends = "geometries"
  , includes = '#include "geometries/shapes/shapes.hpp"'
  , code = '
    SEXP polygon( SEXP df, SEXP geometry_cols, SEXP line_id ) {
      return geometries::shapes::get_listMat( df, geometry_cols, line_id );
    }
  '
)

df <- data.frame(
  x = 1:10
  , y = 10:1
  , z = 21:30
  , m = 30:21
  , val = letters[1:10]
  , id = c( rep(1,5), rep(2,5) )
)

polygon( df, c("x","y"), c("id") )
# [[1]]
#      [,1] [,2]
# [1,]    1   10
# [2,]    2    9
# [3,]    3    8
# [4,]    4    7
# [5,]    5    6
# 
# [[2]]
#      [,1] [,2]
# [1,]    6    5
# [2,]    7    4
# [3,]    8    3
# [4,]    9    2
# [5,]   10    1
```

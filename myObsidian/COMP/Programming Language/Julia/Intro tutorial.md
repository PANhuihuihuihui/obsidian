multiple dispatch
Mathematically, we sometimes think of 1-D vectors as being a subset of 2-D matrices. Computationally, that is not the case. We can verify this by examining the typetree of the `Vector` and `Matrix` types:

The `vec` function returns all elements of an array as a vector. The columns of a matrix are placed in series with each other, as illustrated here:

Also, `range(1; step=2, stop=10)` is equivalent to `1:2:10`.
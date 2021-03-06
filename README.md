
#orca_array 
 
Author: Pramod Gupta, Department of Astronomy, University of Washington

Last Modified: 2015 Oct 27

orca_array consists of multi-dimensional array template classes array1d<T> to array7d<T>
with compile time options for array bounds checking and 
for accessing array elements via Fortran order or C order.

See orca_array.hpp for code.


**(1) Why are orca_array arrays only up to only upto 7 dimensions?**

* In classical physics, to describe a particle you need 3 space coordinates (x,y,z), 3 velocities (v_x, v_y, v_z) and time t.
* More than 7 dimensional arrays are very rare since memory usage increases exponentially like L^d
where L is the size of one dimension and d is the number of dimensions.
* If you need more dimensions, the array7d code can easily be modified for arrayNd.

**(2) What compilers can compile orca_array.hpp?**

orca_array.hpp has been compiled with g++, clang++, and icpc.


**(3) How can one choose between column-major and row-major order of accessing arrays?**

Choose one of below options in orca_array.hpp:

```C++
//First index changes fastest
#define FORTRAN_ORDER 1

//Last index changes fastest (C order)
#define FORTRAN_ORDER 0

```


**(4) Can you show examples of using orca_array arrays?**

```C++
#include "orca_array.hpp"

//defining 2D array
array2d<double> b(10,8);

//using 2D array
b.at(3,4)=3.14;

//Copy constructor and assignment operator are private.
//Hence pass all orca_arrays to a function by reference.

//passing 2D array to function
//m, n are optional
double trace(int m, int n, array2d<double> & myarray2d){
. . .
}

```



**(5) How can one turn on or turn off array bounds checking?**

Choose one of below options in orca_array.hpp:

```C++
#define ARRAY_BOUNDS_CHECK 1

#define ARRAY_BOUNDS_CHECK 0
```

If ARRAY_BOUNDS_CHECK  is 1 and during run time an array index is out of bounds then the program will encounter segmentation fault.

Compile program with -g option and run in debugger to identify line of code as shown below.

Suppose program xyz.cpp uses orca_array.hpp.
If program xyz.cpp has a bug and it runs into a segmentation fault 
due to array out of bounds or negative sizes of dimensions then use
below steps to identify the buggy line of code.


GNU Compiler:
```
g++ -g xyz.cpp -o xyz
gdb xyz
run
bt  (to get backtrace and find line of code)

```

Intel Compiler:
```
icpc -g xyz.cpp -o xyz
idbc xyz
run
bt  (to get backtrace and find line of code)

```




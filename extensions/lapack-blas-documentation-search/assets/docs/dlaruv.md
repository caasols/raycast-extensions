```fortran
subroutine dlaruv (
        integer, dimension( 4 ) iseed,
        integer n,
        double precision, dimension( n ) x
)
```

DLARUV returns a vector of n random real numbers from a uniform (0,1)
distribution (n <= 128).

This is an auxiliary routine called by DLARNV and ZLARNV.

## Parameters
ISEED : INTEGER array, dimension (4) [in,out]
> On entry, the seed of the random number generator; the array
> elements must be between 0 and 4095, and ISEED(4) must be
> odd.
> On exit, the seed is updated.

N : INTEGER [in]
> The number of random numbers to be generated. N <= 128.

X : DOUBLE PRECISION array, dimension (N) [out]
> The generated random numbers.

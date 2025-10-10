```fortran
subroutine cgeql2 (
        integer m,
        integer n,
        complex, dimension( lda, * ) a,
        integer lda,
        complex, dimension( * ) tau,
        complex, dimension( * ) work,
        integer info
)
```

CGEQL2 computes a QL factorization of a complex m by n matrix A:
A = Q \* L.

## Parameters
M : INTEGER [in]
> The number of rows of the matrix A.  M >= 0.

N : INTEGER [in]
> The number of columns of the matrix A.  N >= 0.

A : COMPLEX array, dimension (LDA,N) [in,out]
> On entry, the m by n matrix A.
> On exit, if m >= n, the lower triangle of the subarray
> A(m-n+1:m,1:n) contains the n by n lower triangular matrix L;
> if m <= n, the elements on and below the (n-m)-th
> superdiagonal contain the m by n lower trapezoidal matrix L;
> the remaining elements, with the array TAU, represent the
> unitary matrix Q as a product of elementary reflectors
> (see Further Details).

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,M).

TAU : COMPLEX array, dimension (min(M,N)) [out]
> The scalar factors of the elementary reflectors (see Further
> Details).

WORK : COMPLEX array, dimension (N) [out]

INFO : INTEGER [out]
> = 0: successful exit
> < 0: if INFO = -i, the i-th argument had an illegal value

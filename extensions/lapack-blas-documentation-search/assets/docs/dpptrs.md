```fortran
subroutine dpptrs (
        character uplo,
        integer n,
        integer nrhs,
        double precision, dimension( * ) ap,
        double precision, dimension( ldb, * ) b,
        integer ldb,
        integer info
)
```

DPPTRS solves a system of linear equations A\*X = B with a symmetric
positive definite matrix A in packed storage using the Cholesky
factorization A = U\*\*T\*U or A = L\*L\*\*T computed by DPPTRF.

## Parameters
UPLO : CHARACTER\*1 [in]
> = 'U':  Upper triangle of A is stored;
> = 'L':  Lower triangle of A is stored.

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of columns
> of the matrix B.  NRHS >= 0.

AP : DOUBLE PRECISION array, dimension (N\*(N+1)/2) [in]
> The triangular factor U or L from the Cholesky factorization
> A = U\*\*T\*U or A = L\*L\*\*T, packed columnwise in a linear
> array.  The j-th column of U or L is stored in the array AP
> as follows:
> if UPLO = 'U', AP(i + (j-1)\*j/2) = U(i,j) for 1<=i<=j;
> if UPLO = 'L', AP(i + (j-1)\*(2n-j)/2) = L(i,j) for j<=i<=n.

B : DOUBLE PRECISION array, dimension (LDB,NRHS) [in,out]
> On entry, the right hand side matrix B.
> On exit, the solution matrix X.

LDB : INTEGER [in]
> The leading dimension of the array B.  LDB >= max(1,N).

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value

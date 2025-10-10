```fortran
subroutine zgttrs (
        character trans,
        integer n,
        integer nrhs,
        complex*16, dimension( * ) dl,
        complex*16, dimension( * ) d,
        complex*16, dimension( * ) du,
        complex*16, dimension( * ) du2,
        integer, dimension( * ) ipiv,
        complex*16, dimension( ldb, * ) b,
        integer ldb,
        integer info
)
```

ZGTTRS solves one of the systems of equations
A \* X = B,  A\*\*T \* X = B,  or  A\*\*H \* X = B,
with a tridiagonal matrix A using the LU factorization computed
by ZGTTRF.

## Parameters
TRANS : CHARACTER\*1 [in]
> Specifies the form of the system of equations.
> = 'N':  A \* X = B     (No transpose)
> = 'T':  A\*\*T \* X = B  (Transpose)
> = 'C':  A\*\*H \* X = B  (Conjugate transpose)

N : INTEGER [in]
> The order of the matrix A.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of columns
> of the matrix B.  NRHS >= 0.

DL : COMPLEX\*16 array, dimension (N-1) [in]
> The (n-1) multipliers that define the matrix L from the
> LU factorization of A.

D : COMPLEX\*16 array, dimension (N) [in]
> The n diagonal elements of the upper triangular matrix U from
> the LU factorization of A.

DU : COMPLEX\*16 array, dimension (N-1) [in]
> The (n-1) elements of the first super-diagonal of U.

DU2 : COMPLEX\*16 array, dimension (N-2) [in]
> The (n-2) elements of the second super-diagonal of U.

IPIV : INTEGER array, dimension (N) [in]
> The pivot indices; for 1 <= i <= n, row i of the matrix was
> interchanged with row IPIV(i).  IPIV(i) will always be either
> i or i+1; IPIV(i) = i indicates a row interchange was not
> required.

B : COMPLEX\*16 array, dimension (LDB,NRHS) [in,out]
> On entry, the matrix of right hand side vectors B.
> On exit, B is overwritten by the solution vectors X.

LDB : INTEGER [in]
> The leading dimension of the array B.  LDB >= max(1,N).

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -k, the k-th argument had an illegal value

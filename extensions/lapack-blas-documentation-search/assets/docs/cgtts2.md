```fortran
subroutine cgtts2 (
        integer itrans,
        integer n,
        integer nrhs,
        complex, dimension( * ) dl,
        complex, dimension( * ) d,
        complex, dimension( * ) du,
        complex, dimension( * ) du2,
        integer, dimension( * ) ipiv,
        complex, dimension( ldb, * ) b,
        integer ldb
)
```

CGTTS2 solves one of the systems of equations
A \* X = B,  A\*\*T \* X = B,  or  A\*\*H \* X = B,
with a tridiagonal matrix A using the LU factorization computed
by CGTTRF.

## Parameters
ITRANS : INTEGER [in]
> Specifies the form of the system of equations.
> = 0:  A \* X = B     (No transpose)
> = 1:  A\*\*T \* X = B  (Transpose)
> = 2:  A\*\*H \* X = B  (Conjugate transpose)

N : INTEGER [in]
> The order of the matrix A.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of columns
> of the matrix B.  NRHS >= 0.

DL : COMPLEX array, dimension (N-1) [in]
> The (n-1) multipliers that define the matrix L from the
> LU factorization of A.

D : COMPLEX array, dimension (N) [in]
> The n diagonal elements of the upper triangular matrix U from
> the LU factorization of A.

DU : COMPLEX array, dimension (N-1) [in]
> The (n-1) elements of the first super-diagonal of U.

DU2 : COMPLEX array, dimension (N-2) [in]
> The (n-2) elements of the second super-diagonal of U.

IPIV : INTEGER array, dimension (N) [in]
> The pivot indices; for 1 <= i <= n, row i of the matrix was
> interchanged with row IPIV(i).  IPIV(i) will always be either
> i or i+1; IPIV(i) = i indicates a row interchange was not
> required.

B : COMPLEX array, dimension (LDB,NRHS) [in,out]
> On entry, the matrix of right hand side vectors B.
> On exit, B is overwritten by the solution vectors X.

LDB : INTEGER [in]
> The leading dimension of the array B.  LDB >= max(1,N).

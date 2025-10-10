```fortran
subroutine clagtm (
        character trans,
        integer n,
        integer nrhs,
        real alpha,
        complex, dimension( * ) dl,
        complex, dimension( * ) d,
        complex, dimension( * ) du,
        complex, dimension( ldx, * ) x,
        integer ldx,
        real beta,
        complex, dimension( ldb, * ) b,
        integer ldb
)
```

CLAGTM performs a matrix-matrix product of the form

B := alpha \* A \* X + beta \* B

where A is a tridiagonal matrix of order N, B and X are N by NRHS
matrices, and alpha and beta are real scalars, each of which may be
0., 1., or -1.

## Parameters
TRANS : CHARACTER\*1 [in]
> Specifies the operation applied to A.
> = 'N':  No transpose, B := alpha \* A \* X + beta \* B
> = 'T':  Transpose,    B := alpha \* A\*\*T \* X + beta \* B
> = 'C':  Conjugate transpose, B := alpha \* A\*\*H \* X + beta \* B

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of columns
> of the matrices X and B.

ALPHA : REAL [in]
> The scalar alpha.  ALPHA must be 0., 1., or -1.; otherwise,
> it is assumed to be 0.

DL : COMPLEX array, dimension (N-1) [in]
> The (n-1) sub-diagonal elements of T.

D : COMPLEX array, dimension (N) [in]
> The diagonal elements of T.

DU : COMPLEX array, dimension (N-1) [in]
> The (n-1) super-diagonal elements of T.

X : COMPLEX array, dimension (LDX,NRHS) [in]
> The N by NRHS matrix X.

LDX : INTEGER [in]
> The leading dimension of the array X.  LDX >= max(N,1).

BETA : REAL [in]
> The scalar beta.  BETA must be 0., 1., or -1.; otherwise,
> it is assumed to be 1.

B : COMPLEX array, dimension (LDB,NRHS) [in,out]
> On entry, the N by NRHS matrix B.
> On exit, B is overwritten by the matrix expression
> B := alpha \* A \* X + beta \* B.

LDB : INTEGER [in]
> The leading dimension of the array B.  LDB >= max(N,1).

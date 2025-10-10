```fortran
subroutine csysv_aa_2stage (
        character uplo,
        integer n,
        integer nrhs,
        complex, dimension( lda, * ) a,
        integer lda,
        complex, dimension( * ) tb,
        integer ltb,
        integer, dimension( * ) ipiv,
        integer, dimension( * ) ipiv2,
        complex, dimension( ldb, * ) b,
        integer ldb,
        complex, dimension( * ) work,
        integer lwork,
        integer info
)
```

CSYSV_AA_2STAGE computes the solution to a complex system of
linear equations
A \* X = B,
where A is an N-by-N symmetric matrix and X and B are N-by-NRHS
matrices.

Aasen's 2-stage algorithm is used to factor A as
A = U\*\*T \* T \* U,  if UPLO = 'U', or
A = L \* T \* L\*\*T,  if UPLO = 'L',
where U (or L) is a product of permutation and unit upper (lower)
triangular matrices, and T is symmetric and band. The matrix T is
then LU-factored with partial pivoting. The factored form of A
is then used to solve the system of equations A \* X = B.

This is the blocked version of the algorithm, calling Level 3 BLAS.

## Parameters
UPLO : CHARACTER\*1 [in]
> = 'U':  Upper triangle of A is stored;
> = 'L':  Lower triangle of A is stored.

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of columns
> of the matrix B.  NRHS >= 0.

A : COMPLEX array, dimension (LDA,N) [in,out]
> On entry, the symmetric matrix A.  If UPLO = 'U', the leading
> N-by-N upper triangular part of A contains the upper
> triangular part of the matrix A, and the strictly lower
> triangular part of A is not referenced.  If UPLO = 'L', the
> leading N-by-N lower triangular part of A contains the lower
> triangular part of the matrix A, and the strictly upper
> triangular part of A is not referenced.
> 
> On exit, L is stored below (or above) the subdiagonal blocks,
> when UPLO  is 'L' (or 'U').

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

TB : COMPLEX array, dimension (LTB) [out]
> On exit, details of the LU factorization of the band matrix.

LTB : INTEGER [in]
> The size of the array TB. LTB >= 4\*N, internally
> used to select NB such that LTB >= (3\*NB+1)\*N.
> 
> If LTB = -1, then a workspace query is assumed; the
> routine only calculates the optimal size of LTB,
> returns this value as the first entry of TB, and
> no error message related to LTB is issued by XERBLA.

IPIV : INTEGER array, dimension (N) [out]
> On exit, it contains the details of the interchanges, i.e.,
> the row and column k of A were interchanged with the
> row and column IPIV(k).

IPIV2 : INTEGER array, dimension (N) [out]
> On exit, it contains the details of the interchanges, i.e.,
> the row and column k of T were interchanged with the
> row and column IPIV(k).

B : COMPLEX array, dimension (LDB,NRHS) [in,out]
> On entry, the right hand side matrix B.
> On exit, the solution matrix X.

LDB : INTEGER [in]
> The leading dimension of the array B.  LDB >= max(1,N).

WORK : COMPLEX workspace of size LWORK [out]

LWORK : INTEGER [in]
> The size of WORK. LWORK >= N, internally used to select NB
> such that LWORK >= N\*NB.
> 
> If LWORK = -1, then a workspace query is assumed; the
> routine only calculates the optimal size of the WORK array,
> returns this value as the first entry of the WORK array, and
> no error message related to LWORK is issued by XERBLA.

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value.
> > 0:  if INFO = i, band LU factorization failed on i-th column

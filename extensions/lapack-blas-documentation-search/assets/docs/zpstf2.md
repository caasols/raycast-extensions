```fortran
subroutine zpstf2 (
        character uplo,
        integer n,
        complex*16, dimension( lda, * ) a,
        integer lda,
        integer, dimension( n ) piv,
        integer rank,
        double precision tol,
        double precision, dimension( 2*n ) work,
        integer info
)
```

ZPSTF2 computes the Cholesky factorization with complete
pivoting of a complex Hermitian positive semidefinite matrix A.

The factorization has the form
P\*\*T \* A \* P = U\*\*H \* U ,  if UPLO = 'U',
P\*\*T \* A \* P = L  \* L\*\*H,  if UPLO = 'L',
where U is an upper triangular matrix and L is lower triangular, and
P is stored as vector PIV.

This algorithm does not attempt to check that A is positive
semidefinite. This version of the algorithm calls level 2 BLAS.

## Parameters
UPLO : CHARACTER\*1 [in]
> Specifies whether the upper or lower triangular part of the
> symmetric matrix A is stored.
> = 'U':  Upper triangular
> = 'L':  Lower triangular

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

A : COMPLEX\*16 array, dimension (LDA,N) [in,out]
> On entry, the symmetric matrix A.  If UPLO = 'U', the leading
> n by n upper triangular part of A contains the upper
> triangular part of the matrix A, and the strictly lower
> triangular part of A is not referenced.  If UPLO = 'L', the
> leading n by n lower triangular part of A contains the lower
> triangular part of the matrix A, and the strictly upper
> triangular part of A is not referenced.
> 
> On exit, if INFO = 0, the factor U or L from the Cholesky
> factorization as above.

PIV : INTEGER array, dimension (N) [out]
> PIV is such that the nonzero entries are P( PIV(K), K ) = 1.

RANK : INTEGER [out]
> The rank of A given by the number of steps the algorithm
> completed.

TOL : DOUBLE PRECISION [in]
> User defined tolerance. If TOL < 0, then N\*U\*MAX( A( K,K ) )
> will be used. The algorithm terminates at the (K-1)st step
> if the pivot <= TOL.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

WORK : DOUBLE PRECISION array, dimension (2\*N) [out]
> Work space.

INFO : INTEGER [out]
> < 0: If INFO = -K, the K-th argument had an illegal value,
> = 0: algorithm completed successfully, and
> > 0: the matrix A is either rank deficient with computed rank
> as returned in RANK, or is not positive semidefinite. See
> Section 7 of LAPACK Working Note #161 for further
> information.

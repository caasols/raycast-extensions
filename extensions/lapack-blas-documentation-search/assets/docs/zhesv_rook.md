```fortran
subroutine zhesv_rook (
        character uplo,
        integer n,
        integer nrhs,
        complex*16, dimension( lda, * ) a,
        integer lda,
        integer, dimension( * ) ipiv,
        complex*16, dimension( ldb, * ) b,
        integer ldb,
        complex*16, dimension( * ) work,
        integer lwork,
        integer info
)
```

ZHESV_ROOK computes the solution to a complex system of linear equations
A \* X = B,
where A is an N-by-N Hermitian matrix and X and B are N-by-NRHS
matrices.

The bounded Bunch-Kaufman () diagonal pivoting method is used
to factor A as
A = U \* D \* U\*\*T,  if UPLO = 'U', or
A = L \* D \* L\*\*T,  if UPLO = 'L',
where U (or L) is a product of permutation and unit upper (lower)
triangular matrices, and D is Hermitian and block diagonal with
1-by-1 and 2-by-2 diagonal blocks.

ZHETRF_ROOK is called to compute the factorization of a complex
Hermition matrix A using the bounded Bunch-Kaufman () diagonal
pivoting method.

The factored form of A is then used to solve the system
of equations A \* X = B by calling ZHETRS_ROOK (uses BLAS 2).

## Parameters
UPLO : CHARACTER\*1 [in]
> = 'U':  Upper triangle of A is stored;
> = 'L':  Lower triangle of A is stored.

N : INTEGER [in]
> The number of linear equations, i.e., the order of the
> matrix A.  N >= 0.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of columns
> of the matrix B.  NRHS >= 0.

A : COMPLEX\*16 array, dimension (LDA,N) [in,out]
> On entry, the Hermitian matrix A.  If UPLO = 'U', the leading
> N-by-N upper triangular part of A contains the upper
> triangular part of the matrix A, and the strictly lower
> triangular part of A is not referenced.  If UPLO = 'L', the
> leading N-by-N lower triangular part of A contains the lower
> triangular part of the matrix A, and the strictly upper
> triangular part of A is not referenced.
> 
> On exit, if INFO = 0, the block diagonal matrix D and the
> multipliers used to obtain the factor U or L from the
> factorization A = U\*D\*U\*\*H or A = L\*D\*L\*\*H as computed by
> ZHETRF_ROOK.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

IPIV : INTEGER array, dimension (N) [out]
> Details of the interchanges and the block structure of D.
> 
> If UPLO = 'U':
> Only the last KB elements of IPIV are set.
> 
> If IPIV(k) > 0, then rows and columns k and IPIV(k) were
> interchanged and D(k,k) is a 1-by-1 diagonal block.
> 
> If IPIV(k) < 0 and IPIV(k-1) < 0, then rows and
> columns k and -IPIV(k) were interchanged and rows and
> columns k-1 and -IPIV(k-1) were inerchaged,
> D(k-1:k,k-1:k) is a 2-by-2 diagonal block.
> 
> If UPLO = 'L':
> Only the first KB elements of IPIV are set.
> 
> If IPIV(k) > 0, then rows and columns k and IPIV(k)
> were interchanged and D(k,k) is a 1-by-1 diagonal block.
> 
> If IPIV(k) < 0 and IPIV(k+1) < 0, then rows and
> columns k and -IPIV(k) were interchanged and rows and
> columns k+1 and -IPIV(k+1) were inerchaged,
> D(k:k+1,k:k+1) is a 2-by-2 diagonal block.

B : COMPLEX\*16 array, dimension (LDB,NRHS) [in,out]
> On entry, the N-by-NRHS right hand side matrix B.
> On exit, if INFO = 0, the N-by-NRHS solution matrix X.

LDB : INTEGER [in]
> The leading dimension of the array B.  LDB >= max(1,N).

WORK : COMPLEX\*16 array, dimension (MAX(1,LWORK)) [out]
> On exit, if INFO = 0, WORK(1) returns the optimal LWORK.

LWORK : INTEGER [in]
> The length of WORK.  LWORK >= 1, and for best performance
> LWORK >= max(1,N\*NB), where NB is the optimal blocksize for
> ZHETRF_ROOK.
> for LWORK < N, TRS will be done with Level BLAS 2
> for LWORK >= N, TRS will be done with Level BLAS 3
> 
> If LWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal size of the WORK array, returns
> this value as the first entry of the WORK array, and no error
> message related to LWORK is issued by XERBLA.

INFO : INTEGER [out]
> = 0: successful exit
> < 0: if INFO = -i, the i-th argument had an illegal value
> > 0: if INFO = i, D(i,i) is exactly zero.  The factorization
> has been completed, but the block diagonal matrix D is
> exactly singular, so the solution could not be computed.

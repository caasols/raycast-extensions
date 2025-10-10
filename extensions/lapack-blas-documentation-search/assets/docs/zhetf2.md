```fortran
subroutine zhetf2 (
        character uplo,
        integer n,
        complex*16, dimension( lda, * ) a,
        integer lda,
        integer, dimension( * ) ipiv,
        integer info
)
```

ZHETF2 computes the factorization of a complex Hermitian matrix A
using the Bunch-Kaufman diagonal pivoting method:

A = U\*D\*U\*\*H  or  A = L\*D\*L\*\*H

where U (or L) is a product of permutation and unit upper (lower)
triangular matrices, U\*\*H is the conjugate transpose of U, and D is
Hermitian and block diagonal with 1-by-1 and 2-by-2 diagonal blocks.

This is the unblocked version of the algorithm, calling Level 2 BLAS.

## Parameters
UPLO : CHARACTER\*1 [in]
> Specifies whether the upper or lower triangular part of the
> Hermitian matrix A is stored:
> = 'U':  Upper triangular
> = 'L':  Lower triangular

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

A : COMPLEX\*16 array, dimension (LDA,N) [in,out]
> On entry, the Hermitian matrix A.  If UPLO = 'U', the leading
> n-by-n upper triangular part of A contains the upper
> triangular part of the matrix A, and the strictly lower
> triangular part of A is not referenced.  If UPLO = 'L', the
> leading n-by-n lower triangular part of A contains the lower
> triangular part of the matrix A, and the strictly upper
> triangular part of A is not referenced.
> 
> On exit, the block diagonal matrix D and the multipliers used
> to obtain the factor U or L (see below for further details).

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

IPIV : INTEGER array, dimension (N) [out]
> Details of the interchanges and the block structure of D.
> 
> If UPLO = 'U':
> If IPIV(k) > 0, then rows and columns k and IPIV(k) were
> interchanged and D(k,k) is a 1-by-1 diagonal block.
> 
> If IPIV(k) = IPIV(k-1) < 0, then rows and columns
> k-1 and -IPIV(k) were interchanged and D(k-1:k,k-1:k)
> is a 2-by-2 diagonal block.
> 
> If UPLO = 'L':
> If IPIV(k) > 0, then rows and columns k and IPIV(k) were
> interchanged and D(k,k) is a 1-by-1 diagonal block.
> 
> If IPIV(k) = IPIV(k+1) < 0, then rows and columns
> k+1 and -IPIV(k) were interchanged and D(k:k+1,k:k+1)
> is a 2-by-2 diagonal block.

INFO : INTEGER [out]
> = 0: successful exit
> < 0: if INFO = -k, the k-th argument had an illegal value
> > 0: if INFO = k, D(k,k) is exactly zero.  The factorization
> has been completed, but the block diagonal matrix D is
> exactly singular, and division by zero will occur if it
> is used to solve a system of equations.

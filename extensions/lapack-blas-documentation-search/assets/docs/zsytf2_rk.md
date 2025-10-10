```fortran
subroutine zsytf2_rk (
        character uplo,
        integer n,
        complex*16, dimension( lda, * ) a,
        integer lda,
        complex*16, dimension( * ) e,
        integer, dimension( * ) ipiv,
        integer info
)
```

ZSYTF2_RK computes the factorization of a complex symmetric matrix A
using the bounded Bunch-Kaufman (rook) diagonal pivoting method:

A = P\*U\*D\*(U\*\*T)\*(P\*\*T) or A = P\*L\*D\*(L\*\*T)\*(P\*\*T),

where U (or L) is unit upper (or lower) triangular matrix,
U\*\*T (or L\*\*T) is the transpose of U (or L), P is a permutation
matrix, P\*\*T is the transpose of P, and D is symmetric and block
diagonal with 1-by-1 and 2-by-2 diagonal blocks.

This is the unblocked version of the algorithm, calling Level 2 BLAS.
For more information see Further Details section.

## Parameters
UPLO : CHARACTER\*1 [in]
> Specifies whether the upper or lower triangular part of the
> symmetric matrix A is stored:
> = 'U':  Upper triangular
> = 'L':  Lower triangular

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

A : COMPLEX\*16 array, dimension (LDA,N) [in,out]
> On entry, the symmetric matrix A.
> If UPLO = 'U': the leading N-by-N upper triangular part
> of A contains the upper triangular part of the matrix A,
> and the strictly lower triangular part of A is not
> referenced.
> 
> If UPLO = 'L': the leading N-by-N lower triangular part
> of A contains the lower triangular part of the matrix A,
> and the strictly upper triangular part of A is not
> referenced.
> 
> On exit, contains:
> a) ONLY diagonal elements of the symmetric block diagonal
> matrix D on the diagonal of A, i.e. D(k,k) = A(k,k);
> (superdiagonal (or subdiagonal) elements of D
> are stored on exit in array E), and
> b) If UPLO = 'U': factor U in the superdiagonal part of A.
> If UPLO = 'L': factor L in the subdiagonal part of A.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

E : COMPLEX\*16 array, dimension (N) [out]
> On exit, contains the superdiagonal (or subdiagonal)
> elements of the symmetric block diagonal matrix D
> with 1-by-1 or 2-by-2 diagonal blocks, where
> If UPLO = 'U': E(i) = D(i-1,i), i=2:N, E(1) is set to 0;
> If UPLO = 'L': E(i) = D(i+1,i), i=1:N-1, E(N) is set to 0.
> 
> NOTE: For 1-by-1 diagonal block D(k), where
> 1 <= k <= N, the element E(k) is set to 0 in both
> UPLO = 'U' or UPLO = 'L' cases.

IPIV : INTEGER array, dimension (N) [out]
> IPIV describes the permutation matrix P in the factorization
> of matrix A as follows. The absolute value of IPIV(k)
> represents the index of row and column that were
> interchanged with the k-th row and column. The value of UPLO
> describes the order in which the interchanges were applied.
> Also, the sign of IPIV represents the block structure of
> the symmetric block diagonal matrix D with 1-by-1 or 2-by-2
> diagonal blocks which correspond to 1 or 2 interchanges
> at each factorization step. For more info see Further
> Details section.
> 
> If UPLO = 'U',
> ( in factorization order, k decreases from N to 1 ):
> a) A single positive entry IPIV(k) > 0 means:
> D(k,k) is a 1-by-1 diagonal block.
> If IPIV(k) != k, rows and columns k and IPIV(k) were
> interchanged in the matrix A(1:N,1:N);
> If IPIV(k) = k, no interchange occurred.
> 
> b) A pair of consecutive negative entries
> IPIV(k) < 0 and IPIV(k-1) < 0 means:
> D(k-1:k,k-1:k) is a 2-by-2 diagonal block.
> (NOTE: negative entries in IPIV appear ONLY in pairs).
> 1) If -IPIV(k) != k, rows and columns
> k and -IPIV(k) were interchanged
> in the matrix A(1:N,1:N).
> If -IPIV(k) = k, no interchange occurred.
> 2) If -IPIV(k-1) != k-1, rows and columns
> k-1 and -IPIV(k-1) were interchanged
> in the matrix A(1:N,1:N).
> If -IPIV(k-1) = k-1, no interchange occurred.
> 
> c) In both cases a) and b), always ABS( IPIV(k) ) <= k.
> 
> d) NOTE: Any entry IPIV(k) is always NONZERO on output.
> 
> If UPLO = 'L',
> ( in factorization order, k increases from 1 to N ):
> a) A single positive entry IPIV(k) > 0 means:
> D(k,k) is a 1-by-1 diagonal block.
> If IPIV(k) != k, rows and columns k and IPIV(k) were
> interchanged in the matrix A(1:N,1:N).
> If IPIV(k) = k, no interchange occurred.
> 
> b) A pair of consecutive negative entries
> IPIV(k) < 0 and IPIV(k+1) < 0 means:
> D(k:k+1,k:k+1) is a 2-by-2 diagonal block.
> (NOTE: negative entries in IPIV appear ONLY in pairs).
> 1) If -IPIV(k) != k, rows and columns
> k and -IPIV(k) were interchanged
> in the matrix A(1:N,1:N).
> If -IPIV(k) = k, no interchange occurred.
> 2) If -IPIV(k+1) != k+1, rows and columns
> k-1 and -IPIV(k-1) were interchanged
> in the matrix A(1:N,1:N).
> If -IPIV(k+1) = k+1, no interchange occurred.
> 
> c) In both cases a) and b), always ABS( IPIV(k) ) >= k.
> 
> d) NOTE: Any entry IPIV(k) is always NONZERO on output.

INFO : INTEGER [out]
> = 0: successful exit
> 
> < 0: If INFO = -k, the k-th argument had an illegal value
> 
> > 0: If INFO = k, the matrix A is singular, because:
> If UPLO = 'U': column k in the upper
> triangular part of A contains all zeros.
> If UPLO = 'L': column k in the lower
> triangular part of A contains all zeros.
> 
> Therefore D(k,k) is exactly zero, and superdiagonal
> elements of column k of U (or subdiagonal elements of
> column k of L ) are all zeros. The factorization has
> been completed, but the block diagonal matrix D is
> exactly singular, and division by zero will occur if
> it is used to solve a system of equations.
> 
> NOTE: INFO only stores the first occurrence of
> a singularity, any subsequent occurrence of singularity
> is not stored in INFO even though the factorization
> always completes.

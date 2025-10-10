```fortran
subroutine zhetri2x (
        character uplo,
        integer n,
        complex*16, dimension( lda, * ) a,
        integer lda,
        integer, dimension( * ) ipiv,
        complex*16, dimension( n+nb+1,* ) work,
        integer nb,
        integer info
)
```

ZHETRI2X computes the inverse of a COMPLEX\*16 Hermitian indefinite matrix
A using the factorization A = U\*D\*U\*\*H or A = L\*D\*L\*\*H computed by
ZHETRF.

## Parameters
UPLO : CHARACTER\*1 [in]
> Specifies whether the details of the factorization are stored
> as an upper or lower triangular matrix.
> = 'U':  Upper triangular, form is A = U\*D\*U\*\*H;
> = 'L':  Lower triangular, form is A = L\*D\*L\*\*H.

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

A : COMPLEX\*16 array, dimension (LDA,N) [in,out]
> On entry, the NNB diagonal matrix D and the multipliers
> used to obtain the factor U or L as computed by ZHETRF.
> 
> On exit, if INFO = 0, the (symmetric) inverse of the original
> matrix.  If UPLO = 'U', the upper triangular part of the
> inverse is formed and the part of A below the diagonal is not
> referenced; if UPLO = 'L' the lower triangular part of the
> inverse is formed and the part of A above the diagonal is
> not referenced.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

IPIV : INTEGER array, dimension (N) [in]
> Details of the interchanges and the NNB structure of D
> as determined by ZHETRF.

WORK : COMPLEX\*16 array, dimension (N+NB+1,NB+3) [out]

NB : INTEGER [in]
> Block size

INFO : INTEGER [out]
> = 0: successful exit
> < 0: if INFO = -i, the i-th argument had an illegal value
> > 0: if INFO = i, D(i,i) = 0; the matrix is singular and its
> inverse could not be computed.

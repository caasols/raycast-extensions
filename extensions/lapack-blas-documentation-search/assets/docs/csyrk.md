```fortran
subroutine csyrk (
        character uplo,
        character trans,
        integer n,
        integer k,
        complex alpha,
        complex, dimension(lda,*) a,
        integer lda,
        complex beta,
        complex, dimension(ldc,*) c,
        integer ldc
)
```

CSYRK  performs one of the symmetric rank k operations

C := alpha\*A\*A\*\*T + beta\*C,

or

C := alpha\*A\*\*T\*A + beta\*C,

where  alpha and beta  are scalars,  C is an  n by n symmetric matrix
and  A  is an  n by k  matrix in the first case and a  k by n  matrix
in the second case.

## Parameters
UPLO : CHARACTER\*1 [in]
> On  entry,   UPLO  specifies  whether  the  upper  or  lower
> triangular  part  of the  array  C  is to be  referenced  as
> follows:
> 
> UPLO = 'U' or 'u'   Only the  upper triangular part of  C
> is to be referenced.
> 
> UPLO = 'L' or 'l'   Only the  lower triangular part of  C
> is to be referenced.

TRANS : CHARACTER\*1 [in]
> On entry,  TRANS  specifies the operation to be performed as
> follows:
> 
> TRANS = 'N' or 'n'   C := alpha\*A\*A\*\*T + beta\*C.
> 
> TRANS = 'T' or 't'   C := alpha\*A\*\*T\*A + beta\*C.

N : INTEGER [in]
> On entry,  N specifies the order of the matrix C.  N must be
> at least zero.

K : INTEGER [in]
> On entry with  TRANS = 'N' or 'n',  K  specifies  the number
> of  columns   of  the   matrix   A,   and  on   entry   with
> TRANS = 'T' or 't',  K  specifies  the number of rows of the
> matrix A.  K must be at least zero.

ALPHA : COMPLEX [in]
> On entry, ALPHA specifies the scalar alpha.

A : COMPLEX array, dimension ( LDA, ka ), where ka is [in]
> k  when  TRANS = 'N' or 'n',  and is  n  otherwise.
> Before entry with  TRANS = 'N' or 'n',  the  leading  n by k
> part of the array  A  must contain the matrix  A,  otherwise
> the leading  k by n  part of the array  A  must contain  the
> matrix A.

LDA : INTEGER [in]
> On entry, LDA specifies the first dimension of A as declared
> in  the  calling  (sub)  program.   When  TRANS = 'N' or 'n'
> then  LDA must be at least  max( 1, n ), otherwise  LDA must
> be at least  max( 1, k ).

BETA : COMPLEX [in]
> On entry, BETA specifies the scalar beta.

C : COMPLEX array, dimension ( LDC, N ) [in,out]
> Before entry  with  UPLO = 'U' or 'u',  the leading  n by n
> upper triangular part of the array C must contain the upper
> triangular part  of the  symmetric matrix  and the strictly
> lower triangular part of C is not referenced.  On exit, the
> upper triangular part of the array  C is overwritten by the
> upper triangular part of the updated matrix.
> Before entry  with  UPLO = 'L' or 'l',  the leading  n by n
> lower triangular part of the array C must contain the lower
> triangular part  of the  symmetric matrix  and the strictly
> upper triangular part of C is not referenced.  On exit, the
> lower triangular part of the array  C is overwritten by the
> lower triangular part of the updated matrix.

LDC : INTEGER [in]
> On entry, LDC specifies the first dimension of C as declared
> in  the  calling  (sub)  program.   LDC  must  be  at  least
> max( 1, n ).

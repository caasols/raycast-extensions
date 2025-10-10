```fortran
subroutine clascl (
        character type,
        integer kl,
        integer ku,
        real cfrom,
        real cto,
        integer m,
        integer n,
        complex, dimension( lda, * ) a,
        integer lda,
        integer info
)
```

CLASCL multiplies the M by N complex matrix A by the real scalar
CTO/CFROM.  This is done without over/underflow as long as the final
result CTO\*A(I,J)/CFROM does not over/underflow. TYPE specifies that
A may be full, upper triangular, lower triangular, upper Hessenberg,
or banded.

## Parameters
TYPE : CHARACTER\*1 [in]
> TYPE indices the storage type of the input matrix.
> = 'G':  A is a full matrix.
> = 'L':  A is a lower triangular matrix.
> = 'U':  A is an upper triangular matrix.
> = 'H':  A is an upper Hessenberg matrix.
> = 'B':  A is a symmetric band matrix with lower bandwidth KL
> and upper bandwidth KU and with the only the lower
> half stored.
> = 'Q':  A is a symmetric band matrix with lower bandwidth KL
> and upper bandwidth KU and with the only the upper
> half stored.
> = 'Z':  A is a band matrix with lower bandwidth KL and upper
> bandwidth KU. See CGBTRF for storage details.

KL : INTEGER [in]
> The lower bandwidth of A.  Referenced only if TYPE = 'B',
> 'Q' or 'Z'.

KU : INTEGER [in]
> The upper bandwidth of A.  Referenced only if TYPE = 'B',
> 'Q' or 'Z'.

CFROM : REAL [in]

CTO : REAL [in]
> 
> The matrix A is multiplied by CTO/CFROM. A(I,J) is computed
> without over/underflow if the final result CTO\*A(I,J)/CFROM
> can be represented without over/underflow.  CFROM must be
> nonzero.

M : INTEGER [in]
> The number of rows of the matrix A.  M >= 0.

N : INTEGER [in]
> The number of columns of the matrix A.  N >= 0.

A : COMPLEX array, dimension (LDA,N) [in,out]
> The matrix to be multiplied by CTO/CFROM.  See TYPE for the
> storage type.

LDA : INTEGER [in]
> The leading dimension of the array A.
> If TYPE = 'G', 'L', 'U', 'H', LDA >= max(1,M);
> TYPE = 'B', LDA >= KL+1;
> TYPE = 'Q', LDA >= KU+1;
> TYPE = 'Z', LDA >= 2\*KL+KU+1.

INFO : INTEGER [out]
> 0  - successful exit
> <0 - if INFO = -i, the i-th argument had an illegal value.

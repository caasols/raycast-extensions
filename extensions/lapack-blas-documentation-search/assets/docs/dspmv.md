```fortran
subroutine dspmv (
        character uplo,
        integer n,
        double precision alpha,
        double precision, dimension(*) ap,
        double precision, dimension(*) x,
        integer incx,
        double precision beta,
        double precision, dimension(*) y,
        integer incy
)
```

DSPMV  performs the matrix-vector operation

y := alpha\*A\*x + beta\*y,

where alpha and beta are scalars, x and y are n element vectors and
A is an n by n symmetric matrix, supplied in packed form.

## Parameters
UPLO : CHARACTER\*1 [in]
> On entry, UPLO specifies whether the upper or lower
> triangular part of the matrix A is supplied in the packed
> array AP as follows:
> 
> UPLO = 'U' or 'u'   The upper triangular part of A is
> supplied in AP.
> 
> UPLO = 'L' or 'l'   The lower triangular part of A is
> supplied in AP.

N : INTEGER [in]
> On entry, N specifies the order of the matrix A.
> N must be at least zero.

ALPHA : DOUBLE PRECISION. [in]
> On entry, ALPHA specifies the scalar alpha.

AP : DOUBLE PRECISION array, dimension at least [in]
> ( ( n\*( n + 1 ) )/2 ).
> Before entry with UPLO = 'U' or 'u', the array AP must
> contain the upper triangular part of the symmetric matrix
> packed sequentially, column by column, so that AP( 1 )
> contains a( 1, 1 ), AP( 2 ) and AP( 3 ) contain a( 1, 2 )
> and a( 2, 2 ) respectively, and so on.
> Before entry with UPLO = 'L' or 'l', the array AP must
> contain the lower triangular part of the symmetric matrix
> packed sequentially, column by column, so that AP( 1 )
> contains a( 1, 1 ), AP( 2 ) and AP( 3 ) contain a( 2, 1 )
> and a( 3, 1 ) respectively, and so on.

X : DOUBLE PRECISION array, dimension at least [in]
> ( 1 + ( n - 1 )\*abs( INCX ) ).
> Before entry, the incremented array X must contain the n
> element vector x.

INCX : INTEGER [in]
> On entry, INCX specifies the increment for the elements of
> X. INCX must not be zero.

BETA : DOUBLE PRECISION. [in]
> On entry, BETA specifies the scalar beta. When BETA is
> supplied as zero then Y need not be set on input.

Y : DOUBLE PRECISION array, dimension at least [in,out]
> ( 1 + ( n - 1 )\*abs( INCY ) ).
> Before entry, the incremented array Y must contain the n
> element vector y. On exit, Y is overwritten by the updated
> vector y.

INCY : INTEGER [in]
> On entry, INCY specifies the increment for the elements of
> Y. INCY must not be zero.

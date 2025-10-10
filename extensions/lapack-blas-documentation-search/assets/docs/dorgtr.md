```fortran
subroutine dorgtr (
        character uplo,
        integer n,
        double precision, dimension( lda, * ) a,
        integer lda,
        double precision, dimension( * ) tau,
        double precision, dimension( * ) work,
        integer lwork,
        integer info
)
```

DORGTR generates a real orthogonal matrix Q which is defined as the
product of n-1 elementary reflectors of order N, as returned by
DSYTRD:

if UPLO = 'U', Q = H(n-1) . . . H(2) H(1),

if UPLO = 'L', Q = H(1) H(2) . . . H(n-1).

## Parameters
UPLO : CHARACTER\*1 [in]
> = 'U': Upper triangle of A contains elementary reflectors
> from DSYTRD;
> = 'L': Lower triangle of A contains elementary reflectors
> from DSYTRD.

N : INTEGER [in]
> The order of the matrix Q. N >= 0.

A : DOUBLE PRECISION array, dimension (LDA,N) [in,out]
> On entry, the vectors which define the elementary reflectors,
> as returned by DSYTRD.
> On exit, the N-by-N orthogonal matrix Q.

LDA : INTEGER [in]
> The leading dimension of the array A. LDA >= max(1,N).

TAU : DOUBLE PRECISION array, dimension (N-1) [in]
> TAU(i) must contain the scalar factor of the elementary
> reflector H(i), as returned by DSYTRD.

WORK : DOUBLE PRECISION array, dimension (MAX(1,LWORK)) [out]
> On exit, if INFO = 0, WORK(1) returns the optimal LWORK.

LWORK : INTEGER [in]
> The dimension of the array WORK. LWORK >= max(1,N-1).
> For optimum performance LWORK >= (N-1)\*NB, where NB is
> the optimal blocksize.
> 
> If LWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal size of the WORK array, returns
> this value as the first entry of the WORK array, and no error
> message related to LWORK is issued by XERBLA.

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value

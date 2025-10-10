```fortran
subroutine cgehd2 (
        integer n,
        integer ilo,
        integer ihi,
        complex, dimension( lda, * ) a,
        integer lda,
        complex, dimension( * ) tau,
        complex, dimension( * ) work,
        integer info
)
```

CGEHD2 reduces a complex general matrix A to upper Hessenberg form H
by a unitary similarity transformation:  Q\*\*H \* A \* Q = H .

## Parameters
N : INTEGER [in]
> The order of the matrix A.  N >= 0.

ILO : INTEGER [in]

IHI : INTEGER [in]
> 
> It is assumed that A is already upper triangular in rows
> and columns 1:ILO-1 and IHI+1:N. ILO and IHI are normally
> set by a previous call to CGEBAL; otherwise they should be
> set to 1 and N respectively. See Further Details.
> 1 <= ILO <= IHI <= max(1,N).

A : COMPLEX array, dimension (LDA,N) [in,out]
> On entry, the n by n general matrix to be reduced.
> On exit, the upper triangle and the first subdiagonal of A
> are overwritten with the upper Hessenberg matrix H, and the
> elements below the first subdiagonal, with the array TAU,
> represent the unitary matrix Q as a product of elementary
> reflectors. See Further Details.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

TAU : COMPLEX array, dimension (N-1) [out]
> The scalar factors of the elementary reflectors (see Further
> Details).

WORK : COMPLEX array, dimension (N) [out]

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value.

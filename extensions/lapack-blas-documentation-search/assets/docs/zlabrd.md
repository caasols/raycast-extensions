```fortran
subroutine zlabrd (
        integer m,
        integer n,
        integer nb,
        complex*16, dimension( lda, * ) a,
        integer lda,
        double precision, dimension( * ) d,
        double precision, dimension( * ) e,
        complex*16, dimension( * ) tauq,
        complex*16, dimension( * ) taup,
        complex*16, dimension( ldx, * ) x,
        integer ldx,
        complex*16, dimension( ldy, * ) y,
        integer ldy
)
```

ZLABRD reduces the first NB rows and columns of a complex general
m by n matrix A to upper or lower real bidiagonal form by a unitary
transformation Q\*\*H \* A \* P, and returns the matrices X and Y which
are needed to apply the transformation to the unreduced part of A.

If m >= n, A is reduced to upper bidiagonal form; if m < n, to lower
bidiagonal form.

This is an auxiliary routine called by ZGEBRD

## Parameters
M : INTEGER [in]
> The number of rows in the matrix A.

N : INTEGER [in]
> The number of columns in the matrix A.

NB : INTEGER [in]
> The number of leading rows and columns of A to be reduced.

A : COMPLEX\*16 array, dimension (LDA,N) [in,out]
> On entry, the m by n general matrix to be reduced.
> On exit, the first NB rows and columns of the matrix are
> overwritten; the rest of the array is unchanged.
> If m >= n, elements on and below the diagonal in the first NB
> columns, with the array TAUQ, represent the unitary
> matrix Q as a product of elementary reflectors; and
> elements above the diagonal in the first NB rows, with the
> array TAUP, represent the unitary matrix P as a product
> of elementary reflectors.
> If m < n, elements below the diagonal in the first NB
> columns, with the array TAUQ, represent the unitary
> matrix Q as a product of elementary reflectors, and
> elements on and above the diagonal in the first NB rows,
> with the array TAUP, represent the unitary matrix P as
> a product of elementary reflectors.
> See Further Details.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,M).

D : DOUBLE PRECISION array, dimension (NB) [out]
> The diagonal elements of the first NB rows and columns of
> the reduced matrix.  D(i) = A(i,i).

E : DOUBLE PRECISION array, dimension (NB) [out]
> The off-diagonal elements of the first NB rows and columns of
> the reduced matrix.

TAUQ : COMPLEX\*16 array, dimension (NB) [out]
> The scalar factors of the elementary reflectors which
> represent the unitary matrix Q. See Further Details.

TAUP : COMPLEX\*16 array, dimension (NB) [out]
> The scalar factors of the elementary reflectors which
> represent the unitary matrix P. See Further Details.

X : COMPLEX\*16 array, dimension (LDX,NB) [out]
> The m-by-nb matrix X required to update the unreduced part
> of A.

LDX : INTEGER [in]
> The leading dimension of the array X. LDX >= max(1,M).

Y : COMPLEX\*16 array, dimension (LDY,NB) [out]
> The n-by-nb matrix Y required to update the unreduced part
> of A.

LDY : INTEGER [in]
> The leading dimension of the array Y. LDY >= max(1,N).

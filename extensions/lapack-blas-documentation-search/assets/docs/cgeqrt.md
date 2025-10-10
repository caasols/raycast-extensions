```fortran
subroutine cgeqrt (
        integer m,
        integer n,
        integer nb,
        complex, dimension( lda, * ) a,
        integer lda,
        complex, dimension( ldt, * ) t,
        integer ldt,
        complex, dimension( * ) work,
        integer info
)
```

CGEQRT computes a blocked QR factorization of a complex M-by-N matrix A
using the compact WY representation of Q.

## Parameters
M : INTEGER [in]
> The number of rows of the matrix A.  M >= 0.

N : INTEGER [in]
> The number of columns of the matrix A.  N >= 0.

NB : INTEGER [in]
> The block size to be used in the blocked QR.  MIN(M,N) >= NB >= 1.

A : COMPLEX array, dimension (LDA,N) [in,out]
> On entry, the M-by-N matrix A.
> On exit, the elements on and above the diagonal of the array
> contain the min(M,N)-by-N upper trapezoidal matrix R (R is
> upper triangular if M >= N); the elements below the diagonal
> are the columns of V.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,M).

T : COMPLEX array, dimension (LDT,MIN(M,N)) [out]
> The upper triangular block reflectors stored in compact form
> as a sequence of upper triangular blocks.  See below
> for further details.

LDT : INTEGER [in]
> The leading dimension of the array T.  LDT >= NB.

WORK : COMPLEX array, dimension (NB\*N) [out]

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value

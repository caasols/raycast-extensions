```fortran
subroutine claqps (
        integer m,
        integer n,
        integer offset,
        integer nb,
        integer kb,
        complex, dimension( lda, * ) a,
        integer lda,
        integer, dimension( * ) jpvt,
        complex, dimension( * ) tau,
        real, dimension( * ) vn1,
        real, dimension( * ) vn2,
        complex, dimension( * ) auxv,
        complex, dimension( ldf, * ) f,
        integer ldf
)
```

CLAQPS computes a step of QR factorization with column pivoting
of a complex M-by-N matrix A by using Blas-3.  It tries to factorize
NB columns from A starting from the row OFFSET+1, and updates all
of the matrix with Blas-3 xGEMM.

In some cases, due to catastrophic cancellations, it cannot
factorize NB columns.  Hence, the actual number of factorized
columns is returned in KB.

Block A(1:OFFSET,1:N) is accordingly pivoted, but not factorized.

## Parameters
M : INTEGER [in]
> The number of rows of the matrix A. M >= 0.

N : INTEGER [in]
> The number of columns of the matrix A. N >= 0

OFFSET : INTEGER [in]
> The number of rows of A that have been factorized in
> previous steps.

NB : INTEGER [in]
> The number of columns to factorize.

KB : INTEGER [out]
> The number of columns actually factorized.

A : COMPLEX array, dimension (LDA,N) [in,out]
> On entry, the M-by-N matrix A.
> On exit, block A(OFFSET+1:M,1:KB) is the triangular
> factor obtained and block A(1:OFFSET,1:N) has been
> accordingly pivoted, but no factorized.
> The rest of the matrix, block A(OFFSET+1:M,KB+1:N) has
> been updated.

LDA : INTEGER [in]
> The leading dimension of the array A. LDA >= max(1,M).

JPVT : INTEGER array, dimension (N) [in,out]
> JPVT(I) = K <==> Column K of the full matrix A has been
> permuted into position I in AP.

TAU : COMPLEX array, dimension (KB) [out]
> The scalar factors of the elementary reflectors.

VN1 : REAL array, dimension (N) [in,out]
> The vector with the partial column norms.

VN2 : REAL array, dimension (N) [in,out]
> The vector with the exact column norms.

AUXV : COMPLEX array, dimension (NB) [in,out]
> Auxiliary vector.

F : COMPLEX array, dimension (LDF,NB) [in,out]
> Matrix  F\*\*H = L \* Y\*\*H \* A.

LDF : INTEGER [in]
> The leading dimension of the array F. LDF >= max(1,N).

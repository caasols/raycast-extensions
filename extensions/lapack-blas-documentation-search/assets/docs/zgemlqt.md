```fortran
subroutine zgemlqt (
        character side,
        character trans,
        integer m,
        integer n,
        integer k,
        integer mb,
        complex*16, dimension( ldv, * ) v,
        integer ldv,
        complex*16, dimension( ldt, * ) t,
        integer ldt,
        complex*16, dimension( ldc, * ) c,
        integer ldc,
        complex*16, dimension( * ) work,
        integer info
)
```

ZGEMLQT overwrites the general complex M-by-N matrix C with

SIDE = 'L'     SIDE = 'R'
TRANS = 'N':      Q C            C Q
TRANS = 'C':   Q\*\*H C            C Q\*\*H

where Q is a complex unitary matrix defined as the product of K
elementary reflectors:

Q = H(1) H(2) . . . H(K) = I - V T V\*\*H

generated using the compact WY representation as returned by ZGELQT.

Q is of order M if SIDE = 'L' and of order N  if SIDE = 'R'.

## Parameters
SIDE : CHARACTER\*1 [in]
> = 'L': apply Q or Q\*\*H from the Left;
> = 'R': apply Q or Q\*\*H from the Right.

TRANS : CHARACTER\*1 [in]
> = 'N':  No transpose, apply Q;
> = 'C':  Conjugate transpose, apply Q\*\*H.

M : INTEGER [in]
> The number of rows of the matrix C. M >= 0.

N : INTEGER [in]
> The number of columns of the matrix C. N >= 0.

K : INTEGER [in]
> The number of elementary reflectors whose product defines
> the matrix Q.
> If SIDE = 'L', M >= K >= 0;
> if SIDE = 'R', N >= K >= 0.

MB : INTEGER [in]
> The block size used for the storage of T.  K >= MB >= 1.
> This must be the same value of MB used to generate T
> in ZGELQT.

V : COMPLEX\*16 array, dimension [in]
> (LDV,M) if SIDE = 'L',
> (LDV,N) if SIDE = 'R'
> The i-th row must contain the vector which defines the
> elementary reflector H(i), for i = 1,2,...,k, as returned by
> ZGELQT in the first K rows of its array argument A.

LDV : INTEGER [in]
> The leading dimension of the array V. LDV >= max(1,K).

T : COMPLEX\*16 array, dimension (LDT,K) [in]
> The upper triangular factors of the block reflectors
> as returned by ZGELQT, stored as a MB-by-K matrix.

LDT : INTEGER [in]
> The leading dimension of the array T.  LDT >= MB.

C : COMPLEX\*16 array, dimension (LDC,N) [in,out]
> On entry, the M-by-N matrix C.
> On exit, C is overwritten by Q C, Q\*\*H C, C Q\*\*H or C Q.

LDC : INTEGER [in]
> The leading dimension of the array C. LDC >= max(1,M).

WORK : COMPLEX\*16 array. The dimension of [out]
> WORK is N\*MB if SIDE = 'L', or  M\*MB if SIDE = 'R'.

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value

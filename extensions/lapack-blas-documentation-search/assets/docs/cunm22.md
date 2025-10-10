```fortran
subroutine cunm22 (
        character side,
        character trans,
        integer m,
        integer n,
        integer n1,
        integer n2,
        complex, dimension( ldq, * ) q,
        integer ldq,
        complex, dimension( ldc, * ) c,
        integer ldc,
        complex, dimension( * ) work,
        integer lwork,
        integer info
)
```

CUNM22 overwrites the general complex M-by-N matrix C with

SIDE = 'L'     SIDE = 'R'
TRANS = 'N':      Q \* C          C \* Q
TRANS = 'C':      Q\*\*H \* C       C \* Q\*\*H

where Q is a complex unitary matrix of order NQ, with NQ = M if
SIDE = 'L' and NQ = N if SIDE = 'R'.
The unitary matrix Q processes a 2-by-2 block structure

[  Q11  Q12  ]
Q = [            ]
[  Q21  Q22  ],

where Q12 is an N1-by-N1 lower triangular matrix and Q21 is an
N2-by-N2 upper triangular matrix.

## Parameters
SIDE : CHARACTER\*1 [in]
> = 'L': apply Q or Q\*\*H from the Left;
> = 'R': apply Q or Q\*\*H from the Right.

TRANS : CHARACTER\*1 [in]
> = 'N':  apply Q (No transpose);
> = 'C':  apply Q\*\*H (Conjugate transpose).

M : INTEGER [in]
> The number of rows of the matrix C. M >= 0.

N : INTEGER [in]
> The number of columns of the matrix C. N >= 0.

N2 : N1 is INTEGER [in]
> N2 is INTEGER
> The dimension of Q12 and Q21, respectively. N1, N2 >= 0.
> The following requirement must be satisfied:
> N1 + N2 = M if SIDE = 'L' and N1 + N2 = N if SIDE = 'R'.

Q : COMPLEX array, dimension [in]
> (LDQ,M) if SIDE = 'L'
> (LDQ,N) if SIDE = 'R'

LDQ : INTEGER [in]
> The leading dimension of the array Q.
> LDQ >= max(1,M) if SIDE = 'L'; LDQ >= max(1,N) if SIDE = 'R'.

C : COMPLEX array, dimension (LDC,N) [in,out]
> On entry, the M-by-N matrix C.
> On exit, C is overwritten by Q\*C or Q\*\*H\*C or C\*Q\*\*H or C\*Q.

LDC : INTEGER [in]
> The leading dimension of the array C. LDC >= max(1,M).

WORK : COMPLEX array, dimension (MAX(1,LWORK)) [out]
> On exit, if INFO = 0, WORK(1) returns the optimal LWORK.

LWORK : INTEGER [in]
> The dimension of the array WORK.
> If SIDE = 'L', LWORK >= max(1,N);
> if SIDE = 'R', LWORK >= max(1,M).
> For optimum performance LWORK >= M\*N.
> 
> If LWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal size of the WORK array, returns
> this value as the first entry of the WORK array, and no error
> message related to LWORK is issued by XERBLA.

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value

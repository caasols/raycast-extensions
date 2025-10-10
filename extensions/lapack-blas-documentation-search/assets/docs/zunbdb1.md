```fortran
subroutine zunbdb1 (
        integer m,
        integer p,
        integer q,
        complex*16, dimension(ldx11,*) x11,
        integer ldx11,
        complex*16, dimension(ldx21,*) x21,
        integer ldx21,
        double precision, dimension(*) theta,
        double precision, dimension(*) phi,
        complex*16, dimension(*) taup1,
        complex*16, dimension(*) taup2,
        complex*16, dimension(*) tauq1,
        complex*16, dimension(*) work,
        integer lwork,
        integer info
)
```

ZUNBDB1 simultaneously bidiagonalizes the blocks of a tall and skinny
matrix X with orthonormal columns:

[ B11 ]
[ X11 ]   [ P1 |    ] [  0  ]
[-----] = [---------] [-----] Q1\*\*T .
[ X21 ]   [    | P2 ] [ B21 ]
[  0  ]

X11 is P-by-Q, and X21 is (M-P)-by-Q. Q must be no larger than P,
M-P, or M-Q. Routines ZUNBDB2, ZUNBDB3, and ZUNBDB4 handle cases in
which Q is not the minimum dimension.

The unitary matrices P1, P2, and Q1 are P-by-P, (M-P)-by-(M-P),
and (M-Q)-by-(M-Q), respectively. They are represented implicitly by
Householder vectors.

B11 and B12 are Q-by-Q bidiagonal matrices represented implicitly by
angles THETA, PHI.

## Parameters
M : INTEGER [in]
> The number of rows X11 plus the number of rows in X21.

P : INTEGER [in]
> The number of rows in X11. 0 <= P <= M.

Q : INTEGER [in]
> The number of columns in X11 and X21. 0 <= Q <=
> MIN(P,M-P,M-Q).

X11 : COMPLEX\*16 array, dimension (LDX11,Q) [in,out]
> On entry, the top block of the matrix X to be reduced. On
> exit, the columns of tril(X11) specify reflectors for P1 and
> the rows of triu(X11,1) specify reflectors for Q1.

LDX11 : INTEGER [in]
> The leading dimension of X11. LDX11 >= P.

X21 : COMPLEX\*16 array, dimension (LDX21,Q) [in,out]
> On entry, the bottom block of the matrix X to be reduced. On
> exit, the columns of tril(X21) specify reflectors for P2.

LDX21 : INTEGER [in]
> The leading dimension of X21. LDX21 >= M-P.

THETA : DOUBLE PRECISION array, dimension (Q) [out]
> The entries of the bidiagonal blocks B11, B21 are defined by
> THETA and PHI. See Further Details.

PHI : DOUBLE PRECISION array, dimension (Q-1) [out]
> The entries of the bidiagonal blocks B11, B21 are defined by
> THETA and PHI. See Further Details.

TAUP1 : COMPLEX\*16 array, dimension (P) [out]
> The scalar factors of the elementary reflectors that define
> P1.

TAUP2 : COMPLEX\*16 array, dimension (M-P) [out]
> The scalar factors of the elementary reflectors that define
> P2.

TAUQ1 : COMPLEX\*16 array, dimension (Q) [out]
> The scalar factors of the elementary reflectors that define
> Q1.

WORK : COMPLEX\*16 array, dimension (LWORK) [out]

LWORK : INTEGER [in]
> The dimension of the array WORK. LWORK >= M-Q.
> 
> If LWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal size of the WORK array, returns
> this value as the first entry of the WORK array, and no error
> message related to LWORK is issued by XERBLA.

INFO : INTEGER [out]
> = 0:  successful exit.
> < 0:  if INFO = -i, the i-th argument had an illegal value.

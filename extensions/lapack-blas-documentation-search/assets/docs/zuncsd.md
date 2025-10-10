```fortran
recursive subroutine zuncsd (
        character jobu1,
        character jobu2,
        character jobv1t,
        character jobv2t,
        character trans,
        character signs,
        integer m,
        integer p,
        integer q,
        complex*16, dimension( ldx11, * ) x11,
        integer ldx11,
        complex*16, dimension( ldx12, * ) x12,
        integer ldx12,
        complex*16, dimension( ldx21, * ) x21,
        integer ldx21,
        complex*16, dimension( ldx22,                         * ) x22,
        integer ldx22,
        double precision, dimension( * ) theta,
        complex*16, dimension( ldu1, * ) u1,
        integer ldu1,
        complex*16, dimension( ldu2, * ) u2,
        integer ldu2,
        complex*16, dimension( ldv1t, * ) v1t,
        integer ldv1t,
        complex*16, dimension( ldv2t, * ) v2t,
        integer ldv2t,
        complex*16, dimension( * ) work,
        integer lwork,
        double precision, dimension( * ) rwork,
        integer lrwork,
        integer, dimension( * ) iwork,
        integer info
)
```

ZUNCSD computes the CS decomposition of an M-by-M partitioned
unitary matrix X:

[  I  0  0 |  0  0  0 ]
[  0  C  0 |  0 -S  0 ]
[ X11 | X12 ]   [ U1 |    ] [  0  0  0 |  0  0 -I ] [ V1 |    ]\*\*H
X = [-----------] = [---------] [---------------------] [---------]   .
[ X21 | X22 ]   [    | U2 ] [  0  0  0 |  I  0  0 ] [    | V2 ]
[  0  S  0 |  0  C  0 ]
[  0  0  I |  0  0  0 ]

X11 is P-by-Q. The unitary matrices U1, U2, V1, and V2 are P-by-P,
(M-P)-by-(M-P), Q-by-Q, and (M-Q)-by-(M-Q), respectively. C and S are
R-by-R nonnegative diagonal matrices satisfying C^2 + S^2 = I, in
which R = MIN(P,M-P,Q,M-Q).

## Parameters
JOBU1 : CHARACTER [in]
> = 'Y':      U1 is computed;
> otherwise:  U1 is not computed.

JOBU2 : CHARACTER [in]
> = 'Y':      U2 is computed;
> otherwise:  U2 is not computed.

JOBV1T : CHARACTER [in]
> = 'Y':      V1T is computed;
> otherwise:  V1T is not computed.

JOBV2T : CHARACTER [in]
> = 'Y':      V2T is computed;
> otherwise:  V2T is not computed.

TRANS : CHARACTER [in]
> = 'T':      X, U1, U2, V1T, and V2T are stored in row-major
> order;
> otherwise:  X, U1, U2, V1T, and V2T are stored in column-
> major order.

SIGNS : CHARACTER [in]
> = 'O':      The lower-left block is made nonpositive (the
> convention);
> otherwise:  The upper-right block is made nonpositive (the
> convention).

M : INTEGER [in]
> The number of rows and columns in X.

P : INTEGER [in]
> The number of rows in X11 and X12. 0 <= P <= M.

Q : INTEGER [in]
> The number of columns in X11 and X21. 0 <= Q <= M.

X11 : COMPLEX\*16 array, dimension (LDX11,Q) [in,out]
> On entry, part of the unitary matrix whose CSD is desired.

LDX11 : INTEGER [in]
> The leading dimension of X11. LDX11 >= MAX(1,P).

X12 : COMPLEX\*16 array, dimension (LDX12,M-Q) [in,out]
> On entry, part of the unitary matrix whose CSD is desired.

LDX12 : INTEGER [in]
> The leading dimension of X12. LDX12 >= MAX(1,P).

X21 : COMPLEX\*16 array, dimension (LDX21,Q) [in,out]
> On entry, part of the unitary matrix whose CSD is desired.

LDX21 : INTEGER [in]
> The leading dimension of X11. LDX21 >= MAX(1,M-P).

X22 : COMPLEX\*16 array, dimension (LDX22,M-Q) [in,out]
> On entry, part of the unitary matrix whose CSD is desired.

LDX22 : INTEGER [in]
> The leading dimension of X11. LDX22 >= MAX(1,M-P).

THETA : DOUBLE PRECISION array, dimension (R), in which R = [out]
> MIN(P,M-P,Q,M-Q).
> C = DIAG( COS(THETA(1)), ... , COS(THETA(R)) ) and
> S = DIAG( SIN(THETA(1)), ... , SIN(THETA(R)) ).

U1 : COMPLEX\*16 array, dimension (LDU1,P) [out]
> If JOBU1 = 'Y', U1 contains the P-by-P unitary matrix U1.

LDU1 : INTEGER [in]
> The leading dimension of U1. If JOBU1 = 'Y', LDU1 >=
> MAX(1,P).

U2 : COMPLEX\*16 array, dimension (LDU2,M-P) [out]
> If JOBU2 = 'Y', U2 contains the (M-P)-by-(M-P) unitary
> matrix U2.

LDU2 : INTEGER [in]
> The leading dimension of U2. If JOBU2 = 'Y', LDU2 >=
> MAX(1,M-P).

V1T : COMPLEX\*16 array, dimension (LDV1T,Q) [out]
> If JOBV1T = 'Y', V1T contains the Q-by-Q matrix unitary
> matrix V1\*\*H.

LDV1T : INTEGER [in]
> The leading dimension of V1T. If JOBV1T = 'Y', LDV1T >=
> MAX(1,Q).

V2T : COMPLEX\*16 array, dimension (LDV2T,M-Q) [out]
> If JOBV2T = 'Y', V2T contains the (M-Q)-by-(M-Q) unitary
> matrix V2\*\*H.

LDV2T : INTEGER [in]
> The leading dimension of V2T. If JOBV2T = 'Y', LDV2T >=
> MAX(1,M-Q).

WORK : COMPLEX\*16 array, dimension (MAX(1,LWORK)) [out]
> On exit, if INFO = 0, WORK(1) returns the optimal LWORK.

LWORK : INTEGER [in]
> The dimension of the array WORK.
> 
> If LWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal size of the WORK array, returns
> this value as the first entry of the work array, and no error
> message related to LWORK is issued by XERBLA.

RWORK : DOUBLE PRECISION array, dimension MAX(1,LRWORK) [out]
> On exit, if INFO = 0, RWORK(1) returns the optimal LRWORK.
> If INFO > 0 on exit, RWORK(2:R) contains the values PHI(1),
> ..., PHI(R-1) that, together with THETA(1), ..., THETA(R),
> define the matrix in intermediate bidiagonal-block form
> remaining after nonconvergence. INFO specifies the number
> of nonzero PHI's.

LRWORK : INTEGER [in]
> The dimension of the array RWORK.
> 
> If LRWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal size of the RWORK array, returns
> this value as the first entry of the work array, and no error
> message related to LRWORK is issued by XERBLA.

IWORK : INTEGER array, dimension (M-MIN(P,M-P,Q,M-Q)) [out]

INFO : INTEGER [out]
> = 0:  successful exit.
> < 0:  if INFO = -i, the i-th argument had an illegal value.
> > 0:  ZBBCSD did not converge. See the description of RWORK
> above for details.

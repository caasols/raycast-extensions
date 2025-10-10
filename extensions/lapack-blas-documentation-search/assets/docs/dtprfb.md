```fortran
subroutine dtprfb (
        character side,
        character trans,
        character direct,
        character storev,
        integer m,
        integer n,
        integer k,
        integer l,
        double precision, dimension( ldv, * ) v,
        integer ldv,
        double precision, dimension( ldt, * ) t,
        integer ldt,
        double precision, dimension( lda, * ) a,
        integer lda,
        double precision, dimension( ldb, * ) b,
        integer ldb,
        double precision, dimension( ldwork, * ) work,
        integer ldwork
)
```

DTPRFB applies a real  block reflector H or its
transpose H\*\*T to a real matrix C, which is composed of two
blocks A and B, either from the left or right.

## Parameters
SIDE : CHARACTER\*1 [in]
> = 'L': apply H or H\*\*T from the Left
> = 'R': apply H or H\*\*T from the Right

TRANS : CHARACTER\*1 [in]
> = 'N': apply H (No transpose)
> = 'T': apply H\*\*T (Transpose)

DIRECT : CHARACTER\*1 [in]
> Indicates how H is formed from a product of elementary
> reflectors
> = 'F': H = H(1) H(2) . . . H(k) (Forward)
> = 'B': H = H(k) . . . H(2) H(1) (Backward)

STOREV : CHARACTER\*1 [in]
> Indicates how the vectors which define the elementary
> reflectors are stored:
> = 'C': Columns
> = 'R': Rows

M : INTEGER [in]
> The number of rows of the matrix B.
> M >= 0.

N : INTEGER [in]
> The number of columns of the matrix B.
> N >= 0.

K : INTEGER [in]
> The order of the matrix T, i.e. the number of elementary
> reflectors whose product defines the block reflector.
> K >= 0.

L : INTEGER [in]
> The order of the trapezoidal part of V.
> K >= L >= 0.  See Further Details.

V : DOUBLE PRECISION array, dimension [in]
> (LDV,K) if STOREV = 'C'
> (LDV,M) if STOREV = 'R' and SIDE = 'L'
> (LDV,N) if STOREV = 'R' and SIDE = 'R'
> The pentagonal matrix V, which contains the elementary reflectors
> H(1), H(2), ..., H(K).  See Further Details.

LDV : INTEGER [in]
> The leading dimension of the array V.
> If STOREV = 'C' and SIDE = 'L', LDV >= max(1,M);
> if STOREV = 'C' and SIDE = 'R', LDV >= max(1,N);
> if STOREV = 'R', LDV >= K.

T : DOUBLE PRECISION array, dimension (LDT,K) [in]
> The triangular K-by-K matrix T in the representation of the
> block reflector.

LDT : INTEGER [in]
> The leading dimension of the array T.
> LDT >= K.

A : DOUBLE PRECISION array, dimension [in,out]
> (LDA,N) if SIDE = 'L' or (LDA,K) if SIDE = 'R'
> On entry, the K-by-N or M-by-K matrix A.
> On exit, A is overwritten by the corresponding block of
> H\*C or H\*\*T\*C or C\*H or C\*H\*\*T.  See Further Details.

LDA : INTEGER [in]
> The leading dimension of the array A.
> If SIDE = 'L', LDA >= max(1,K);
> If SIDE = 'R', LDA >= max(1,M).

B : DOUBLE PRECISION array, dimension (LDB,N) [in,out]
> On entry, the M-by-N matrix B.
> On exit, B is overwritten by the corresponding block of
> H\*C or H\*\*T\*C or C\*H or C\*H\*\*T.  See Further Details.

LDB : INTEGER [in]
> The leading dimension of the array B.
> LDB >= max(1,M).

WORK : DOUBLE PRECISION array, dimension [out]
> (LDWORK,N) if SIDE = 'L',
> (LDWORK,K) if SIDE = 'R'.

LDWORK : INTEGER [in]
> The leading dimension of the array WORK.
> If SIDE = 'L', LDWORK >= K;
> if SIDE = 'R', LDWORK >= M.

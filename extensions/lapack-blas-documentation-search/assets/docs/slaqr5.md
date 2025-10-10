```fortran
subroutine slaqr5 (
        logical wantt,
        logical wantz,
        integer kacc22,
        integer n,
        integer ktop,
        integer kbot,
        integer nshfts,
        real, dimension( * ) sr,
        real, dimension( * ) si,
        real, dimension( ldh, * ) h,
        integer ldh,
        integer iloz,
        integer ihiz,
        real, dimension( ldz, * ) z,
        integer ldz,
        real, dimension( ldv, * ) v,
        integer ldv,
        real, dimension( ldu, * ) u,
        integer ldu,
        integer nv,
        real, dimension( ldwv, * ) wv,
        integer ldwv,
        integer nh,
        real, dimension( ldwh, * ) wh,
        integer ldwh
)
```

SLAQR5, called by SLAQR0, performs a
single small-bulge multi-shift QR sweep.

## Parameters
WANTT : LOGICAL [in]
> WANTT = .true. if the quasi-triangular Schur factor
> is being computed.  WANTT is set to .false. otherwise.

WANTZ : LOGICAL [in]
> WANTZ = .true. if the orthogonal Schur factor is being
> computed.  WANTZ is set to .false. otherwise.

KACC22 : INTEGER with value 0, 1, or 2. [in]
> Specifies the computation mode of far-from-diagonal
> orthogonal updates.
> = 0: SLAQR5 does not accumulate reflections and does not
> use matrix-matrix multiply to update far-from-diagonal
> matrix entries.
> = 1: SLAQR5 accumulates reflections and uses matrix-matrix
> multiply to update the far-from-diagonal matrix entries.
> = 2: Same as KACC22 = 1. This option used to enable exploiting
> the 2-by-2 structure during matrix multiplications, but
> this is no longer supported.

N : INTEGER [in]
> N is the order of the Hessenberg matrix H upon which this
> subroutine operates.

KTOP : INTEGER [in]

KBOT : INTEGER [in]
> These are the first and last rows and columns of an
> isolated diagonal block upon which the QR sweep is to be
> applied. It is assumed without a check that
> either KTOP = 1  or   H(KTOP,KTOP-1) = 0
> and
> either KBOT = N  or   H(KBOT+1,KBOT) = 0.

NSHFTS : INTEGER [in]
> NSHFTS gives the number of simultaneous shifts.  NSHFTS
> must be positive and even.

SR : REAL array, dimension (NSHFTS) [in,out]

SI : REAL array, dimension (NSHFTS) [in,out]
> SR contains the real parts and SI contains the imaginary
> parts of the NSHFTS shifts of origin that define the
> multi-shift QR sweep.  On output SR and SI may be
> reordered.

H : REAL array, dimension (LDH,N) [in,out]
> On input H contains a Hessenberg matrix.  On output a
> multi-shift QR sweep with shifts SR(J)+i\*SI(J) is applied
> to the isolated diagonal block in rows and columns KTOP
> through KBOT.

LDH : INTEGER [in]
> LDH is the leading dimension of H just as declared in the
> calling procedure.  LDH >= MAX(1,N).

ILOZ : INTEGER [in]

IHIZ : INTEGER [in]
> Specify the rows of Z to which transformations must be
> applied if WANTZ is .TRUE.. 1 <= ILOZ <= IHIZ <= N

Z : REAL array, dimension (LDZ,IHIZ) [in,out]
> If WANTZ = .TRUE., then the QR Sweep orthogonal
> similarity transformation is accumulated into
> Z(ILOZ:IHIZ,ILOZ:IHIZ) from the right.
> If WANTZ = .FALSE., then Z is unreferenced.

LDZ : INTEGER [in]
> LDA is the leading dimension of Z just as declared in
> the calling procedure. LDZ >= N.

V : REAL array, dimension (LDV,NSHFTS/2) [out]

LDV : INTEGER [in]
> LDV is the leading dimension of V as declared in the
> calling procedure.  LDV >= 3.

U : REAL array, dimension (LDU,2\*NSHFTS) [out]

LDU : INTEGER [in]
> LDU is the leading dimension of U just as declared in the
> in the calling subroutine.  LDU >= 2\*NSHFTS.

NV : INTEGER [in]
> NV is the number of rows in WV agailable for workspace.
> NV >= 1.

WV : REAL array, dimension (LDWV,2\*NSHFTS) [out]

LDWV : INTEGER [in]
> LDWV is the leading dimension of WV as declared in the
> in the calling subroutine.  LDWV >= NV.

NH : INTEGER [in]
> NH is the number of columns in array WH available for
> workspace. NH >= 1.

WH : REAL array, dimension (LDWH,NH) [out]

LDWH : INTEGER [in]
> Leading dimension of WH just as declared in the
> calling procedure.  LDWH >= 2\*NSHFTS.

```fortran
subroutine dlar1v (
        integer n,
        integer b1,
        integer bn,
        double precision lambda,
        double precision, dimension( * ) d,
        double precision, dimension( * ) l,
        double precision, dimension( * ) ld,
        double precision, dimension( * ) lld,
        double precision pivmin,
        double precision gaptol,
        double precision, dimension( * ) z,
        logical wantnc,
        integer negcnt,
        double precision ztz,
        double precision mingma,
        integer r,
        integer, dimension( * ) isuppz,
        double precision nrminv,
        double precision resid,
        double precision rqcorr,
        double precision, dimension( * ) work
)
```

DLAR1V computes the (scaled) r-th column of the inverse of
the sumbmatrix in rows B1 through BN of the tridiagonal matrix
L D L\*\*T - sigma I. When sigma is close to an eigenvalue, the
computed vector is an accurate eigenvector. Usually, r corresponds
to the index where the eigenvector is largest in magnitude.
The following steps accomplish this computation :
(a) Stationary qd transform,  L D L\*\*T - sigma I = L(+) D(+) L(+)\*\*T,
(b) Progressive qd transform, L D L\*\*T - sigma I = U(-) D(-) U(-)\*\*T,
(c) Computation of the diagonal elements of the inverse of
L D L\*\*T - sigma I by combining the above transforms, and choosing
r as the index where the diagonal of the inverse is (one of the)
largest in magnitude.
(d) Computation of the (scaled) r-th column of the inverse using the
twisted factorization obtained by combining the top part of the
the stationary and the bottom part of the progressive transform.

## Parameters
N : INTEGER [in]
> The order of the matrix L D L\*\*T.

B1 : INTEGER [in]
> First index of the submatrix of L D L\*\*T.

BN : INTEGER [in]
> Last index of the submatrix of L D L\*\*T.

LAMBDA : DOUBLE PRECISION [in]
> The shift. In order to compute an accurate eigenvector,
> LAMBDA should be a good approximation to an eigenvalue
> of L D L\*\*T.

L : DOUBLE PRECISION array, dimension (N-1) [in]
> The (n-1) subdiagonal elements of the unit bidiagonal matrix
> L, in elements 1 to N-1.

D : DOUBLE PRECISION array, dimension (N) [in]
> The n diagonal elements of the diagonal matrix D.

LD : DOUBLE PRECISION array, dimension (N-1) [in]
> The n-1 elements L(i)\*D(i).

LLD : DOUBLE PRECISION array, dimension (N-1) [in]
> The n-1 elements L(i)\*L(i)\*D(i).

PIVMIN : DOUBLE PRECISION [in]
> The minimum pivot in the Sturm sequence.

GAPTOL : DOUBLE PRECISION [in]
> Tolerance that indicates when eigenvector entries are negligible
> w.r.t. their contribution to the residual.

Z : DOUBLE PRECISION array, dimension (N) [in,out]
> On input, all entries of Z must be set to 0.
> On output, Z contains the (scaled) r-th column of the
> inverse. The scaling is such that Z(R) equals 1.

WANTNC : LOGICAL [in]
> Specifies whether NEGCNT has to be computed.

NEGCNT : INTEGER [out]
> If WANTNC is .TRUE. then NEGCNT = the number of pivots < pivmin
> in the  matrix factorization L D L\*\*T, and NEGCNT = -1 otherwise.

ZTZ : DOUBLE PRECISION [out]
> The square of the 2-norm of Z.

MINGMA : DOUBLE PRECISION [out]
> The reciprocal of the largest (in magnitude) diagonal
> element of the inverse of L D L\*\*T - sigma I.

R : INTEGER [in,out]
> The twist index for the twisted factorization used to
> compute Z.
> On input, 0 <= R <= N. If R is input as 0, R is set to
> the index where (L D L\*\*T - sigma I)^{-1} is largest
> in magnitude. If 1 <= R <= N, R is unchanged.
> On output, R contains the twist index used to compute Z.
> Ideally, R designates the position of the maximum entry in the
> eigenvector.

ISUPPZ : INTEGER array, dimension (2) [out]
> The support of the vector in Z, i.e., the vector Z is
> nonzero only in elements ISUPPZ(1) through ISUPPZ( 2 ).

NRMINV : DOUBLE PRECISION [out]
> NRMINV = 1/SQRT( ZTZ )

RESID : DOUBLE PRECISION [out]
> The residual of the FP vector.
> RESID = ABS( MINGMA )/SQRT( ZTZ )

RQCORR : DOUBLE PRECISION [out]
> The Rayleigh Quotient correction to LAMBDA.
> RQCORR = MINGMA\*TMP

WORK : DOUBLE PRECISION array, dimension (4\*N) [out]

```fortran
subroutine slarz (
        character side,
        integer m,
        integer n,
        integer l,
        real, dimension( * ) v,
        integer incv,
        real tau,
        real, dimension( ldc, * ) c,
        integer ldc,
        real, dimension( * ) work
)
```

SLARZ applies a real elementary reflector H to a real M-by-N
matrix C, from either the left or the right. H is represented in the
form

H = I - tau \* v \* v\*\*T

where tau is a real scalar and v is a real vector.

If tau = 0, then H is taken to be the unit matrix.


H is a product of k elementary reflectors as returned by STZRZF.

## Parameters
SIDE : CHARACTER\*1 [in]
> = 'L': form  H \* C
> = 'R': form  C \* H

M : INTEGER [in]
> The number of rows of the matrix C.

N : INTEGER [in]
> The number of columns of the matrix C.

L : INTEGER [in]
> The number of entries of the vector V containing
> the meaningful part of the Householder vectors.
> If SIDE = 'L', M >= L >= 0, if SIDE = 'R', N >= L >= 0.

V : REAL array, dimension (1+(L-1)\*abs(INCV)) [in]
> The vector v in the representation of H as returned by
> STZRZF. V is not used if TAU = 0.

INCV : INTEGER [in]
> The increment between elements of v. INCV <> 0.

TAU : REAL [in]
> The value tau in the representation of H.

C : REAL array, dimension (LDC,N) [in,out]
> On entry, the M-by-N matrix C.
> On exit, C is overwritten by the matrix H \* C if SIDE = 'L',
> or C \* H if SIDE = 'R'.

LDC : INTEGER [in]
> The leading dimension of the array C. LDC >= max(1,M).

WORK : REAL array, dimension [out]
> (N) if SIDE = 'L'
> or (M) if SIDE = 'R'

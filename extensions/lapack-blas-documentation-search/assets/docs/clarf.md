```fortran
subroutine clarf (
        character side,
        integer m,
        integer n,
        complex, dimension( * ) v,
        integer incv,
        complex tau,
        complex, dimension( ldc, * ) c,
        integer ldc,
        complex, dimension( * ) work
)
```

CLARF applies a complex elementary reflector H to a complex M-by-N
matrix C, from either the left or the right. H is represented in the
form

H = I - tau \* v \* v\*\*H

where tau is a complex scalar and v is a complex vector.

If tau = 0, then H is taken to be the unit matrix.

To apply H\*\*H (the conjugate transpose of H), supply conjg(tau) instead
tau.

## Parameters
SIDE : CHARACTER\*1 [in]
> = 'L': form  H \* C
> = 'R': form  C \* H

M : INTEGER [in]
> The number of rows of the matrix C.

N : INTEGER [in]
> The number of columns of the matrix C.

V : COMPLEX array, dimension [in]
> (1 + (M-1)\*abs(INCV)) if SIDE = 'L'
> or (1 + (N-1)\*abs(INCV)) if SIDE = 'R'
> The vector v in the representation of H. V is not used if
> TAU = 0.

INCV : INTEGER [in]
> The increment between elements of v. INCV <> 0.

TAU : COMPLEX [in]
> The value tau in the representation of H.

C : COMPLEX array, dimension (LDC,N) [in,out]
> On entry, the M-by-N matrix C.
> On exit, C is overwritten by the matrix H \* C if SIDE = 'L',
> or C \* H if SIDE = 'R'.

LDC : INTEGER [in]
> The leading dimension of the array C. LDC >= max(1,M).

WORK : COMPLEX array, dimension [out]
> (N) if SIDE = 'L'
> or (M) if SIDE = 'R'

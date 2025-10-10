```fortran
subroutine clarfx (
        character side,
        integer m,
        integer n,
        complex, dimension( * ) v,
        complex tau,
        complex, dimension( ldc, * ) c,
        integer ldc,
        complex, dimension( * ) work
)
```

CLARFX applies a complex elementary reflector H to a complex m by n
matrix C, from either the left or the right. H is represented in the
form

H = I - tau \* v \* v\*\*H

where tau is a complex scalar and v is a complex vector.

If tau = 0, then H is taken to be the unit matrix

This version uses inline code if H has order < 11.

## Parameters
SIDE : CHARACTER\*1 [in]
> = 'L': form  H \* C
> = 'R': form  C \* H

M : INTEGER [in]
> The number of rows of the matrix C.

N : INTEGER [in]
> The number of columns of the matrix C.

V : COMPLEX array, dimension (M) if SIDE = 'L' [in]
> or (N) if SIDE = 'R'
> The vector v in the representation of H.

TAU : COMPLEX [in]
> The value tau in the representation of H.

C : COMPLEX array, dimension (LDC,N) [in,out]
> On entry, the m by n matrix C.
> On exit, C is overwritten by the matrix H \* C if SIDE = 'L',
> or C \* H if SIDE = 'R'.

LDC : INTEGER [in]
> The leading dimension of the array C. LDC >= max(1,M).

WORK : COMPLEX array, dimension (N) if SIDE = 'L' [out]
> or (M) if SIDE = 'R'
> WORK is not referenced if H has order < 11.

```fortran
subroutine dpbequ (
        character uplo,
        integer n,
        integer kd,
        double precision, dimension( ldab, * ) ab,
        integer ldab,
        double precision, dimension( * ) s,
        double precision scond,
        double precision amax,
        integer info
)
```

DPBEQU computes row and column scalings intended to equilibrate a
symmetric positive definite band matrix A and reduce its condition
number (with respect to the two-norm).  S contains the scale factors,
S(i) = 1/sqrt(A(i,i)), chosen so that the scaled matrix B with
elements B(i,j) = S(i)\*A(i,j)\*S(j) has ones on the diagonal.  This
choice of S puts the condition number of B within a factor N of the
smallest possible condition number over all possible diagonal
scalings.

## Parameters
UPLO : CHARACTER\*1 [in]
> = 'U':  Upper triangular of A is stored;
> = 'L':  Lower triangular of A is stored.

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

KD : INTEGER [in]
> The number of superdiagonals of the matrix A if UPLO = 'U',
> or the number of subdiagonals if UPLO = 'L'.  KD >= 0.

AB : DOUBLE PRECISION array, dimension (LDAB,N) [in]
> The upper or lower triangle of the symmetric band matrix A,
> stored in the first KD+1 rows of the array.  The j-th column
> of A is stored in the j-th column of the array AB as follows:
> if UPLO = 'U', AB(kd+1+i-j,j) = A(i,j) for max(1,j-kd)<=i<=j;
> if UPLO = 'L', AB(1+i-j,j)    = A(i,j) for j<=i<=min(n,j+kd).

LDAB : INTEGER [in]
> The leading dimension of the array A.  LDAB >= KD+1.

S : DOUBLE PRECISION array, dimension (N) [out]
> If INFO = 0, S contains the scale factors for A.

SCOND : DOUBLE PRECISION [out]
> If INFO = 0, S contains the ratio of the smallest S(i) to
> the largest S(i).  If SCOND >= 0.1 and AMAX is neither too
> large nor too small, it is not worth scaling by S.

AMAX : DOUBLE PRECISION [out]
> Absolute value of largest matrix element.  If AMAX is very
> close to overflow or very close to underflow, the matrix
> should be scaled.

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value.
> > 0:  if INFO = i, the i-th diagonal element is nonpositive.

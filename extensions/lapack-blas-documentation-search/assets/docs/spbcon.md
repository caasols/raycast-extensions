```fortran
subroutine spbcon (
        character uplo,
        integer n,
        integer kd,
        real, dimension( ldab, * ) ab,
        integer ldab,
        real anorm,
        real rcond,
        real, dimension( * ) work,
        integer, dimension( * ) iwork,
        integer info
)
```

SPBCON estimates the reciprocal of the condition number (in the
1-norm) of a real symmetric positive definite band matrix using the
Cholesky factorization A = U\*\*T\*U or A = L\*L\*\*T computed by SPBTRF.

An estimate is obtained for norm(inv(A)), and the reciprocal of the
condition number is computed as RCOND = 1 / (ANORM \* norm(inv(A))).

## Parameters
UPLO : CHARACTER\*1 [in]
> = 'U':  Upper triangular factor stored in AB;
> = 'L':  Lower triangular factor stored in AB.

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

KD : INTEGER [in]
> The number of superdiagonals of the matrix A if UPLO = 'U',
> or the number of subdiagonals if UPLO = 'L'.  KD >= 0.

AB : REAL array, dimension (LDAB,N) [in]
> The triangular factor U or L from the Cholesky factorization
> A = U\*\*T\*U or A = L\*L\*\*T of the band matrix A, stored in the
> first KD+1 rows of the array.  The j-th column of U or L is
> stored in the j-th column of the array AB as follows:
> if UPLO ='U', AB(kd+1+i-j,j) = U(i,j) for max(1,j-kd)<=i<=j;
> if UPLO ='L', AB(1+i-j,j)    = L(i,j) for j<=i<=min(n,j+kd).

LDAB : INTEGER [in]
> The leading dimension of the array AB.  LDAB >= KD+1.

ANORM : REAL [in]
> The 1-norm (or infinity-norm) of the symmetric band matrix A.

RCOND : REAL [out]
> The reciprocal of the condition number of the matrix A,
> computed as RCOND = 1/(ANORM \* AINVNM), where AINVNM is an
> estimate of the 1-norm of inv(A) computed in this routine.

WORK : REAL array, dimension (3\*N) [out]

IWORK : INTEGER array, dimension (N) [out]

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value

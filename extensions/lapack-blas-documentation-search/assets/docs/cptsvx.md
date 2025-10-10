```fortran
subroutine cptsvx (
        character fact,
        integer n,
        integer nrhs,
        real, dimension( * ) d,
        complex, dimension( * ) e,
        real, dimension( * ) df,
        complex, dimension( * ) ef,
        complex, dimension( ldb, * ) b,
        integer ldb,
        complex, dimension( ldx, * ) x,
        integer ldx,
        real rcond,
        real, dimension( * ) ferr,
        real, dimension( * ) berr,
        complex, dimension( * ) work,
        real, dimension( * ) rwork,
        integer info
)
```

CPTSVX uses the factorization A = L\*D\*L\*\*H to compute the solution
to a complex system of linear equations A\*X = B, where A is an
N-by-N Hermitian positive definite tridiagonal matrix and X and B
are N-by-NRHS matrices.

Error bounds on the solution and a condition estimate are also
provided.

## Parameters
FACT : CHARACTER\*1 [in]
> Specifies whether or not the factored form of the matrix
> A is supplied on entry.
> = 'F':  On entry, DF and EF contain the factored form of A.
> D, E, DF, and EF will not be modified.
> = 'N':  The matrix A will be copied to DF and EF and
> factored.

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of columns
> of the matrices B and X.  NRHS >= 0.

D : REAL array, dimension (N) [in]
> The n diagonal elements of the tridiagonal matrix A.

E : COMPLEX array, dimension (N-1) [in]
> The (n-1) subdiagonal elements of the tridiagonal matrix A.

DF : REAL array, dimension (N) [in,out]
> If FACT = 'F', then DF is an input argument and on entry
> contains the n diagonal elements of the diagonal matrix D
> from the L\*D\*L\*\*H factorization of A.
> If FACT = 'N', then DF is an output argument and on exit
> contains the n diagonal elements of the diagonal matrix D
> from the L\*D\*L\*\*H factorization of A.

EF : COMPLEX array, dimension (N-1) [in,out]
> If FACT = 'F', then EF is an input argument and on entry
> contains the (n-1) subdiagonal elements of the unit
> bidiagonal factor L from the L\*D\*L\*\*H factorization of A.
> If FACT = 'N', then EF is an output argument and on exit
> contains the (n-1) subdiagonal elements of the unit
> bidiagonal factor L from the L\*D\*L\*\*H factorization of A.

B : COMPLEX array, dimension (LDB,NRHS) [in]
> The N-by-NRHS right hand side matrix B.

LDB : INTEGER [in]
> The leading dimension of the array B.  LDB >= max(1,N).

X : COMPLEX array, dimension (LDX,NRHS) [out]
> If INFO = 0 or INFO = N+1, the N-by-NRHS solution matrix X.

LDX : INTEGER [in]
> The leading dimension of the array X.  LDX >= max(1,N).

RCOND : REAL [out]
> The reciprocal condition number of the matrix A.  If RCOND
> is less than the machine precision (in particular, if
> RCOND = 0), the matrix is singular to working precision.
> This condition is indicated by a return code of INFO > 0.

FERR : REAL array, dimension (NRHS) [out]
> The forward error bound for each solution vector
> X(j) (the j-th column of the solution matrix X).
> If XTRUE is the true solution corresponding to X(j), FERR(j)
> is an estimated upper bound for the magnitude of the largest
> element in (X(j) - XTRUE) divided by the magnitude of the
> largest element in X(j).

BERR : REAL array, dimension (NRHS) [out]
> The componentwise relative backward error of each solution
> vector X(j) (i.e., the smallest relative change in any
> element of A or B that makes X(j) an exact solution).

WORK : COMPLEX array, dimension (N) [out]

RWORK : REAL array, dimension (N) [out]

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value
> > 0:  if INFO = i, and i is
> <= N:  the leading principal minor of order i of A
> is not positive, so the factorization could not
> be completed, and the solution has not been
> computed. RCOND = 0 is returned.
> = N+1: U is nonsingular, but RCOND is less than machine
> precision, meaning that the matrix is singular
> to working precision.  Nevertheless, the
> solution and error bounds are computed because
> there are a number of situations where the
> computed solution can be more accurate than the
> value of RCOND would suggest.

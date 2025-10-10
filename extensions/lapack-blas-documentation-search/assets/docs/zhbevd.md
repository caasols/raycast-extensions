```fortran
subroutine zhbevd (
        character jobz,
        character uplo,
        integer n,
        integer kd,
        complex*16, dimension( ldab, * ) ab,
        integer ldab,
        double precision, dimension( * ) w,
        complex*16, dimension( ldz, * ) z,
        integer ldz,
        complex*16, dimension( * ) work,
        integer lwork,
        double precision, dimension( * ) rwork,
        integer lrwork,
        integer, dimension( * ) iwork,
        integer liwork,
        integer info
)
```

ZHBEVD computes all the eigenvalues and, optionally, eigenvectors of
a complex Hermitian band matrix A.  If eigenvectors are desired, it
uses a divide and conquer algorithm.

## Parameters
JOBZ : CHARACTER\*1 [in]
> = 'N':  Compute eigenvalues only;
> = 'V':  Compute eigenvalues and eigenvectors.

UPLO : CHARACTER\*1 [in]
> = 'U':  Upper triangle of A is stored;
> = 'L':  Lower triangle of A is stored.

N : INTEGER [in]
> The order of the matrix A.  N >= 0.

KD : INTEGER [in]
> The number of superdiagonals of the matrix A if UPLO = 'U',
> or the number of subdiagonals if UPLO = 'L'.  KD >= 0.

AB : COMPLEX\*16 array, dimension (LDAB, N) [in,out]
> On entry, the upper or lower triangle of the Hermitian band
> matrix A, stored in the first KD+1 rows of the array.  The
> j-th column of A is stored in the j-th column of the array AB
> as follows:
> if UPLO = 'U', AB(kd+1+i-j,j) = A(i,j) for max(1,j-kd)<=i<=j;
> if UPLO = 'L', AB(1+i-j,j)    = A(i,j) for j<=i<=min(n,j+kd).
> 
> On exit, AB is overwritten by values generated during the
> reduction to tridiagonal form.  If UPLO = 'U', the first
> superdiagonal and the diagonal of the tridiagonal matrix T
> are returned in rows KD and KD+1 of AB, and if UPLO = 'L',
> the diagonal and first subdiagonal of T are returned in the
> first two rows of AB.

LDAB : INTEGER [in]
> The leading dimension of the array AB.  LDAB >= KD + 1.

W : DOUBLE PRECISION array, dimension (N) [out]
> If INFO = 0, the eigenvalues in ascending order.

Z : COMPLEX\*16 array, dimension (LDZ, N) [out]
> If JOBZ = 'V', then if INFO = 0, Z contains the orthonormal
> eigenvectors of the matrix A, with the i-th column of Z
> holding the eigenvector associated with W(i).
> If JOBZ = 'N', then Z is not referenced.

LDZ : INTEGER [in]
> The leading dimension of the array Z.  LDZ >= 1, and if
> JOBZ = 'V', LDZ >= max(1,N).

WORK : COMPLEX\*16 array, dimension (MAX(1,LWORK)) [out]
> On exit, if INFO = 0, WORK(1) returns the optimal LWORK.

LWORK : INTEGER [in]
> The dimension of the array WORK.
> If N <= 1,               LWORK must be at least 1.
> If JOBZ = 'N' and N > 1, LWORK must be at least N.
> If JOBZ = 'V' and N > 1, LWORK must be at least 2\*N\*\*2.
> 
> If LWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal sizes of the WORK, RWORK and
> IWORK arrays, returns these values as the first entries of
> the WORK, RWORK and IWORK arrays, and no error message
> related to LWORK or LRWORK or LIWORK is issued by XERBLA.

RWORK : DOUBLE PRECISION array, [out]
> dimension (LRWORK)
> On exit, if INFO = 0, RWORK(1) returns the optimal LRWORK.

LRWORK : INTEGER [in]
> The dimension of array RWORK.
> If N <= 1,               LRWORK must be at least 1.
> If JOBZ = 'N' and N > 1, LRWORK must be at least N.
> If JOBZ = 'V' and N > 1, LRWORK must be at least
> 1 + 5\*N + 2\*N\*\*2.
> 
> If LRWORK = -1, then a workspace query is assumed; the
> routine only calculates the optimal sizes of the WORK, RWORK
> and IWORK arrays, returns these values as the first entries
> of the WORK, RWORK and IWORK arrays, and no error message
> related to LWORK or LRWORK or LIWORK is issued by XERBLA.

IWORK : INTEGER array, dimension (MAX(1,LIWORK)) [out]
> On exit, if INFO = 0, IWORK(1) returns the optimal LIWORK.

LIWORK : INTEGER [in]
> The dimension of array IWORK.
> If JOBZ = 'N' or N <= 1, LIWORK must be at least 1.
> If JOBZ = 'V' and N > 1, LIWORK must be at least 3 + 5\*N .
> 
> If LIWORK = -1, then a workspace query is assumed; the
> routine only calculates the optimal sizes of the WORK, RWORK
> and IWORK arrays, returns these values as the first entries
> of the WORK, RWORK and IWORK arrays, and no error message
> related to LWORK or LRWORK or LIWORK is issued by XERBLA.

INFO : INTEGER [out]
> = 0:  successful exit.
> < 0:  if INFO = -i, the i-th argument had an illegal value.
> > 0:  if INFO = i, the algorithm failed to converge; i
> off-diagonal elements of an intermediate tridiagonal
> form did not converge to zero.

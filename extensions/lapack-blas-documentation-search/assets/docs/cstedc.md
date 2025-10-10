```fortran
subroutine cstedc (
        character compz,
        integer n,
        real, dimension( * ) d,
        real, dimension( * ) e,
        complex, dimension( ldz, * ) z,
        integer ldz,
        complex, dimension( * ) work,
        integer lwork,
        real, dimension( * ) rwork,
        integer lrwork,
        integer, dimension( * ) iwork,
        integer liwork,
        integer info
)
```

CSTEDC computes all eigenvalues and, optionally, eigenvectors of a
symmetric tridiagonal matrix using the divide and conquer method.
The eigenvectors of a full or band complex Hermitian matrix can also
be found if CHETRD or CHPTRD or CHBTRD has been used to reduce this
matrix to tridiagonal form.

## Parameters
COMPZ : CHARACTER\*1 [in]
> = 'N':  Compute eigenvalues only.
> = 'I':  Compute eigenvectors of tridiagonal matrix also.
> = 'V':  Compute eigenvectors of original Hermitian matrix
> also.  On entry, Z contains the unitary matrix used
> to reduce the original matrix to tridiagonal form.

N : INTEGER [in]
> The dimension of the symmetric tridiagonal matrix.  N >= 0.

D : REAL array, dimension (N) [in,out]
> On entry, the diagonal elements of the tridiagonal matrix.
> On exit, if INFO = 0, the eigenvalues in ascending order.

E : REAL array, dimension (N-1) [in,out]
> On entry, the subdiagonal elements of the tridiagonal matrix.
> On exit, E has been destroyed.

Z : COMPLEX array, dimension (LDZ,N) [in,out]
> On entry, if COMPZ = 'V', then Z contains the unitary
> matrix used in the reduction to tridiagonal form.
> On exit, if INFO = 0, then if COMPZ = 'V', Z contains the
> orthonormal eigenvectors of the original Hermitian matrix,
> and if COMPZ = 'I', Z contains the orthonormal eigenvectors
> of the symmetric tridiagonal matrix.
> If  COMPZ = 'N', then Z is not referenced.

LDZ : INTEGER [in]
> The leading dimension of the array Z.  LDZ >= 1.
> If eigenvectors are desired, then LDZ >= max(1,N).

WORK : COMPLEX array, dimension (MAX(1,LWORK)) [out]
> On exit, if INFO = 0, WORK(1) returns the optimal LWORK.

LWORK : INTEGER [in]
> The dimension of the array WORK.
> If COMPZ = 'N' or 'I', or N <= 1, LWORK must be at least 1.
> If COMPZ = 'V' and N > 1, LWORK must be at least N\*N.
> Note that for COMPZ = 'V', then if N is less than or
> equal to the minimum divide size, usually 25, then LWORK need
> only be 1.
> 
> If LWORK = -1, then a workspace query is assumed; the routine
> only calculates the optimal sizes of the WORK, RWORK and
> IWORK arrays, returns these values as the first entries of
> the WORK, RWORK and IWORK arrays, and no error message
> related to LWORK or LRWORK or LIWORK is issued by XERBLA.

RWORK : REAL array, dimension (MAX(1,LRWORK)) [out]
> On exit, if INFO = 0, RWORK(1) returns the optimal LRWORK.

LRWORK : INTEGER [in]
> The dimension of the array RWORK.
> If COMPZ = 'N' or N <= 1, LRWORK must be at least 1.
> If COMPZ = 'V' and N > 1, LRWORK must be at least
> 1 + 3\*N + 2\*N\*lg N + 4\*N\*\*2 ,
> where lg( N ) = smallest integer k such
> that 2\*\*k >= N.
> If COMPZ = 'I' and N > 1, LRWORK must be at least
> 1 + 4\*N + 2\*N\*\*2 .
> Note that for COMPZ = 'I' or 'V', then if N is less than or
> equal to the minimum divide size, usually 25, then LRWORK
> need only be max(1,2\*(N-1)).
> 
> If LRWORK = -1, then a workspace query is assumed; the
> routine only calculates the optimal sizes of the WORK, RWORK
> and IWORK arrays, returns these values as the first entries
> of the WORK, RWORK and IWORK arrays, and no error message
> related to LWORK or LRWORK or LIWORK is issued by XERBLA.

IWORK : INTEGER array, dimension (MAX(1,LIWORK)) [out]
> On exit, if INFO = 0, IWORK(1) returns the optimal LIWORK.

LIWORK : INTEGER [in]
> The dimension of the array IWORK.
> If COMPZ = 'N' or N <= 1, LIWORK must be at least 1.
> If COMPZ = 'V' or N > 1,  LIWORK must be at least
> 6 + 6\*N + 5\*N\*lg N.
> If COMPZ = 'I' or N > 1,  LIWORK must be at least
> 3 + 5\*N .
> Note that for COMPZ = 'I' or 'V', then if N is less than or
> equal to the minimum divide size, usually 25, then LIWORK
> need only be 1.
> 
> If LIWORK = -1, then a workspace query is assumed; the
> routine only calculates the optimal sizes of the WORK, RWORK
> and IWORK arrays, returns these values as the first entries
> of the WORK, RWORK and IWORK arrays, and no error message
> related to LWORK or LRWORK or LIWORK is issued by XERBLA.

INFO : INTEGER [out]
> = 0:  successful exit.
> < 0:  if INFO = -i, the i-th argument had an illegal value.
> > 0:  The algorithm failed to compute an eigenvalue while
> working on the submatrix lying in rows and columns
> INFO/(N+1) through mod(INFO,N+1).

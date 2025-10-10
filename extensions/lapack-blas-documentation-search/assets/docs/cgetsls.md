```fortran
subroutine cgetsls (
        character trans,
        integer m,
        integer n,
        integer nrhs,
        complex, dimension( lda, * ) a,
        integer lda,
        complex, dimension( ldb, * ) b,
        integer ldb,
        complex, dimension( * ) work,
        integer lwork,
        integer info
)
```

CGETSLS solves overdetermined or underdetermined complex linear systems
involving an M-by-N matrix A, using a tall skinny QR or short wide LQ
factorization of A.

It is assumed that A has full rank, and only a rudimentary protection
against rank-deficient matrices is provided. This subroutine only detects
exact rank-deficiency, where a diagonal element of the triangular factor
of A is exactly zero.

It is conceivable for one (or more) of the diagonal elements of the triangular
factor of A to be subnormally tiny numbers without this subroutine signalling
an error. The solutions computed for such almost-rank-deficient matrices may
be less accurate due to a loss of numerical precision.


The following options are provided:

1. If TRANS = 'N' and m >= n:  find the least squares solution of
an overdetermined system, i.e., solve the least squares problem
minimize || B - A\*X ||.

2. If TRANS = 'N' and m < n:  find the minimum norm solution of
an underdetermined system A \* X = B.

3. If TRANS = 'C' and m >= n:  find the minimum norm solution of
an undetermined system A\*\*T \* X = B.

4. If TRANS = 'C' and m < n:  find the least squares solution of
an overdetermined system, i.e., solve the least squares problem
minimize || B - A\*\*T \* X ||.

Several right hand side vectors b and solution vectors x can be
handled in a single call; they are stored as the columns of the
M-by-NRHS right hand side matrix B and the N-by-NRHS solution
matrix X.

## Parameters
TRANS : CHARACTER\*1 [in]
> = 'N': the linear system involves A;
> = 'C': the linear system involves A\*\*H.

M : INTEGER [in]
> The number of rows of the matrix A.  M >= 0.

N : INTEGER [in]
> The number of columns of the matrix A.  N >= 0.

NRHS : INTEGER [in]
> The number of right hand sides, i.e., the number of
> columns of the matrices B and X. NRHS >=0.

A : COMPLEX array, dimension (LDA,N) [in,out]
> On entry, the M-by-N matrix A.
> On exit,
> A is overwritten by details of its QR or LQ
> factorization as returned by CGEQR or CGELQ.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,M).

B : COMPLEX array, dimension (LDB,NRHS) [in,out]
> On entry, the matrix B of right hand side vectors, stored
> columnwise; B is M-by-NRHS if TRANS = 'N', or N-by-NRHS
> if TRANS = 'C'.
> On exit, if INFO = 0, B is overwritten by the solution
> vectors, stored columnwise:
> if TRANS = 'N' and m >= n, rows 1 to n of B contain the least
> squares solution vectors.
> if TRANS = 'N' and m < n, rows 1 to N of B contain the
> minimum norm solution vectors;
> if TRANS = 'C' and m >= n, rows 1 to M of B contain the
> minimum norm solution vectors;
> if TRANS = 'C' and m < n, rows 1 to M of B contain the
> least squares solution vectors.

LDB : INTEGER [in]
> The leading dimension of the array B. LDB >= MAX(1,M,N).

WORK : (workspace) COMPLEX array, dimension (MAX(1,LWORK)) [out]
> On exit, if INFO = 0, WORK(1) contains optimal (or either minimal
> or optimal, if query was assumed) LWORK.
> See LWORK for details.

LWORK : INTEGER [in]
> The dimension of the array WORK. LWORK >= 1.
> If LWORK = -1 or -2, then a workspace query is assumed.
> If LWORK = -1, the routine calculates optimal size of WORK for the
> optimal performance and returns this value in WORK(1).
> If LWORK = -2, the routine calculates minimal size of WORK and
> returns this value in WORK(1).

INFO : INTEGER [out]
> = 0:  successful exit
> < 0:  if INFO = -i, the i-th argument had an illegal value
> > 0:  if INFO =  i, the i-th diagonal element of the
> triangular factor of A is exactly zero, so that A does not have
> full rank; the least squares solution could not be
> computed.

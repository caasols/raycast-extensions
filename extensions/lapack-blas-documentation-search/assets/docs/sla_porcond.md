```fortran
real function sla_porcond (
        character uplo,
        integer n,
        real, dimension( lda, * ) a,
        integer lda,
        real, dimension( ldaf, * ) af,
        integer ldaf,
        integer cmode,
        real, dimension( * ) c,
        integer info,
        real, dimension( * ) work,
        integer, dimension( * ) iwork
)
```

SLA_PORCOND Estimates the Skeel condition number of  op(A) \* op2(C)
where op2 is determined by CMODE as follows
CMODE =  1    op2(C) = C
CMODE =  0    op2(C) = I
CMODE = -1    op2(C) = inv(C)
The Skeel condition number  cond(A) = norminf( |inv(A)||A| )
is computed by computing scaling factors R such that
diag(R)\*A\*op2(C) is row equilibrated and computing the standard
infinity-norm condition number.

## Parameters
UPLO : CHARACTER\*1 [in]
> = 'U':  Upper triangle of A is stored;
> = 'L':  Lower triangle of A is stored.

N : INTEGER [in]
> The number of linear equations, i.e., the order of the
> matrix A.  N >= 0.

A : REAL array, dimension (LDA,N) [in]
> On entry, the N-by-N matrix A.

LDA : INTEGER [in]
> The leading dimension of the array A.  LDA >= max(1,N).

AF : REAL array, dimension (LDAF,N) [in]
> The triangular factor U or L from the Cholesky factorization
> A = U\*\*T\*U or A = L\*L\*\*T, as computed by SPOTRF.

LDAF : INTEGER [in]
> The leading dimension of the array AF.  LDAF >= max(1,N).

CMODE : INTEGER [in]
> Determines op2(C) in the formula op(A) \* op2(C) as follows:
> CMODE =  1    op2(C) = C
> CMODE =  0    op2(C) = I
> CMODE = -1    op2(C) = inv(C)

C : REAL array, dimension (N) [in]
> The vector C in the formula op(A) \* op2(C).

INFO : INTEGER [out]
> = 0:  Successful exit.
> i > 0:  The ith argument is invalid.

WORK : REAL array, dimension (3\*N). [out]
> Workspace.

IWORK : INTEGER array, dimension (N). [out]
> Workspace.

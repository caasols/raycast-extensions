```fortran
subroutine dsb2st_kernels (
        character uplo,
        logical wantz,
        integer ttype,
        integer st,
        integer ed,
        integer sweep,
        integer n,
        integer nb,
        integer ib,
        double precision, dimension( lda, * ) a,
        integer lda,
        double precision, dimension( * ) v,
        double precision, dimension( * ) tau,
        integer ldvt,
        double precision, dimension( * ) work
)
```

DSB2ST_KERNELS is an internal routine used by the DSYTRD_SB2ST
subroutine.

## Parameters
UPLO : CHARACTER\*1 [in]

WANTZ : LOGICAL which indicate if Eigenvalue are requested or both [in]
> Eigenvalue/Eigenvectors.

TTYPE : INTEGER [in]

ST : INTEGER [in]
> internal parameter for indices.

ED : INTEGER [in]
> internal parameter for indices.

SWEEP : INTEGER [in]
> internal parameter for indices.

N : INTEGER. The order of the matrix A. [in]

NB : INTEGER. The size of the band. [in]

IB : INTEGER. [in]

A : DOUBLE PRECISION array. A pointer to the matrix A. [in,out]

LDA : INTEGER. The leading dimension of the matrix A. [in]

V : DOUBLE PRECISION array, dimension 2\*n if eigenvalues only are [out]
> requested or to be queried for vectors.

TAU : DOUBLE PRECISION array, dimension (2\*n). [out]
> The scalar factors of the Householder reflectors are stored
> in this array.

LDVT : INTEGER. [in]

WORK : DOUBLE PRECISION array. Workspace of size nb. [out]

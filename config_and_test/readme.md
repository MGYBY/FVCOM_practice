# Some config files and test files for FVCOM

## Tricks for compiling FVCOM
- 80% of the problems could be solved by following this procedure: [Link](https://inductiva.ai/blog/article/compiling-fvcom-a-handy-toolbox-for-solving-common-issues) , but this tutorial does not seem pay attention to parallel running.
- Or follow Intel HPCKit: [Link]( https://www.bilibili.com/video/BV1ud4y12773/?spm_id_from=333.337.search-card.all.click&vd_source=05a73533c9b530f758c0381bf3bb542e). Compilation command: `make CC=icc CXX=icpc FC=ifort`.
- Error undefined reference to 'partition_'.
  - Simple solution : https://github.com/FVCOM-GitHub/FVCOM/issues/17 but that does not support parallelism.
  - This problem is related to `FLAG_411`. A better solution is to compile Metis lib offline with `gklib_path` flag.
- Finally, number of files is 533 (statistics by Dolphin).
- Testing compilation by the "Estuary" example: [file](), command: `mpirun -np 4 ./fvcom --CASENAME=tst`.

## Compilation of *NH* module
- Compile using the latest version of FVCOM 4.* or 5.*. Petsc version: 3.18.5.
- Petsc needs to be compiled using more general options `./configure  --download-metis --download-parametis --with-fc=mpif90 --with-cc=mpicc --with-cxx=mpicxx --download-hypre --download-fblaslapack  --with-precision=double -DPETSC-SKIP-ATTRIBUTE-MPI-TYPE-TAG=1 -Dfallow-argument-mismatch=1`.
- Refer to the related issue: https://github.com/FVCOM-GitHub/FVCOM/issues/26
- `mod_petsc.F` and `mod_non_hydro.F` need to be modified according to the most updated syntax of Petsc. 

# Some config files and test files for FVCOM

## Tricks for compiling FVCOM
- 80% of the problems could be solved by following this procedure: [Link](https://inductiva.ai/blog/article/compiling-fvcom-a-handy-toolbox-for-solving-common-issues) , but this tutorial does not seem pay attention to parallel running.
- Error undefined reference to 'partition_'.
  - Simple solution : https://github.com/FVCOM-GitHub/FVCOM/issues/17 but that does not support parallelism.
  - This problem is related to `FLAG_411`. A better solution is to compile Metis lib offline with `gklib_path` flag.
- Finally, number of files is 533 (statistics by Dolphin).
- Testing compilation by the "Estuary" example: [file](), command: `mpirun -np 4 ./fvcom --CASENAME=tst`.

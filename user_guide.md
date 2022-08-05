# NaluCFD User Guide
This document will guide a user through accessing the installation of _NaluCFD_ on `hpcc-cluster-36`, setting up and running a simulation, and visualizing results.

## Accessing the build

After connecting to the Stanford VPN, connect to the cluster:

```
ssh markben@hpcc-cluster-36
```

using the password found under the `password.txt` file elsewhere in this repository. 

The executable has been installed under `$HOME/codes/nalu/build/Nalu/build/` and is called `naluX`.

## Running a simulation

_NaluCFD_ has a regression suite - a set of CFD simulation cases that provide coverage of all the features of the codebase - that is run nightly. We will run one of 
these cases to verify that the installation works as expected. All the required files for the simulation have been collected into the directory `test-simulation`. 

```
cd $HOME/test-simulation
```

To run the simulation on the compute node using 16 MPI ranks:

```
sbatch job.script
```

The output files are written to `$HOME/test-simulation/output`.

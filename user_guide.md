# NaluCFD User Guide
This document will guide a user through accessing the installation of _NaluCFD_ on `hpcc-cluster-36`, setting up and running a simulation, and visualizing results.

## Accessing the build

After connecting to the Stanford VPN, connect to the HPCC cluster login node, thence to the cluster:

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

The output files are written to `$HOME/test-simulation/probe1`

## Post-processing 
### Note: all commands in this section must be run from a shell on your local computer.

In a new terminal, from your local machine, copy the output probe file from the cluster:

```
scp markben@hpcc-cluster-36:/home/markben/channel/probe1.dat .
```

Copy the post-processing script over to your local machine:

```
scp markben@hpcc-cluster-36:/home/markben/channel/nalu_post_proc.py .
```

The python script plots streamwise velocity profile for a plane channel flow at Re 1000 (based on friction number). The script requires a working python3 installation, which can be obtained from a variety of sources. Here, we use `pip`:

```
pip install python
```

**Note:** If `pip` is not already installed on your system, use the following link to download and install it: (https://pip.pypa.io/en/stable/installation/).

To install the dependencies, download the `requirements.txt` file from the top level of the repository, and run

```
pip install -r requirements.txt
```

Run the script with 

```
python3 nalu_post_proc.py
```

The output should be as below:

![Streamwise velocity plot](https://github.com/mulligatawny/me344-sum2022-project/blob/main/uplus.png)

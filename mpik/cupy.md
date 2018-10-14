# Using Cupy in GPU cluster


## About Cupy

Cupy is a python library providing NumPy-like API for GPU computation.
Thanks to (almost) the same API to NumPy, development of GPU-enabled script is very easy
(although some knowledge is necessary to build an efficient algorith).
You can even develop and debug the script in CPU environment (such as your local machine) and run it in the GPU machine, by writing your script as below

```python
try:
    import cupy as xp
except ImportError:
    import numpy as xp

x = xp.arange(6).reshape(2, 3).astype('f')
x.sum(axis=1)
```

See [official web page](https://cupy.chainer.org/) for the details.


## Requirement

Of course, we need GPUs in the computational environment.
In MPI-K, [**lfg**](https://www.mpi-hd.mpg.de/mpi/en/computing/software-on-the-cluster/cluster-configuration/) provides Tesla M2090 (today: 14.10.2018).

[CUDA](https://developer.nvidia.com/cuda-zone) must be installed in the system.
**lfg** now has CUDA-9.2.


## Building a virtual environment with Anaconda.

I recommend to build a virtual environment for Cupy, so that the compilation of the library does not affect any existing scripts.
[*Anaconda*](https://www.anaconda.com/) provides convenient functionalities to build virtual environments.
We would use **anaconda** for Python environment.

### Installing Anaconda

There are several versions of Anaconda distributions.
Typically, people like to use [*Anaconda distribution*](https://www.anaconda.com/download/#linux) which includes many widely used libraries.
However, it consumes a lot of storages. So we now install [*Miniconda*](https://conda.io/miniconda.html) that includes minimum amount of libraries.

First login to the **lfg** server,
```bash
ssh [username]@lfg1
```
(replace [username] by your account)

Then, download miniconda and run the downloaded script,
```bash
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh
bash miniconda.sh -b -p $HOME/miniconda
```
It creates `miniconda` directory in your home directory.

In order to run Python of miniconda environment, we need to add the directory to `$PATH`.
We may want use miniconda instead of the natively installed python, it would be a good idea to put it in your `.bashrc` file.

```bash
echo '# for anaconda distribution' >> $HOME/.bashrc
echo 'export PATH="$HOME/miniconda/bin:$PATH"' >> $HOME/.bashrc
```

Now, `python` command uses **Anaconda**'s python instead of the natively installed one.


### Building a virtual environment for Cupy

In order to create a virtual environment with Anaconda, use `conda` command as below,
```bash
conda create -n cupy python==3.7
```
This creates a virtual environment named **cupy** with python 3.7.

In order to activate this, type the below
```bash
source activate cupy
```
Now, `(cupy)` is shown in the terminal.

![termninal](figs/virtual_env.png)

(Note, as I customized my `.bashrc` file so that the terminal looks Ubuntu-like, your terminal looks different (not colored, etc...). Please just find '(cupy)' is in the head of the command line.)

To deactivate the virtual environment,
```bash
source deactivate
```
then, you will be back to the root environment and `(cupy)` in the terminal will be gone.


## Installing Cupy in the virtual environment

### Install dependent libraries

Cupy depends on some libraries, *numpy*, *cython*, *mock*.
We need to install them before installing Cupy.

In Anaconda distribution, there are multiple options to install libraries.
For example, to install numpy, you can do either
+ `conda install numpy`
+ `pip install numpy`

In many cases, the use of `conda` command is better because anaconda provides optimized wheels for many systems.
For example, `conda install numpy` installs *numpy* that is optimized with [*MKL* (math kernel libary)](https://software.intel.com/en-us/mkl) by Intel.
However, anaconda does not support all the libraries. Cupy is not registered.

Therefore, we would install *numpy*, *cython*, *mock* (and if you want, also *scipy*, *matplotlib*, *ipython*) via Anaconda.

```bash
source activate cupy
conda install numpy cython mock scipy matplotlib ipython
```

### Install Cupy

Now we are ready to install Cupy.
Just use `pip` command for this

```bash
pip install cupy
```
(It will take several minutes. Take a cup of coffee)

Let's test the installation.
Lauch the interactive console,
```bash
python
```
and type
```python
>>> import cupy as cp
>>> cp.arange(6).reshape(2, 3).sum(axis=1)
array([ 3, 12])
```
If no errors, then you completed the installation.
Congratulations! 

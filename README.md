<div align="center">
	<img src="http://socsci.uci.edu/~jkrichma/CARL-Logo-small.jpg" width="300"/>
</div>

# CARLsim 5

[![Build Status](https://travis-ci.org/UCI-CARL/CARLsim5.svg?branch=master)](https://travis-ci.org/UCI-CARL/CARLsim5)
[![Coverage Status](https://coveralls.io/repos/github/UCI-CARL/CARLsim5/badge.svg?branch=master)](https://coveralls.io/github/UCI-CARL/CARLsim5?branch=master)
[![Docs](https://img.shields.io/badge/docs-v5.0.0-blue.svg)](http://uci-carl.github.io/CARLsim5)
[![Google group](https://img.shields.io/badge/Google-Discussion%20group-blue.svg)](https://groups.google.com/forum/#!forum/carlsim-snn-simulator)

CARLsim is an efficient, easy-to-use, GPU-accelerated library for simulating large-scale spiking neural network (SNN) models with a high degree of biological detail. CARLsim allows execution of networks of Izhikevich spiking neurons with realistic synaptic dynamics on both generic x86 CPUs and standard off-the-shelf GPUs. The simulator provides a PyNN-like programming interface in C/C++, which allows for details and parameters to be specified at the synapse, neuron, and network level.

<!-- New features in CARLsim 5 include:
- Multi-GPU support
- Hybrid CPU/GPU mode
- Multi-compartment and LIF point neurons -->

If you use CARLsim or PyCARL in your research, please cite our papers [CARLsim](https://www.socsci.uci.edu/~jkrichma/Chou-Kashyap-CARLsim4-IJCNN2018.pdf) and [PyCARL](https://arxiv.org/abs/2003.09696).

Chou*, T.-S., Kashyap*, H.J., Xing, J., Listopad, S., Rounds, E.L., Beyeler, M., Dutt, N., and Krichmar, J.L. (2018). "CARLsim 4: An Open Source Library for Large Scale, Biologically Detailed Spiking Neural Network Simulation using Heterogeneous Clusters." In Proceedings of IEEE International Joint Conference on Neural Networks (IJCNN), pp. 1158-1165.

Balaji, A., Adiraju, P., Kashyap, H. J., Das, A., Krichmar, J. L., Dutt, N. D., & Catthoor, F. (2020). PyCARL: A PyNN Interface for Hardware-Software Co-Simulation of Spiking Neural Network. arXiv preprint arXiv:2003.09696. (To appear in IJCNN 2020)




## News
We released PyCARL which is an interface of CARLsim to the pyNN framework! Please check [here](https://github.com/UCI-CARL/CARLsim5/tree/master/pyCARL) for more details.


## Installation

Detailed instructions for installing the latest stable release of CARLsim on Mac OS X / Linux
can be found in our [User Guide](http://uci-carl.github.io/CARLsim5/ch1_getting_started.html).

### Linux/MacOS

#### For Beginner

1. Download CARLsim 5 zip file by clicking on the `Clone or download` box in the top-right corner.

2. Unzip the source code.

3. Go into `CARLsim5` folder
   ```
   $ cd CARLsim5
   ```

4. Make and install
   ```
   $ make
   $ make install
   ```

5. Verify installation
   ```
   $ cd ~
   $ ls
   ```
   You will see `CARL` folder

6. Go back to `CARLsim5` folder and start your own project! The "Hello World" project is a goot starting point for this.
   Make sure it runs:
   ```
   $ cd CARLsim5
   $ cd projects/hello_world
   $ make
   $ ./hello_world
   ```

#### Ubuntu 20.04+ compatibility
GCC & G++ versions 8.0 or below are needed for CARLsim compatibility and this must manually be installed on Ubuntu 20.04+. For example for version 7:
   ```
   $ sudo apt install gcc-7 g++7
   ```
Use update-alternatives to switch versions. For example for GCC, (substitute G++ for GCC when switching G++):
   ```
   $ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7
   $ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 11
   $ sudo update-alternatives --config gcc
   ```
Then type selection for GCC 7. Once CARLsim is installed run update-alternatives to switch back to normal versions of GCC and G++ for other software.

#### For Advanced User and Developer

1. Fork CARLsim 5 by clicking on the `Fork` box in the top-right corner.

2. Clone the repo, where `YourUsername` is your actual GitHub user name:
   ```
   $ git clone --recursive https://github.com/UCI-CARL/CARLsim5.git
   $ cd CARLsim5
   ```
   Note the `--recursive` option: It will make sure Google Test gets installed.

3. Choose between stable release and latest development version:
   - For the latest development branch, you are already on the right branch (`master`).
   - For stable release, choose from https://github.com/UCI-CARL/CARLsim5/releases

4. Choose the installation directory: By default, the CARLsim library lives in `~/CARL/lib`, and CARLsim include files live in `~/CARL/include`.
    You can overwrite these by exporting an evironment variable called `CARLSIM5_INSTALL_DIR`:
    ```
    $ export CARLSIM5_INSTALL_DIR=/path/to/your/preferred/dir
    ```
    or
    ```
    $ export CARLSIM5_INSTALL_DIR=/usr/local
    ```
    if you want to install CARLsim library for all users.
    
    Also set the following evironment variable:
    ```
    $ export CUDA_PATH=/path/to/CUDA
    ```
    By default CUDA is installed to `/usr/local/cuda` in Linux systems.

5. Make and install:
   ```
   $ make -j4
   $ sudo -E make install
   ```
   Note the `-E` flag, which will cause `sudo` to remember the `CARLSIM5_INSTALL_DIR`.

7. In order to make sure the installation was successful, you can run the regression suite:

   ```
   $ make test
   $ ./carlsim/test/carlsim_tests
   ```
   
8. Start your own project! The "Hello World" project is a goot starting point for this.
   Make sure it runs:

   ```
   $ cd projects/hello_world
   $ make
   $ ./hello_world
   ```

   You can easily create your own project based on this template using the `init.sh` script:

   ```
   $ cd projects
   $ ./init.sh project_name
   ```
   where `project_name` is the name of your new project.
   The script will copy all files from `hello_world/` to `project_name/`, make all required
   file changes to compile the new project, and add all new files to git.

#### Using nvidia docker
1. Using CARLsim5 on an Nvidia-docker image follows the instructions above. Only important thing to keep in mind is to copy the $CUDA_PATH/samples directory to the docker, which does not come with the nvidia docker image. CARLsim5 uses "helper_functions.h" from the library.

#### Using CMake

1. Obtatin `CARLsim5`'s source code.

2. Create a build directory (you can make it anywhere)

   ```
   $ mkdir .build
   ```

3. Proceed into build directory and do configuration:

   ```
   $ cd .build
   $ cmake \
       -DCMAKE_BUILD_TYPE=Release \
       -DCMAKE_INSTALL_PREFIX=/usr/local/carlsim \
       -DCARLSIM_NO_CUDA=OFF \
       <path-to-carlsim>
   ```

   As you can see `cmake` accepts several options `-D<name>=<value>`: they define cmake variables.
   `CMAKE_BUILD_TYPE=Release` means that we are going to build release version of the library.
   If you need debug version then pass `Debug`.
   `CMAKE_INSTALL_PREFIX` specifies a directory which we are going to install the library into.
   `CARLSIM_NO_CUDA` switches on/off support of CUDA inside the library.
   `<path-to-carlsim>` must be replaced with the path to the CARLsim5's source directory.

4. Build:

   ```
   make -j <jobs-num>
   ```
   
   Set `<jobs-num>` to the number of logical processors your computer has plus one,
   this will employ parallel building.

5. Install:

   ```
   make install
   ```
   


## Prerequisites

CARLsim 5 comes with the following requirements:
- (optional) CMake 3.0 or higher in case you want to build it using CMake.
- (optional) CUDA Toolkit 6.0 or higher. For platform-specific CUDA installation instructions, please navigate to 
  the [NVIDIA CUDA Zone](https://developer.nvidia.com/cuda-zone).
  This is only required if you want to run CARLsim in `GPU_MODE`. Make sure to install the 
  CUDA samples, too, as CARLsim relies on the file `helper_cuda.h`.
- (optional) A GPU with compute capability 2.0 or higher. To find the compute capability of your device please 
  refer to the [CUDA article on Wikipedia](http://en.wikipedia.org/wiki/CUDA).
  This is only required if you want to run CARLsim in `GPU_MODE`.
- (optional) MATLAB R2014a or higher. This is only required if you want to use the Offline Analysis Toolbox (OAT).

As of CARLsim 3.1 it is no longer necessary to have the CUDA framework installed. However, CARLsim development 
will continue to focus on the GPU implementation.

The latest release was tested on the following platforms:
- Ubuntu 16.04
- Mac OS X 10.11 (El Capitan)

The latest release has at least partial compatibility on the following platforms:
- Ubuntu 20.04+
  The majority but not all test cases have been found to pass with these OS distributions.

## In case of a pthread error

If one encounters a "nvcc fatal: Unknown option '-pthread'" error a workaround for fixing this is to change the code in carlsim/configure.mk from "-pthread" to "-Xcompiler -pthread". This is not included in the standard project code because this fix is platform dependent and may not work on all systems. See [reference](https://gitlab.kitware.com/cmake/cmake/-/issues/18008) for additional details.
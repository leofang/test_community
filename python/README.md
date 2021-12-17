# cuQuantum Python

## Documentation

Please visit [TBD](https://docs.nvidia.com/cuda/cuquantum/python/index.html).

## Building

### Requirements

Build-time dependencies of the cuQuantum Python package and some versions that
are known to work are as follows:

* CUDA Toolkit 11.4+
* cuQuantum 0.1.0
* cuTENSOR 1.4.0+
* Cython - e.g. 0.29.21

### Install cuQuantum Python from conda-forge

If you already have a Conda environment set up, it is the easiest to install cuQuantum Python from the conda-forge channel:
```
conda install -c conda-forge cuquantum-python
```
The Conda solver will address all dependencies for you.

### Install cuQuantum Python from source

To compile and install cuQuantum Python from source, please follow the steps below:

1. Set `CUDA_PATH` to point to your CUDA installation
2. Set `CUQUANTUM_ROOT` to point to your cuQuantum installation
3. Set `CUTENSOR_ROOT` to point to your cuTENSOR installation
4. Make sure CUDA, cuQuantum and cuTENSOR are visible in your `LD_LIBRARY_PATH`
5. Run `pip install -v .`

Notes:
- For the `pip install` step, adding the `-e` flag after `-v` would allow installing the package in-place (i.e., in "editable mode" for testing/developing).
- If `CUSTATEVEC_ROOT` and `CUTENSORNET_ROOT` are set (for the cuStateVec and the cuTensorNet libraries, respectively), they overwrite `CUQUANTUM_ROOT`.
- For local development, set `CUQUANTUM_IGNORE_SOLVER=1` to ignore the dependency on the `cuquantum` wheel.


## Running

### Requirements

Runtime dependencies of the cuQuantum Python package include:

* An NVIDIA GPU with compute capability 7.0+
* Driver: Linux (4xx.xx.xx or later) ***TODO***
* CUDA Toolkit 11.4+
* cuQuantum 0.1.0
* cuTENSOR 1.4.0+
* NumPy v1.17+
* CuPy v9.5.0+
* PyTorch v1.10+ (optional)

If you install everything from conda-forge, the dependencies are taken care for you (except for the driver).

If you build cuQuantum Python from source, please make sure the paths to the cuQuantum and cuTENSOR libraries are added
to your `LD_LIBRARY_PATH` environment variable.

Known issues:
- If a system has multiple copies of cuTENSOR, one of which is installed in a default system path, the Python runtime could pick it up despite cuQuantum Python is linked to another copy installed elsewhere, potentially causing a version-mismatch error. The proper fix is to remove cuTENSOR from the system paths to ensure the visibility of the proper copy. **DO NOT ATTEMPT** to use `LD_PRELOAD` to overwrite it --- it could cause hard to debug behaviors!
- In certain environments, if PyTorch is installed `import cuquantum` could fail (with a segmentation fault). It is currently under investigation and a temporary workaround is to import `torch` before importing `cuquantum`.

### Samples

Samples for demonstrating the usage of both low-level and high-level Python APIs are
available in the `samples` directory. The low-level API samples are 1:1 translations of the corresponding
samples written in C. The high-level API samples demonstrate pythonic usages of the cuTensorNet
library in Python.


## Testing

If pytest is installed, run `pytest tests` in the Python source root directory would
run all tests.

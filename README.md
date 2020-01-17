# Cubik

A C++ tensor library with built-in transparency for CPU and GPU. 

Cubik is inspired by [NumPy](https://numpy.org/) when it comes to naming convention, but we rely on highly-optimized libraries such as:

- [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)
- [Intel MKL](https://software.intel.com/en-us/mkl)
- [Intel MKL-DNN](https://github.com/intel/mkl-dnn)
- [NVIDIA CUDA](https://developer.nvidia.com/cuda-zone)
- [NVIDIA cuBlas](https://docs.nvidia.com/cuda/cublas/index.html)
- [NVIDIA cuDNN](https://developer.nvidia.com/cudnn)


## Prerequisites

- gcc with C++11
- cmake
- Anaconda/Miniconda

### Linux

```
sudo apt-get install build-essential cmake conda
```

### Mac OS

```
brew install cmake
brew cask install anaconda
```

### Windows

```
1. Uninstall Windows
2. Install Linux
3. Read Linux steps
```

## Installation

The required libraries are easy-to-install using the conda package manager:

Create and activate the environment:

```
conda env create -f environment.yml
conda activate cubik-env
```

Build from source:

```
mkdir build
cd build
cmake ..
make -j$(num_cores)
```

> Note: These steps are for Linux and Mac OS
> To known the number of logical cores type: `nproc` (linux) or `sysctl -n hw.logicalcpu` (mac os)

### Backend support

#### GPU (CUDA) support 

If you have CUDA installed, you can build Cubik with GPU support by adding `-DBACKEND=cuda` to your cmake options.

#### GPU (cuDNN) support

Some of Cubik's functionality (e.g. conv2d) depends on the [NVIDIA cuDNN libraries](https://developer.nvidia.com/cudnn).
If CMake is unable to find cuDNN automatically, try setting CUDNN_ROOT, such as `-DCUDNN_ROOT="/path/to/CUDNN"` 

#### CPU (MKL) support

Cubik can leverage Intel's MKL library to speed up computation on the CPU. 

To use MKL, include the following cmake option: 

```
-DMKL=TRUE
```

If CMake is unable to find MKL automatically, try setting MKL_ROOT, such as:

```
-DMKL_ROOT="/path/to/MKL"
```

### Additional flags

#### Eigen3

At the core of many numerical operations, we use [Eigen3](http://eigen.tuxfamily.org/index.php?title=Main_Page).
If CMake is unable to find Eigen3 automatically, try setting `EIGEN3_INCLUDE_DIR`, such as:

```
-DEIGEN3_INCLUDE_DIR=/path/to/eigen
```


## Why Cubik?

When I started to work on the [EDDL](https://github.com/deephealthproject/eddl), I realized that most of the C++ libraries for linear algebra were designed for 1 and 2D tensors. Additionally, most of them didn't offer hardware transparency.

Since we could not build a high-performance library that matched [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) or [cuBlas](https://docs.nvidia.com/cuda/cublas/index.html) at the benchmarks, we decided to write a wrapper that at least could provide us with hardware-transparency.

> Notes:
> 1. Many deep learning libraries have a C++ API but due to the goals of the main project, the use of one these was out of the question.
> 2. Some libraries met our requirements such as [CuPy](https://cupy.chainer.org/), but we needed to write a C++ tensor library with support for dynamic neural networks.

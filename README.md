# Cubik

A C++ tensor library with built-in transparency for CPU and GPU, based on Eigen and cuBlas.

## Why?

When I started to work on the [EDDL](https://github.com/deephealthproject/eddl), I realized that most of the C++ libraries for linear algebra were designed for 1 and 2D tensors. Addionally, most of them didn't offer hardware transparency.

Since we could not build a high-performance library that matched [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) or [cuBlas](https://docs.nvidia.com/cuda/cublas/index.html) at the benchmarks, we decided to write a wrapper that at least could provide us with hardware-transparency.

> Notes:
> 1. Many deep learning libraries have a C++ API but due to the goals of the main project, the use one of these was out of the question.
> 2. There were libraries that met our requirements such as [CuPy](https://cupy.chainer.org/), but we needed to write a C++ tensor library with support for dynamic neural networks.

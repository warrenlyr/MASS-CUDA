# MASS-CUDA
**Version v0.7.0 | Last Updated: March 10th, 2024**

**Repo on Bitbucket**: https://bitbucket.org/mass_library_developers/mass_cuda_core/src/main/

Welcome to the repository of the MASS CUDA Library. This extension of the MASS library, found [here](https://depts.washington.edu/dslab/MASS/), is specifically designed to facilitate high-performance agent-based model simulations utilizing General-Purpose Graphics Processing Unit (GPGPU), with a focus on Nvidia CUDA technology. The library is currently under active development and is presently not suited for production environments.

## Overview
The MASS (Multi-Agent Spatial Simulation) is an open-source framework aimed at the efficient parallelization of agent-based simulations. The suite targets applications across a wide array of fields, including but not limited to physical, biological, social, and strategic domains. It is particularly useful for simulations requiring complex multi-entity interactions, with applicable scenarios ranging from molecular dynamics and neural networks to urban planning.

The MASS suite includes two primary versions developed for CPU-based computation:

- [MASS C++ Library](https://bitbucket.org/mass_library_developers/mass_cpp_core/src/master/)
- [MASS Java Library](https://bitbucket.org/mass_library_developers/mass_java_core/src/master/)

These versions operate on CPU-based computations. The MASS CUDA library extends the capabilities of MASS to support simulations on GPGPU, specifically leveraging Nvidia CUDA for enhanced parallel computing efficiency.

The objective of the MASS CUDA library is to provide a scalable, high-performance framework for the development of agent-based simulations on Nvidia GPUs. It is designed to be accessible to researchers and developers, including those not familiar with CUDA programming, through a high-level API.

More information about MASS can be found out the University of Washington Distributed Systems Lab [Homepage](http://depts.washington.edu/dslab/MASS).

## User Manual

The library is in a phase of rapid development, with the current release being version 0.7.0. This version introduces significant improvements in data structures and algorithms, enhancing performance exponentially. The user manual, available on the project's [Wiki page](https://bitbucket.org/mass_library_developers/mass_cuda_core/wiki/), offers comprehensive guidance on utilizing the MASS CUDA library for developing simulations on Nvidia GPUs.

## Getting Started
### Prerequisites
- **NVCC** (CUDA Compiler) must be in your system’s $PATH. This is pre-configured for users on UW's Juno server.
- **C++14** compatibility is required for building the MASS CUDA library. Please ensure your compiler is updated accordingly.

### Development Setup
1. Development Environment: Execute `make develop` in the root directory to install all necessary dependencies for library development and testing.
2. Building the Library: After modifications, use `make build` to compile the library.
3. Testing: Run `make test` to execute unit tests using the [Google Test](https://google.github.io/googletest/) framework, located in the test directory.

### Installing the MASS CUDA Library
While the `install-mass` Makefile target is not essential for library development, it aids application developers in installing the MASS CUDA library and its dependencies into their `include` and `libs` directories.

Explore example applications using the MASS CUDA library in [this repository](https://bitbucket.org/mass_application_developers/mass_cuda_appl/src/main/). The [Application Template](https://bitbucket.org/mass_application_developers/mass_cuda_appl/src/main/AppTemplate/) is a great starting point for developing your applications. The [Game of Life](https://bitbucket.org/mass_application_developers/mass_cuda_appl/src/warren_develop/GameOfLife/GameOfLife_PlaceV2/) is a simple example of an application using the MASS CUDA library, which you can use as a reference.

### Developer Documentation
An updated developer manual for the MASS CUDA library is pending. In the meantime, the [MASS C++ Library Developer Manual](https://depts.washington.edu/dslab/MASS/docs/MassCpp.pdf) can provide valuable insights into the MASS library framework. We'll update this section as more documentation becomes available.



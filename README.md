# MASS-CUDA
**Version v0.7.1 | Last Updated: March 13th, 2024**

Source repo: https://bitbucket.org/mass_library_developers/mass_cuda_core/src/main/

Welcome to the repository of the MASS CUDA Library. This extension of the MASS library, found [here](https://depts.washington.edu/dslab/MASS/), is specifically designed to facilitate high-performance agent-based model simulations utilizing General-Purpose Graphics Processing Unit (GPGPU), with a focus on Nvidia CUDA technology. The library is currently under active development and is presently not suited for production environments.

- [Overview](#overview)
- [Introduction](#introduction)
    - [Why Agent-Based Modeling?](#why-agent-based-modeling)
        - [Parallel and Distributed Computing: The Basics](#parallel-and-distributed-computing-the-basics)
        - [The Reality of Scalability and Communication Overhead](#the-reality-of-scalability-and-communication-overhead)
        - [Agent-based Modeling as a Solution](#agent-based-modeling-as-a-solution)
    - [What is MASS, In Short?](#what-is-mass-in-short)
    - [What is MASS CUDA?](#what-is-mass-cuda)
- [User Manual](#user-manual)
- [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Development Setup](#development-setup)
    - [Installing the MASS CUDA Library](#installing-the-mass-cuda-library)
    - [Developer Documentation](#developer-documentation)
- [Contact and Contributions](#contact-and-contributions)

## Overview
The MASS (Multi-Agent Spatial Simulation) is an open-source framework aimed at the efficient parallelization of agent-based simulations. The suite targets applications across a wide array of fields, including but not limited to physical, biological, social, and strategic domains. It is particularly useful for simulations requiring complex multi-entity interactions, with applicable scenarios ranging from molecular dynamics and neural networks to urban planning.

The MASS suite includes two primary versions developed for CPU-based computation:

- [MASS C++ Library](https://bitbucket.org/mass_library_developers/mass_cpp_core/src/master/)
- [MASS Java Library](https://bitbucket.org/mass_library_developers/mass_java_core/src/master/)

These versions operate on CPU-based computations. The MASS CUDA library extends the capabilities of MASS to support simulations on GPGPU, specifically leveraging Nvidia CUDA for enhanced parallel computing efficiency.

The objective of the MASS CUDA library is to provide a scalable, high-performance framework for the development of agent-based simulations on Nvidia GPUs. It is designed to be accessible to researchers and developers, including those not familiar with CUDA programming, through a high-level API.

More information about MASS can be found out the University of Washington Distributed Systems Lab [Homepage](http://depts.washington.edu/dslab/MASS).

## Introduction
### Why Agent-Based Modeling?
#### Parallel and Distributed Computing: The Basics
In parallel and distributed computing, the strategy of utilizing multiple machines, or computing nodes, to tackle a problem is common. The essence of this approach is to divide a problem into smaller parts, each of which is handled by a different computing node simultaneously. Theoretically, if a problem is divided among four nodes, it should take roughly a quarter of the time to solve, assuming perfect efficiency. The expectation is that by increasing the number of computing nodes, the time to solve the problem decreases, improving performance.

[![Parallel Computing](./assets/parallel_computing%20(1).png)](https://pythonnumericalmethods.berkeley.edu/notebooks/chapter13.01-Parallel-Computing-Basics.html)

#### The Reality of Scalability and Communication Overhead
However, the improvement in performance isn't always proportional to the number of added computing nodes. One primary reason is the communication overhead among the nodes. As the number of nodes increases, so does the requirement for communication between them, leading to significant overhead. Two main issues contribute to this overhead:
1. **Data Distribution**: Initially, data must be distributed to each computing node, a process that inherently lacks parallelism. With more nodes, the data distribution phase becomes more cumbersome and time-consuming.
2. **Inter-node Communication**: Each node may require data or state information from its neighbors to proceed with its computation. This necessitates constant communication between nodes, increasing linearly with the number of nodes and adding to the overhead.

[![Distributed Computing](./assets/distributed_computing.gif)](https://www.sciencedirect.com/topics/computer-science/distributed-computing)

#### Agent-based Modeling as a Solution
Agent-based modeling (ABM) offers an innovative approach to addressing the scalability and communication challenges inherent in traditional parallel and distributed computing models. ABM focuses on defining autonomous agents with their own behaviors and rules, which interact within a defined environment. Here’s why and how ABM is effective:

- **Data Locality**: In ABM, data is distributed to nodes but remains stationary. Computation, in the form of agents, moves to where the data resides. This significantly reduces the need for data transfer, as agents process data locally where possible.
- **Reduced Communication Overhead**: Since agents operate on local data and only interact with their immediate environment, the volume of data that needs to be transferred between nodes is minimized. Agents only communicate when necessary, based on their interactions within the simulation environment, which is often less data-intensive than constantly syncing state information across nodes.
- **Scalability**: By minimizing communication overhead and keeping data localized, ABM can scale more effectively than traditional parallel computing approaches. The addition of more computing nodes does not exponentially increase the communication burden, allowing for more linear scalability under the right conditions.

### What is MASS, In Short?
The Multi-Agent Spatial Simulation (MASS) library is a specialized framework designed for the development of agent-based models within the realms of parallel and distributed computing. It serves as a tool to efficiently create, manage, and simulate agents and their interactions within a defined environment. MASS is structured around two fundamental concepts: **Agent** and **Place**.

- **Place**: This component acts as the spatial container or environment where agents operate. It holds data or attributes relevant to the simulation and defines the spatial relationships, including the identification of neighboring places. This structural design facilitates the exchange of information among places, making it convenient for an agent to access and retrieve data about its immediate surroundings or neighbors.

- **Agent**: This is the dynamic, computational unit within MASS. Agents contain user-defined logic or functions that dictate their behavior within the simulation. They are mobile and can move from one place to another, executing computations that can influence both their state and the state of the places they interact with. The mobility of agents allows for a dynamic simulation environment where interactions and behaviors evolve over time.

To streamline the management of agents and places, MASS introduces two classes: Agents and Places. These serve as containers or managers for agent and place objects, respectively. They offer a high-level API through which users can interact with and manipulate the agent-based model. This design not only simplifies the development process but also enhances the scalability and flexibility of simulations, allowing researchers and developers to focus on the domain-specific aspects of their models without getting bogged down by the underlying computational complexities.

One example to help illustrate the concept of MASS is the traffic simulation. In this scenario, places represent the road segments, intersections, or traffic nodes, while agents represent the vehicles. The agents move from one place to another, interacting with the environment and other agents, simulating the dynamics of traffic flow. The places contain data such as traffic density, speed limits, and road conditions, which influence the behavior of the agents. This is just one of many applications where MASS can be effectively utilized to model complex systems and their interactions.

### What is MASS CUDA?
The MASS library has been equipped with functions like `Places.exchangeAll()`, `Places.callAll()`, and `Agents.manageAll()`, designed to operate across all Place or Agent objects concurrently. These functions are inherently parallel, making them ideal candidates for acceleration using General-Purpose Graphics Processing Unit (GPGPU) technology. This is the premise behind the development of MASS CUDA.

MASS CUDA enhances the library by enabling it not just to run on distributed memory systems but also to exploit the computational prowess of GPUs, particularly Nvidia GPUs with CUDA technology. Unlike a conventional computing mode where a single CPU handles computations, a GPU boasts thousands of cores capable of executing many threads simultaneously. This architecture allows for the massively parallel processing of Place and Agent computations, significantly accelerating the execution of agent-based models.

Lack of familiarity with GPGPU doesn't pose a barrier to leveraging the MASS CUDA library. This version is crafted to ensure ease of use and accessibility for researchers and developers, even those who may not have prior experience with CUDA. Nonetheless, a deeper understanding of CUDA programming can be advantageous, enabling further optimization of your code for enhanced performance.

## User Manual

The library is in a phase of rapid development, with the current release being version v0.7.1. This version introduces significant improvements in data structures and algorithms, enhancing performance exponentially. The user manual, available on the project's [Wiki page](https://bitbucket.org/mass_library_developers/mass_cuda_core/wiki/), offers comprehensive guidance on utilizing the MASS CUDA library for developing simulations on Nvidia GPUs.

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

## Contact and Contributions
For inquiries or contributions to the MASS CUDA Library project, please contact:

**Professor Munehiro Fukuda (Project Owner):**
- Email: [mfukuda@uw.edu](mailto:mfukuda@uw.edu)

**Warren Liu (Active Developer):**
- Email: [yiranluw@uw.edu](mailto:yiranluw@uw.edu)

**All Contributors:**
- [MASS CUDA Library Contributors](https://depts.washington.edu/dslab/MASS/#:~:text=3.%20MASS%20CUDA%3A%20GPU%20Platform%20for%20Agent%2DBased%20Models)

Explore example applications using the MASS CUDA library in [this repository](https://bitbucket.org/mass_application_developers/mass_cuda_appl/src/main/). The [Application Template](https://bitbucket.org/mass_application_developers/mass_cuda_appl/src/main/AppTemplate/) is a great starting point for developing your applications. The [Game of Life](https://bitbucket.org/mass_application_developers/mass_cuda_appl/src/warren_develop/GameOfLife/GameOfLife_PlaceV2/) is a simple example of an application using the MASS CUDA library, which you can use as a reference.

### Developer Documentation
An updated developer manual for the MASS CUDA library is pending. In the meantime, the [MASS C++ Library Developer Manual](https://depts.washington.edu/dslab/MASS/docs/MassCpp.pdf) can provide valuable insights into the MASS library framework. We'll update this section as more documentation becomes available.



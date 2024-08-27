# Checkpointing in DOLFINx using ADIOS2

This project is dedicated to the implementation of native checkpointing in
the FEniCS project which is a popular open-source computing platform
for solving partial differential equations (PDEs) with
the finite element method (FEM).
Large scale simulation of scientific and engineering problems requires
high performance and distributed memory systems.
Computing resources and time are not unlimited and efficient usage of the
computing resources calls for scalable and flexible checkpointing which
is the ability to start, pause and resume simulations, thus saving energy
consumption and money.

The common use case of checkpointing is for visualization, which calls for
mapping the data structures of the scientific simulation softwares to the
dedicated file systems, for example VTX and VTKHDF etc, which can then be
recognized by the visualization tools like Paraview and ViSit.
Other use cases include:
(i) flexible start and stop of the simulation,
(ii) control over simulation in case of diverging iterative solvers,
(iii) for aggregated post processing and
(iv) in adjoint computations.

The goals of this GSoC project and its extended future work is based on the
inclusion of the prototype checkpointing framework
[ADIOS4DOLFINx](https://jsdokken.com/adios4dolfinx/README.html,)
into DOLFINx the main component of the FEniCS project.
ADIOS4DOLFINx ([Dokken, 2024](https://github.com/openjournals/joss-papers/blob/joss.06451/joss.06451/10.21105.joss.06451.pdf)) implements several variations of checkpointing using the state of
the art *The Adaptable Input Output (I/O) System* called
[ADIOS2](https://csmd.ornl.gov/software/adios2).

In the current state of the project, we have only focussed on the N-to-M checkpointing,
i.e., writing (saving) on N processors and reading (loading) on M processors.
This is useful since, postprocessing and visualization of the simulation is generally a
distinct part of the workflow with dedicated softwares which need to consume the data of
the simulation from a compute cluster and may usually be performed locally with different
number of processors.

This checkpointing functionality is developed as a core feature of the DOLFINx.
Since DOLFINx is a C++ library with a Python wrapper,
this feature is implemented in C++ with appropriate APIs
exposed to the python user using nanobind.

N-to-N optimized version of checkpointing with the partition information stored and
snapshot checkpointing are deferred for future.

The current state of the work of this GSoC project consists of the following *pull requests* (PRs):
TODO: short summary?

1. Write and read mesh using ADIOS2 [(open)](https://github.com/FEniCS/dolfinx/pull/3291)
2. Write and read meshtags using ADIOS2 [(open)](https://github.com/FEniCS/dolfinx/pull/3324)
3. Write functions using ADIOS2 [(open)](https://github.com/FEniCS/dolfinx/pull/3368)

The mentors for this GSoC project were Jørgen S. Dokken and Jack S. Hale.

## Details

TODO: Write up details of the whole project split across the following chapters/blogs (try jupyterbook)

The details of the project are discussed in the following chapters:

 - [Chapter 1](chapter1.md) : Introduction to DOLFINx and setting up the development environment
 - [Chapter 2](chapter2.md) : Opening up the "black box" DOLFINx and experimenting with VTKHDF and ADIOS2
 - [Chapter 3](chapter3.md) : Checkpointing module (part 1): Mesh
 - [Chapter 4](chapter4.md) : Checkpointing module (part 2): Meshtags
 - [Chapter 5](chapter5.md) : Checkpointing module (part 3): Functions
 - [Chapter 6](chapter6.md) : Future work

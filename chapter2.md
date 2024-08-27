# Chapter 2 : Opening up the "black box" DOLFINx and experimenting with VTKHDF and ADIOS2

## Tinkering with DOLFINx
TODO: write about

Use of parallel debug to go through the DOLFINx objects and data structures
Use of networkx python graph library to understand, geometry and topology dof local
and global enumeration and visualization of the partitions.
NOTE: There already exists a more mature tool febug to do the same and much more.

## Experiment with writing DOLFINx data to VTKHDF format for visualization in paraview

## ADIOS2
Coming back to the main goal of this GSoC project which was to use ADIOS2 library to
create native checkpointing for DOLFINx, we give a brief introduction of ADIOS2.
ADIOS2 is an open-source framework that provides solutions for scalable
parallel I/O for scientific data management, with a unified application
programming interface (API) for various backends.
The ADIOS2 concepts of typical scientific data handling is done via

 - Variable: which are n-dimensional data objects with premitive data types
 - Attribute: defines the associated meta-data
 - Step: an abstraction for sequence of quantities, eg., time-step, iteration-step, etc
 - Engine: the unified interface to different backends handling different file types, data transfer over networks, etc
 - Operator: data compression task via third party libraries.

Moreover, it is possible to have an hardware aware fine tuning of
parameters of ADIOS2 though run time configuration files.
We use only a tiny subset of the features of the ADIOS2 library.
Our target engine types are BP4, BP5 and HDF5, and our unit tests have successfully passed for BP4 and BP5.
We write data from (multiple) processes to global arrays and read back chunks to reconstruct the DOLFINx objects: Mesh, Meshtags and Functions.

NOTE: An idea for a future feature enhancement is that we could use data compression operators for arrays which store topology offsets and cell types which have a great potential for compression.

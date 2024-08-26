# Checkpointing module (part 1): Mesh

Mesh data consists of geometry and topology.
Geometry can be time dependent.
Topology is constant over time.

TODO:
 - [ ] description of node coordinates and coordinate element.
 - [ ] description of topology and mapping between geometry and topology entities

1. Attributes
 
 - `version` : version of DOLFINx
 - `git_hash` : GIT HASH of the DOLFINx used to generate the data
 - `name` : name of the mesh
 - `dim` : geometrical dimension of the mesh
 - `tdim` : topological dimension
 - `cell_type` : cell type of the coordinate element
 - `degree` : polynomial degree of the coordinate element used to define the triangulation
 - `lagrange_variant` : integration points

2. Variables
Note: The following scalar variables are used to define the size of the ADIOS2 global arrays when
writing and can be inferred from the dimensions of the saved ADIOS2 global arrays when reading.
Therefore, these scalar variables are not saved.

   - Scalars
        - `num_nodes` : number of vertices in the mesh
        - `num_cells` : number of cells

   - Arrays
        - `x` : coordinate array, size `(num_nodes, 3)`
        - `topology` : cell to vertex connectivity
            - `topology_array` : flattened array
            - `topolgy_offset` : offsets demarcating the cells

        The following are needed in optimized N-N checkpointing where the
        partition information is also saved.
        - `input_global_indices` : original input mesh's global indices
        - `orginal_cell_indices` : original input mesh's cell indices

## Typical write

A typical task in writing the data consists of determining (fetching/computing)
the global sizes of the arrays, finding the local section identified via offset
and count in the global arrays.
And preparation of the array and calling `engine.Put(...)` which will then either
immediately write, or put to ADIOS2 internal buffer or defer the write until the
EndStep collective.
This behaviour is either enforced (hardcoded) in the implementation based on a
necessity for a specific variable or controlled at runtime via config files.
The functionality of control via config files needs to be thoroughly tested yet.

Example:
```
   adios2::Variable<T> var_x = io.DefineVariable<T>("x",
                                                {num_dofs_global, 3},
                                                {offset, 0},
                                                {num_dofs_local, 3},
                                                adios2::ConstantDims);
 
   engine.Put(var_x, x.data());
```

## Typical read

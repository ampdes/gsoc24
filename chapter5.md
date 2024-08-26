# Checkpointing module (part 3): Functions

TODO: fill in details

Note:
1. Multiplicities of FunctionSpaces
2. Multiplicities of Functions from the same FunctionSpace

1. Attributes
    - `functionspace_names` : Array of strings of functionspace names
    - `function_names` : Array of strings of function names

2. Variables
    - Scalars
        - `num_cells_global`
        - `num_dofs_per_cell` : different than the one for mesh
        - `dofmap_bs` :
        - `num_dofs_global_dmap` :

    - Arrays
        - `cell_permutations` :
        - `topology` :
            - `topology_array` : dofmap of the function space
            - `topology_offsets` : xdofmap
        - `values` :

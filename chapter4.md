# Checkpointing module (part 2): Meshtags

Meshtags consists of entity topology and the values associated with entities.
Entity types could be: *points*, *edges*, *facets* and *cells*.
Moreover, for the same entity type, say *edges* there can be multiplicities of meshtags.

It is possible to save a collection of meshtags using a single IO and Engine to a ADIOS2 folder say `meshtags.bp`.
Each meshtags data is separated from another over step concept of ADIOS2.

The python API for reading the mesh can read all meshtags and return as a dictionary.

The metadata of meshtags is:

1. Attributes
   - `names` : array of name of meshtags
   - `dtypes` : array of data type of the meshtags, can be any of the integral and float type (NOTE: currently only int32 and double supported)
   - `dims` : array containing the dimension of the topological entity to which meshtags are associated with 

2. Variables

Note: The following scalar variables are used to define the size of the ADIOS2 global arrays when
writing and can be inferred from the dimensions of the saved ADIOS2 global arrays when reading.
Therefore, these scalar variables are not saved.

   - Scalars
        - `{name}_num_tag_entities_global`
        - `{name}_num_dofs_per_entity`
        - `{name}_num_saved_tag_entities`

   - Arrays
        - `{name}_topology` : This is a 2 dimensional array of size
            `({name}_num_saved_tag_entities, {name}_num_dofs_per_entity)`
        - `{name}_values` : This is an array of length `{name}_num_saved_tag_entities`

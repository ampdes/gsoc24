# Chapter 6: Future work

## 1. Variants of the checkpointing

 -  N-to-N : this would serve as an optimized version, where partitioning
    information is also saved to the file and not recomputed,
    rather the state is read back in as it was saved.
    An intended use-case is when the alloted compute time on a compute
    cluster is fixed but the simulation would require more.
 -  Snapshot: a lightweight checkpointing where only the relevant local
    information is saved with much of local-to-global information active
    on RAM. The intended use-case as outlined in ([Dokken,
    2024](https://github.com/openjournals/joss-papers/blob/joss.06451/joss.06451/10.21105.joss.06451.pdf))
    is for a fall-back mechanism in case of diverging iterative solver,
    or for an aggregated post postprocessing at the end of the
    simulation.

## 2. Adapdation of the checkpointing module to the mixed topology cases

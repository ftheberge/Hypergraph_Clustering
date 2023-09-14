# Hypergraph_Clustering
Modularity and clustering for hypergraphs using HyperNetX (HNX) representation

**This new version is a re-write as of the new version 2 of HNX, tested with version 2.0.3**

**Changes merged in this forked version of HyperNetX:** https://github.com/ftheberge/HyperNetX/tree/modularity

HNX details can be found at: https://github.com/pnnl/HyperNetX

# Required packages

* ```pip install igraph```
* ```pip install hypernetx```
  
or to install HyperNetX with the new modularity module:
* ```pip install git+https://github.com/ftheberge/HyperNetX.git@modularity#egg=hypernetx```

# Summary of new/old functions for modularity and clustering

With the new data structure in version 2 of HNX, we can achieve considerable speed-ups with functions in the **hypergraph_modularity** module. 
One of the main change is that we no longer need to precompute some attributes before calling the **modularity** function, which is now much faster. 
The same is true for the simple **last_step** heuristic algorithm.

As illustrated in this [notebook](https://github.com/ftheberge/Hypergraph_Clustering/blob/main/Notebooks/Hypergraph_Clustering_HNX2.ipynb), we can see a speedup of a few order of magnitude; 
for example with a 1000-node graph, pre-computation takes 19s and modularity evaluation 6s; this whole process is now down to 53ms!

## Unchanged functions (already in HNX hypergraph_modularity module):

- dict2part(D)
- part2dict(A)
- linear(d, c)
- majority(d, c)
- strict(d, c)
- two_section(HG)
- kumar(HG, delta=0.01)

## Functions no longer required (removed from HNX hypergraph_modularity module)

- precompute_attributes(H)
- _compute_partition_probas(HG, A)
- _degree_tax(HG, Pr, wdc)
- _edge_contribution(HG, A, wdc)
- _delta_ec(HG, P, v, a, b, wdc)
- _bin_ppmf(d, c, p)
- _delta_dt(HG, P, v, a, b, wdc)

## Functions with new version (updated in HNX hypergraph_modularity module)

- modularity(HG, A, wdc=linear)
- last_step(HG, L, wdc=linear, delta=0.01)

## New (hidden) functions (added in HNX hypergraph_modularity module)

- _last_step_unweighted
- _last_step_weighted

# References:

[1] Kumar T., Vaidyanathan S., Ananthapadmanabhan H., Parthasarathy S., Ravindran B. (2020) A New Measure of Modularity in Hypergraphs: Theoretical Insights and Implications for Effective Clustering. In: Cherifi H., Gaito S., Mendes J., Moro E., Rocha L. (eds) Complex Networks and Their Applications VIII. COMPLEX NETWORKS 2019. Studies in Computational Intelligence, vol 881. Springer, Cham. https://doi.org/10.1007/978-3-030-36687-2_24

[2] Kamiński B., Prałat P. and Théberge F. “Community Detection Algorithm Using Hypergraph Modularity”. In: Benito R.M., Cherifi C., Cherifi H., Moro E., Rocha L.M., Sales-Pardo M. (eds) Complex Networks & Their Applications IX. COMPLEX NETWORKS 2020. Studies in Computational Intelligence, vol 943. Springer, Cham. https://doi.org/10.1007/978-3-030-65347-7_13

[3] Kamiński B., Poulin V., Prałat P., Szufel P. and Théberge F. “Clustering via hypergraph modularity”, Plos ONE 2019, https://doi.org/10.1371/journal.pone.0224307


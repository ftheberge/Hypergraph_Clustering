# Hypergraph_Clustering
Modularity and clustering for hypergraphs using HyperNetX (HNX) representation

**This is work in progress**

HyperNetX details can be found at: https://github.com/pnnl/HyperNetX

See example code in the Notebook directory: https://github.com/ftheberge/Hypergraph_Clustering/blob/main/Notebooks/Hypergraph_Clustering.ipynb

Required packages:

* pip install python-igraph
* pip install partition-igraph
* pip install hypernetx

Game of thrones dataset built from: https://github.com/jeffreylancaster/game-of-thrones

## Summary of functions for HNX hypergraphs

We build the hypergraph HG using:
```python
HG = hnx.Hypergraph(dict(enumerate(Edges)))
```
where 'Edges' is a list of sets; edges are then indexed as 0-based integers, so to preserve unique ids, we represent nodes as strings. 
For example Edges[0] = {'A', 'B', 'C'}

### Modularity

The following function is called to compute required quantities for modularity and clustering:

```python
HNX_precompute(HG)
```

To compute H-modularity for HG w.r.t. partition A (list of sets covering the vertices):
```python
HNX_modularity(HG, A, wcd=linear)
```
where 'wcd' is the weight function (default = 'linear'). Other choices are 'strict' and 'majority', or any user-supplied function with the following format:
```python
def linear(d,c):
    return c/d if c>d/2 else 0
```

where d is the edge size, and d>=c>d/2 the number of nodes in the majority class.

### Two-section graph

To build the random-walk based 2-section graph given hypergraph HG:
```python
G = HNX_2section(HG)
```
where G is an igraph Graph.

### Kumar clustering algorithm

Given hypergraph HG, compute a partition of the vertices as per Kumar's algorithm described in [1]:

```python
K = HNX_Kumar(HG, delta=.01)
```

where delta is the convergence stopping criterion. Partition is returned as a dictionary.

### Hypergraph-based clustering

Given hypergraph HG and initial partition L, compute a partition of the vertices as per Last-Step algorithm described in [2]:

```python
A = HNX_LastStep(HG, L, wdc=linear, delta = .01)
```

where 'wcd' is the the weight function (default = 'linear') and delta is the convergence stopping criterion. Returned partition is a list of sets.

### Papers:

[1] Kumar T., Vaidyanathan S., Ananthapadmanabhan H., Parthasarathy S., Ravindran B. (2020) A New Measure of Modularity in Hypergraphs: Theoretical Insights and Implications for Effective Clustering. In: Cherifi H., Gaito S., Mendes J., Moro E., Rocha L. (eds) Complex Networks and Their Applications VIII. COMPLEX NETWORKS 2019. Studies in Computational Intelligence, vol 881. Springer, Cham. https://doi.org/10.1007/978-3-030-36687-2_24

[2] B. Kaminski, P. Pralat and F. Théberge, Community Detection Algorithm Using Hypergraph Modularity, to appear in the proceedings of Complex Networks 2020, Springer.

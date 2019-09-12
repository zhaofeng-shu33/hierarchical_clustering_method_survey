## Modularity based method

Let $m$ be the number of edges, $A_{ij}$ be the adjacency matrix and $C_i$ be a cluster of the graph. The modularity is written as
$$
Q = \frac{1}{2m} \sum_{ij} (A_{ij} - P_{ij}) \delta(C_i, C_j)
$$
$P_{ij}$ represents the expected number of edges between vertices $i$ and $j$ in a random graph which has the same node degree distribution as the original graph. Suppose vertices $i$ and $j$ have degree $k_i$ and $k_j$ respectively, then $P_{ij} = \frac{k_i k_j}{2m}$.

Maximizing modularity gives a cluster of the graph.

Basic idea is to merge two clusters at each step. For sparse graph, Clauset et. al. [2004] proposes an efficient algorithm to accomplish this merge, which achieves $O(md\log n)$ where $d$ is the depth of the dendrogram. To achieve this time bound, $\Delta Q_{ij}$ is maintained rather than the adjacency matrix. See [fastmodularity](https://www.cs.unm.edu/~aaron/research/fastmodularity.htm) for detail.



## Divisive approach

The first algorithm in community detection is proposed by Newman and Girvan using a divisive approach. It removes one edge with the largest "betweenness" measure in each step until the graph is split into singletons. The betweenness measure is not unique. For example, we can use the shortest-path betweenness. That is, "the number of shortest paths between all vertex pairs that run along that edge". The time complexity to calculate this measure for all edges is $O(mn)$ using breadth first search for each node.
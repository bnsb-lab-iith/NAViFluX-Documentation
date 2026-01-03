### Centrality Analysis

The **Centrality Analysis** feature allows you to calculate **network-based** metrics on your model. This helps you find the most important reactions or metabolites by quantifying their connectivity and influence in the network.

All **Centrality metrics** are calculated using the Python [NetworkX package](https://networkx.org/).

---

![Centrality Analysis Workflow](./../images/pathway-visualizer/centrality-analysis.png)

### Steps
1. Click the **Centrality Analysis** button.
2. Select the desired metrics to be calculated and click **"Calculate and download results"**.
3. A zip file will be downloaded containing the selected metrics in `.csv` format.


### Degree Centrality

Degree centrality is defined as the number of direct edges a node has in a given network. For directed metabolic pathways, degree centrality is split into **in-degree** (number of incoming edges) and **out-degree** (number of outgoing edges).

**Mathematical Formulae:**  

For a directed graph \(G = (V,E)\) and node \(v\):

- **In-degree centrality:**  

$$
C_{D}^{in}(v) = \frac{\deg^{in}(v)}{|V|-1}
$$

- **Out-degree centrality:**  

$$
C_{D}^{out}(v) = \frac{\deg^{out}(v)}{|V|-1}
$$

where:

- \(\deg^{in}(v)\) = number of incoming edges to \(v\)  
- \(\deg^{out}(v)\) = number of outgoing edges from \(v\)  

Both values are normalized by \(|V|-1\), so that:

$$
0 \leq C_D(v) \leq 1
$$

---

### Betweenness Centrality

Betweenness centrality measures how frequently a node lies on shortest paths between other nodes in the network. This helps identify **bottleneck reactions** that control the flow of metabolites.

**Mathematical Formula:**

For a graph \(G = (V,E)\) and node \(v\):

$$
C_B(v) = \sum_{s \neq v \neq t \in V} \frac{\sigma_{st}(v)}{\sigma_{st}}
$$

where:

- \(\sigma_{st}\) = number of shortest paths between nodes \(s\) and \(t\)  
- \(\sigma_{st}(v)\) = number of those paths that pass through node \(v\)

**Normalization:**

To scale values between 0 and 1:

- **Undirected graphs:**

$$
C_B^{norm}(v) = \frac{C_B(v)}{(n-1)(n-2)/2}
$$

- **Directed graphs:**

$$
C_B^{norm}(v) = \frac{C_B(v)}{(n-1)(n-2)}
$$

where \(n = |V|\) is the total number of nodes.

---

### Closeness Centrality

Closeness centrality explains how close a node is to all other nodes in the network based on the average length of shortest paths.

**Mathematical Formula:**

For a connected graph \(G = (V,E)\) and node \(v\):

$$
C_C(v) = \frac{n-1}{\sum_{t \in V \setminus \{v\}} d(v,t)}
$$

where:

- \(n = |V|\) is the total number of nodes  
- \(d(v,t)\) is the shortest path distance between \(v\) and \(t\)

The denominator is the **farness** (total distance from \(v\) to all other nodes), and closeness is its reciprocal.

---

### Eigenvector Centrality

Eigenvector centrality measures a node's importance based on its connections **and the importance of the nodes it connects to**.

**Mathematical Formula:**

For a node \(v\):

$$
x_v = \frac{1}{\lambda} \sum_{t \in V} A_{vt} \, x_t
$$

where:

- \(A\) is the adjacency matrix of the graph  
- \(x_v\) is the centrality score of node \(v\)  
- \(\lambda\) is the largest eigenvalue of \(A\)

In vector form:

$$
Ax = \lambda x
$$

The components of \(x\) give the **eigenvector centrality scores** of the nodes.

---

### PageRank Centrality

PageRank is a variant of eigenvector centrality that measures a node's importance based on both the **number of incoming links** and the **importance of the linking nodes**, while also incorporating a probability of randomly jumping to another node.

**Mathematical Formula:**

For a directed graph \(G = (V,E)\) and node \(v\):

$$
PR(v) = \frac{1-d}{N} + d \sum_{u \in M(v)} \frac{PR(u)}{\deg^{out}(u)}
$$

where:

- \(N = |V|\) is the total number of nodes  
- \(d\) is the damping factor (usually 0.85)  
- \(M(v)\) is the set of nodes linking to \(v\)  
- \(\deg^{out}(u)\) is the out-degree of node \(u\)

The algorithm is solved iteratively until values converge, giving a normalized importance score for each node.

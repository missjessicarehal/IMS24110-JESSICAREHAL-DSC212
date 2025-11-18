# IMS24110-JESSICAREHAL-DSC212
This project uses recursive spectral modularity to split the Karate Club graph into meaningful communities. By analyzing eigenvectors, modularity gains, and centrality metrics, it reveals how tightly connected groups form and highlights influential nodes in the network.”
### Overview  

This project explores **community detection** in social networks through the concept of **modularity**.  
Using the **recursive spectral modularity partitioning** method proposed by Newman (2006), the analysis is performed on **Zachary’s Karate Club graph** — a classic real-world dataset representing friendships among members of a university karate club.  

The main objective is to understand how mathematical principles from graph theory and linear algebra can uncover underlying community structures within networks.  

---

### Background  

Zachary’s Karate Club network consists of 34 members connected by 78 edges representing social interactions.  
During Zachary’s fieldwork, a disagreement between the club instructor (“Mr. Hi”) and the administrator caused the club to split into two factions.  
This dataset is a benchmark in network science because it allows us to test whether community detection algorithms can recover this real-world division using only structural information.  

---

### Mathematical Foundation  

The **modularity matrix** is defined as:

$$
B = A - \frac{kk^{T}}{2m}
$$

where  

- \( A \) is the adjacency matrix,  
- \( k \) is the degree vector,  
- \( m \) is the total number of edges in the network.  

The **modularity score** for a partition represented by vector \( s \in \{-1, +1\}^n \) is given by:

$$
Q = \frac{1}{4m} s^{T} B s
$$

Maximizing \( Q \) corresponds to finding the community structure that deviates most from randomness.  

The **leading eigenvector** of \( B \) provides the relaxed solution to this optimization problem.  
Nodes are assigned to communities based on the sign of their corresponding entries in this eigenvector.  
To detect multiple communities, this bipartitioning process is applied recursively to each subgraph until no further split improves modularity (i.e., the largest eigenvalue ≤ 0).  

---

### Methodology  

1. Load the **Karate Club graph** using NetworkX.  
2. Construct the **modularity matrix** for the current subgraph.  
3. Compute its leading eigenpair $(\lambda_1, u_1)$.  
4. If $\lambda_1 > 0$:  
   - Split nodes into two groups based on the sign of entries in $u_1$.  
   - Recurse on each group.  
   - Visualize the graph after each split using distinct colors.  
5. After each iteration, compute the following metrics for all nodes:  
   - Degree centrality  
   - Betweenness centrality  
   - Closeness centrality  
   - Clustering coefficient  
6. Plot how these metrics evolve across iterations.  
7. Discuss which nodes remain central and how the community structure influences network metrics.  

All code and visualizations were implemented in **Python** using NetworkX, NumPy, and Matplotlib.  

---

### Key Findings  

- The recursive spectral method successfully reproduced the **two major communities** observed in the real split between the instructor’s and the administrator’s groups.  
- **Nodes 1 and 34** exhibited the highest betweenness centrality, consistently serving as **bridge nodes** between communities.  
- **Degree** and **closeness centralities** were higher within dense subgroups, while **clustering coefficients** decreased for nodes near community boundaries.  
- The overall modularity value increased during early iterations and plateaued once meaningful partitions stabilized, confirming convergence.  

---

### Insights  

- Modularity effectively distinguishes statistically significant communities by comparing observed edge densities with those expected under a random null model.  
- The spectral approach provides an interpretable, eigenvector-based method that links algebraic properties to social structure.  
- Tracking the evolution of centrality metrics revealed how influence and connectivity redistribute as communities form.  

---

### Limitations  

- Recursive bisection enforces binary splits, which may not capture overlapping or nested community structures.  
- Modularity suffers from the **resolution limit problem**, potentially merging smaller communities into larger ones.  
- Eigenvalue computations can become unstable for graphs with nearly equal leading eigenvalues.  

---

### Conclusion  

This study demonstrates how theoretical constructs such as **modularity** and **spectral decomposition** translate into practical algorithms for community detection.  
Through the recursive modularity framework, the project highlights the interplay between **network structure**, **eigenvalue analysis**, and **social dynamics**.  

The Karate Club network serves as a clear example of how mathematical models can successfully uncover hidden divisions in real-world social systems.  

---

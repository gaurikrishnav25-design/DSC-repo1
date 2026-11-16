# Modularity on the Karate Club Graph
### Introduction
In the 1970s, anthropologist Wayne Zachary mapped the social ties among 34 members of a university karate club, creating a famous network graph. When a dispute later split the club into two rival factions led by the instructor and the president, members largely sided with their existing friend groups. Because we know both the pre-split friendships and the final outcome, this small network serves as the classic benchmark for testing whether mathematical community-detection algorithms can predict real-world social divisions.


# Goal

The goal of this assignment is to build a Python algorithm (using basic scientific Python libraries and NetworkX) to uncover hidden social communities within the classic Karate Club network.


• Implement Recursive Spectral Modularity: Write an algorithm that repeatedly splits the network into smaller communities using the leading eigenvector of the modularity matrix B, stopping when the largest eigenvalue λ₁ ≤ 0.


• Visualize Community Splits


• Calculate four metrics for every node after each split—degree centrality, betweenness centrality, closeness centrality, and clustering coefficient—and plot how these values change across iterations.

### Main steps
1) #### Building Modularity matrix
   #### Why modularity?
   While splitting,
   simply minimizing cut edges often isolates a single node instead of finding true, meaningful communities. Modularity checks whether a network division is statistically surprising compared to random chance.It compares actual within-group edges to a random baseline where nodes keep their original number of connections.Maximize the gap between observed internal edges and random expectations to uncover real community structure.


2) #### Repeat the split recursively on each community until no split improves modularity.


3) #### Draw the graph after every split with a fixed layout and one colour per community.


4) #### Compute degree, betweenness, closeness and clustering for every node after each split and plot how they evolve.


5) #### Discuss which nodes stay central and how community structure shapes these metrics.


## Conclusion

Using Newman’s spectral modularity maximization algorithm on Zachary's Karate Club network ($n = 34$, $m = 78$), the network naturally partitions into **4 distinct communities** with a maximum global modularity score of **$Q = 0.3934$**:

* **Optimal Community Structure:** The first bisection divides the club into two primary factions ($16$ and $18$ nodes, $Q = 0.3715$), capturing the historical split around the instructor (Node 0) and the administrator (Node 33). A second recursive split refines these into four tighter subgroups ($7, 9, 12,$ and $6$ nodes), increasing modularity to $Q = 0.3934$, after which no further split yields a positive modularity gain ($\Delta Q \le 0$).
* **Decline in Global Centrality:** As inter-community edges are removed across iterations, **degree, betweenness, and closeness centralities drop sharply** for nearly all nodes. Hub nodes such as **Node 0** (degree centrality $0.4848 \rightarrow 0.1515$; betweenness $0.4376 \rightarrow 0.0107$) and **Node 33** (degree centrality $0.5152 \rightarrow 0.3333$; betweenness $0.3041 \rightarrow 0.0587$) lose their global bridging roles once cross-group links are severed.
* **Preservation of Local Cohesion:** Unlike global centrality measures, the **local clustering coefficient remains high or increases** for most nodes across splits (e.g., Node 0 rises from $0.1500$ to $0.4000$, and Node 33 rises from $0.1103$ to $0.1818$). This confirms that spectral bisection effectively isolates densely connected local triangles while cutting sparse bridges between communities.




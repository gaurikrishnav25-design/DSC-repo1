###Modularity on the Karate Club Graph
#Introduction
In the 1970s, anthropologist Wayne Zachary mapped the social ties among 34 members of a university karate club, creating a famous network graph. When a dispute later split the club into two rival factions led by the instructor and the president, members largely sided with their existing friend groups. Because we know both the pre-split friendships and the final outcome, this small network serves as the classic benchmark for testing whether mathematical community-detection algorithms can predict real-world social divisions.

#Main steps
1) Building Modularity matrix
   Why modularity?
   While splitting,
   simply minimizing cut edges often isolates a single node instead of finding true, meaningful communities. Modularity checks whether a network division is statistically surprising compared to random chance.It compares actual within-group edges to a random baseline where nodes keep their original number of connections.Maximize the gap between observed internal edges and random expectations to uncover real community structure.
   • Graph Setup: A graph with \(n\) nodes and \(m\) edges is represented by an adjacency matrix \(A\) (\(1\) if connected, \(0\) otherwise), where each node \(i\) has degree \(k_{i}\).
• Group Labels: A split into two communities is encoded by a vector \(s \in \{-1, +1\}^n\), assigning \(+1\) to group 1 and \(-1\) to group 2.
• Expected Random Edges: Under a random null model that preserves node degrees, the expected number of edges between nodes \(i\) and \(j\) is \(\frac{k_{i}k_{j}}{2m}\).
• The Modularity Matrix (\(B\)): Defined as \(B = A - \frac{k k^\top}{2m}\), its entries \(B_{ij} = A_{ij} - \frac{k_i k_j}{2m}\) measure the difference between actual and expected edges. Because \(B\) is real and symmetric, it has real eigenvalues and orthonormal eigenvectors.
• The Modularity Score (\(Q\)): Calculated as \(Q = \frac{1}{4m} s^\top B s\), where a large positive score means the split has significantly more internal edges than random chance.
• The Optimization Goal: Find the vector \(s \in \{-1, +1\}^n\) that maximizes \(Q\).

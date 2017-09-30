# Prim-s-Algorithm-Visualization---Java-
In computer science, Prim's algorithm is a greedy algorithm that finds a minimum spanning tree for a weighted undirected graph. This means it finds a subset of the edges that forms a tree that includes every vertex, where the total weight of all the edges in the tree is minimized. The algorithm operates by building this tree one vertex at a time, from an arbitrary starting vertex, at each step adding the cheapest possible connection from the tree to another vertex.

Description

The algorithm may informally be described as performing the following steps:

Initialize a tree with a single vertex, chosen arbitrarily from the graph.
Grow the tree by one edge: of the edges that connect the tree to vertices not yet in the tree, find the minimum-weight edge, and transfer it to the tree.
Repeat step 2 (until all vertices are in the tree).
In more detail, it may be implemented following the pseudocode below.

Associate with each vertex v of the graph a number C[v] (the cheapest cost of a connection to v) and an edge E[v] (the edge providing that cheapest connection). To initialize these values, set all values of C[v] to +∞ (or to any number larger than the maximum edge weight) and set each E[v] to a special flag value indicating that there is no edge connecting v to earlier vertices.
Initialize an empty forest F and a set Q of vertices that have not yet been included in F (initially, all vertices).
Repeat the following steps until Q is empty:
Find and remove a vertex v from Q having the minimum possible value of C[v]
Add v to F and, if E[v] is not the special flag value, also add E[v] to F
Loop over the edges vw connecting v to other vertices w. For each such edge, if w still belongs to Q and vw has smaller weight than C[w], perform the following steps:
Set C[w] to the cost of edge vw
Set E[w] to point to edge vw.
Return F
As described above, the starting vertex for the algorithm will be chosen arbitrarily, because the first iteration of the main loop of the algorithm will have a set of vertices in Q that all have equal weights, and the algorithm will automatically start a new tree in F when it completes a spanning tree of each connected component of the input graph. The algorithm may be modified to start with any particular vertex s by setting C[s] to be a number smaller than the other values of C (for instance, zero), and it may be modified to only find a single spanning tree rather than an entire spanning forest (matching more closely the informal description) by stopping whenever it encounters another vertex flagged as having no associated edge.

Different variations of the algorithm differ from each other in how the set Q is implemented: as a simple linked list or array of vertices, or as a more complicated priority queue data structure. This choice leads to differences in the time complexity of the algorithm. In general, a priority queue will be quicker at finding the vertex v with minimum cost, but will entail more expensive updates when the value of C[w] changes.

Time complexity

A simple implementation of Prim's, using an adjacency matrix or an adjacency list graph representation and linearly searching an array of weights to find the minimum weight edge to add, requires O(|V|2) running time. However, this running time can be greatly improved further by using heaps to implement finding minimum weight edges in the algorithm's inner loop.

A first improved version uses a heap to store all edges of the input graph, ordered by their weight. This leads to an O(|E| log |E|) worst-case running time. But storing vertices instead of edges can improve it still further. The heap should order the vertices by the smallest edge-weight that connects them to any vertex in the partially constructed minimum spanning tree (MST) (or infinity if no such edge exists). Every time a vertex v is chosen and added to the MST, a decrease-key operation is performed on all vertices w outside the partial MST such that v is connected to w, setting the key to the minimum of its previous value and the edge cost of (v,w).

Using a simple binary heap data structure, Prim's algorithm can now be shown to run in time O(|E| log |V|) where |E| is the number of edges and |V| is the number of vertices. Using a more sophisticated Fibonacci heap, this can be brought down to O(|E| + |V| log |V|), which is asymptotically faster when the graph is dense enough that |E| is ω(|V|), and linear time when |E| is at least |V| log |V|. For graphs of even greater density (having at least |V|c edges for some c > 1), Prim's algorithm can be made to run in linear time even more simply, by using a d-ary heap in place of a Fibonacci heap.

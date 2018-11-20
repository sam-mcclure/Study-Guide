# Graphs

* Graphs are like trees, but they don't have a root node, can have directions or not, and don't have restraints on which nodes can be connected

* Every graph must have at least a single node

* **Singleton Graph** - A graph with just one node

* Edges/links can connect nodes in any way possible. Can either have a direction or no direction

* **Directed Edge** - Two nodes are connected in a very specific way, i.e. have direction/one way travel. Can only travel from the origin to the destination ( A connects to B = A -> B NOT A <- B)

* **Undirected Edge** - The path between two nodes goes both ways. Origin and destination are not fixed

* **Directed Graph/Digraph** - All the edges in a graph are directed

* **Undirected Graph** - All the edges in a graph are undirected


* Graphs are a way to formally represent a network, or a collection of interconnected objects

* In mathematics, graphs are defined as ordered pairs with two parts: vertices and edges

* Mathematically definition for a graph is G = (V, E), where v is a set of nodes, also called vertices, and e is a set of edges, also called links ( V and E are objects)

* The web is a massive graph structure

* **Graph** - A graph G is an ordered pair of a set V of vertices and a set E of edges. G = (V, E)

* Facebook is an undirected graph (both must be friends in order to have a connects) and the edges can be considered the same

* Twitter is an unweights directional graph because users don't have to follow each other, can be one sided, and the edges can be considered the same

* Web-Crawling is Graph Traversal

* Weighted graphs add some kind of value to the edges, such as the length.

* A highway system is an weighted undirected graph. Roads go both ways, but some roads are preferable based on road length

* An intercity road system is a weighted directed graph. Can possibly have one way roads an some roads are preferable based on road length

* |V| -> Number of vertices, |E| -> Number of edges

* **Self-Loop** - Both end points of an edge are the same. Node points back to itself. Interlinked webpages can have a link to itself, this would be a self-loop, just refreshes the page. Can be directed or undirected

* **Multi-Edge** - An edge that occurs more than once in a graph. A graph of a flight system may have multiple edges to the same place, but with different costs

* **Simple Graph** - A graph with no self-loop or multi-edges

* Minimum possible edges in a graph is 0

* Maximum possible edges in directed graph if |v| = n, then 0 <= |E| <= n(n - 1) ( no self loop or multiedges)

* Max edges in undirected graph is half of those for directed: 0 <= |E| <= (n (n - 1))/ 2

* A graph is dense (too many edges) if |E| is close to maximum. Typically stored in the computer in an adjacency matrix

* A graph is sparse (too few edges) if |E| is close to number of vertices. Typically stored in the computer in adjacency list

* **Walk** - A sequence of vertices where each adjacent pair is connected by an edge

* **Simple Path** - A walk in which no vertices (and thus no edges) are repeated

* **Trail** - A walk in which no edges are repeated

* If you have a repeating path, there is also a way to make a simple path out of it

* **Strongly Connected Graph** - If there is a path from any vertex to any other vertex (any possible path between all vertices) in a directed graph.

* **Connected** - If there is a path from any vertex to any other vertex in undirected path

* **Weakly Connected** - If a directed graph is not strongly connected but can be turned into a connected graph by treating all edges as undirected

* **Closed Walk** - Starts and ends at same vertex and length (|E|) is greater than 0

* **Simple Cycle** - A closed walk with no repeated edges besides start/end

* **Acyclic Graph** - A graph with no cycle (ie a tree with undirected edges)

* **Directed Acyclic Graph (DAG)** 

* To create and store graph in computer, you can create two lists: one for vertices and one for edges. Can use array or dynamic list

* Vertices list will be a list of names/strings

* Edge list will be an object with two fields (start and end vertices). Can make a class and store start and end idx. If graph is weighted, add a third value to store the weight 

* For vertex list, least number of rows needed is |v|. Length of each row could be different (ie city names). All rows don't cost the same. However, average space will still be O(n)

* For edge list, we can store pointers to vertex list or index of vertices, which would make it O(n) to number of edges

* Overall space is O(|V| + |E|)

* Most frequently used operation is finding all nodes adjacent (direcly connected) to given node. Perform linear node search of edges to check for given node, would be O(n) or O (|E|)

* To find if two given nodes are conencted, at worst case, you'd have to go through all nodes, which is O(n) again

* Number of edges can go up to O(n^2) so operations of O(|E|) can be costly. Want to keep things to O(|V|). Overall not efficient

11/20/18

## Adjacency Matrix

* In order to keep the cost of lookups in a graph, you can store edges in a 2D matrix/array of size v*V

* Use indices from the vertex list. A at [i][j] can be set to 1 if there is an edge from i to j, otherwise set to 0. For undirected graph, you'd need to set [i][j] and [j][i] to 1.

* For undirected graph, you only have to go through half of the graph, since it's symmetrical

* The time cost of finding all nodes adjacent to a specific node, you have to find the index from the vertex list, then go to that index in the adjacency matrix and scan that row. This will be O(|V|) operation

* If we know the index, we can access an edge in constant time

* If names are given, complexity for finding if two nodes are connected are O(|V|) from vertex list

* We can store the vertices in a hash table to make lookup time constant

* For a weighted graph, the value at [i][j] can be the weight of the edge, the other values can be set to infinity (a value that wouldn't be valid)

* The adjacency matrix saves on time, but takes up more space. We're using v^2 space instead of E space. This is good for dense graphs (close to V^2 edges), but for sparse graphs, we're wasting a lot of memory

* Most real world graphs will be sparse

## Adjacency List

* Adjacency matrixes are efficient for time, but not space. Don't need to keep track of edges that don't exist, this takes up to much space. Should be able to infer nodes are not connected by seeing which nodes are connected

* Instead of storing edges as an array, you can keep a list of all nodes to which a node is connected

* Can use a linked list or a binary search tree or an array to store values

* Each row can be a one-dimensional array of the connected nodes to the node at that index. Will be space of O(|E|). Worst case lookup is linear O(|V|). If the rows are sorted, can use a binary search. Keeping the arrays sorted is costly in other ways

* In order to add or delete nodes, in an adjacency matrix it's easy, but for adjacency list, you have to dynamically change the array.

* If each row was a linked list, insertion and deletion gets easier. Would need a linked list for each node. Create array of pointers that point to head of linked list

* Adjacency list is a linked list. For weighted graph, store an extra field in each node. Otherwise, each node has a value and a pointer to next node

* Space complexity is O(|E| + |V|). Most graphs are sparse, so this is okay. 

# Week 1
## Graphs

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

11/21/18

## BFS/DFS for Graphs

* Trees are a type of graph, but graphs are not a type of tree

* Depth-First (goes from top to bottom and back up) traversal requires a stack

* DFS - Take first node, node A, and push it into the stack and visit it. Take all vertices connected to A and pick the 'least' (B), push it onto the stack and visit it. Then check adjacent unvisited vertices of B and take the least. Keep going until you've visited all vertices. When there are no nodes left, you pop off the top of the stack until you get to a node that has new nodes to visit

* Breadth First traversal uses queues. 

* Main differece of Depth-First Traversal and Breadth-First traversal for grpahs is that DFS uses a stack (LIFO) and BFS uses a Queue (FIFO)

* For BFS, we're going to start at vertex A and visit it, then visit least near node (B) and add it to the queue. We don't visit it yet. Instead, we add all nodes adjacent to A and add those vertices to the queue in asceding order (B - D - G). When there are no connected vertices left, you shift off the first (A) and move to the next node (B). You visit that node, shift it off, and add all of its adjacent vertices to the queue.

* Unlike trees, graphs may contain cycles, so we may come to the same node again. To avoid processing a node more than once, we use a boolean visited array.

* Time complexity of DFS is O(|V| + |E|)

* Travel the graph in layers

* You take starting vertex, then add all vertices that are connected to the first vertex. Traverse nodes in layers. Since we have cycles, each node cound be visisted inifinite times, so use a boolean visited array (1 if visited, else 0)

* The key data structure will be a queue (FIFO). Visted array starts will 0 for every node and the queue starts as empty

W1D4

## BFS 

* Breadth First Traversal (or Search) for a graph is very similar to BFS for a tree. the only catch is, unlike trees, graphs may contain cycles, so we may come to the same node again. To avoid processing a node more than once, we use a boolean visited array. For simplicity, it is assumd that all vertices are reachable from the starting vertex

* Time complexity O(V + E) where V is the number of vertices in the graph and E is the number of edges in the graph

W1D5

## Topological Sort

* Given a directed acyclic graph, topological sort is the ordering of vertices of this graph such that for every edge u,v going from u to v, u should always appear before v in the ordering

* One application of topological sort is in the build system. The computer knows what order to download the packages based on dependencies using a topological sort

* Use a set and a stack. The set has all the visited vertices while the stack has all the vertices in topological order

* You start at a vertex and add it to the set. You then find it's children and add them to the set. If a node has no children, it is added to the stack. We keep visiting a node's children in the set and them putting them in the stack. If there are no children let for the nodes in the set, we pick any other unexplored node and repeat the process. Don't do anything if child is already in the visited set. When there are no unvisited nodes, you pop items from the stack and that is the topological order

* Topological sorting for a Directed Acyclic Graph (DAG) is a linear ordering of vertices such that for every directed edge u,v vertex u comes before v in the ordering. Topological Sorting for a graph is not possible if the graph is not a DAG

* There can be more the one topological sorting for a graph. The first vertex in topological sorting is always a vertex with in-degree as 0 (a vertex with no incoming edges)

* In DFS, we print a vertex and then recursively call DFS for its adjacent vertices. In topological sorting, we need to print a vertex before its adjacent vertices.

* We can modify DFS to find Topological sorting of a graph. In DFS, we start from a vertex, we first print it and then recursively call DFS for its adjacent vertices. In topological sorting, we use a temporary stack. We don't print the vertex immeadiately, we first recursively call topological sorting for all its adjacent vertices, then push it to a stack. Finally, print contents of the stack. Note that a vertex is pushed to the stack only when all of its adjacent vertices (and their adjacent vertices and so on) are already in the stack.

* This is simply DFS with an extra stack, so time complexity is the same O(V+E)

* Topological sorting is mainly used for scheduling jobs from the given dependencies among jobs. In compsci, applications of this type arise in instruction scheduling, ordering of formula cell evaluation when recomputing formula values in spreadsheets, logic synthesis, determining the order of compilation tasks to perform in makefiles, data serializatio, and resolving symbol dependencies in linkers

W1D6

## Djikstra

* Used to find single-source shortest path. Given a graph and a source vertex, you have to find the shortest path of every other vertex from this source vertex

* Works on both directed and undirected graph as long as the weight on the edge is not negative

* It is a greedy algorithm. We need to use a heap Map that has methods for add, extractMin, contains, and decrease (combination of binary heap and hash map)

* To start, you pick the vertice that you want to travel from and inside the map, set the distance from each vertex to A to be infinity. Then, set the distance from the starting node to itself to 0, then use extractMin to get A out, then explore all its neighbors and update their distance from A. Do another extractMin and explore neighbors. Keep doing extractMin until all of the elements are in the heap.. You will have a map for V parent and one for V dist. 

* When you use extractMin on A, A's parent will be null and A's distance will be 0. If you find a path that is shorter than current known distance, update distance. Extractmin again and for the new vertex, we will examine the connected nodes. If the node is not in the heap anymore, nothing happens. If it is, we update with the minimum distance from A(if A to E is 2 and E to F is 3, min is 5). Keep going until map heap is empty.

* To find the path, you check the parent map and follow the parents from a point until you reach destination node.

* Time complexity is O(Elog(V)) and space is O(V + E)

* Given a graph and a source vertex in the graph, find the shortest path from source to all vertices in the given graph

* We generate a shortest path tree with given source as the root. We maintain two sets, one set contains vertices included in the shortest path tree, the other set includes vertices not yet in the shortest path tree. At every step of the algorithm, we find a vertex which is in the other set (not included yet set) and has a minimum distance from the source.

* Steps:
1. Create a set sptSet(shortest path tree set) that keeps track of vertices included in shortest path tree, ie whose minimum distance from a source is calculated and finalized. Initially this set it empty.
2. Assign a distance value to all vertices in the input graph. Initialize all distance values as infinite. Assign distance value 0 for the source vertex so that it's picked first.
3. While sptSet doesn't include all vertices:
    a. Pick a vertex u which is not yet in sptSet and has a minimum distance value
    b. Include u in sptSet
    c. Update distance value of all adjacent vertices of u. To update the distance values, iterate through all adjacent vertices. For every adjacent vertex v, if sum of distance value of u (from source) and weight of edge u-v, is less than the distance value of v, then update the distance value of v.
# Graphs

1.  How do we define a graph mathematically?
- G = (V, E) A graph G is an ordered pair of a set V of vertices and a set E of edges

2. What is the difference between directed, undirected, weighted, and unweighted?
- A directed graph has specific direction for edges and that can only be traverse in one-direction (ie from A to B). 
- An undirected graph has no directional edges, so the edges are bidirectional (can go from A to B or B to A). 
- A weighted graph has some kind of value weight for edges, such as length. 
- In an unweighted graph, all edges can be considered to have no weight/the same weight.

3. Give an example of various types of graphs (Weighted Undirected, Unweighted Directed, Unweighted Undirected, etc.)
- Facebook is an unweighted undirected graph because connections can only exist bidirectionally (have to both be friends to have a connection) and connections can be considered to have the same weight.
- Twitter is an unweighted directed graph because users can optionally both be following each other (ie you can follow a user and they might not follow you back) and the connections have the same weight
- A highway system is a wieghted undirected graph because the roads go in both directions, but they all have different lengths 
- An intercity road system is a weighted directional graph because roads can be one way and they have different lenghts

4. What makes a graph a simple graph? What attributes would make it not simple?
- A simple graph is a graph that has no self-loops or multi-edges, meaning no nodes point to themselves and there is only one connection from one node to another (all edges occur once)

5. What is the maximum number of edges in a directed simple graph? Undirected simple graph? Answer should be in terms of N
- Max edges in a directed simple graph are n(n - 1)
- Max edges in an undirected simple graph are (n(n-1))/2

6. Describe the levels of connectivity a graph can have (strongly connected, weakly connected).
- A directed graph is strongly connected if there is a path from any vertex to any other vertex (any possible path between all vertices). An undirected path with the same criteria is called connected
- A weakly connected directed graph is one that is only considered connected if it were treated as an undirected graph

7. What are cycles?
- A closed walk is a path that start and ends at the same vertex and has a length greater than 1. A simple cycle is a closed walk with no repeated edges

8. What are some naive ways we can store and traverse graphs? Be able to discuss time/space complexity of these approaches, and what issues we may face.
- You can store a graph as two lists: a vertex list and an edge list. The vertex list can be an array of a strings, denoting the vertex's name. These strings could be of varrying length (ie, San Francisco is bigger than A), but this should be negligable and take up O(|V|) space, relative to number of vertices.
The edges list will be an array of objects that have start and end vertices and optionally a weight. We should either store pointers to the vertices or use the indexes of the vertices from the vetices list. This will save space and we would have O(|E|) space, relative to number of edges.
The most frequently used operations would be finding all nodes connected to a node or checking to see if two nodes are connected. Both operations have a worse case of O(n) because you have to check the whole list find related nodes or see if there's a connection. There may be O(|V|^2) number of edges which would make this inefficient. We would rather have O(|V|)

9. Give a high level overview of an Adjacency Matrix
- When storing the edges of a graph, instead of having a list, you can make a 2D matrix of all of the verticies in the graph and fill in the edges at [i][j] with a truthy value or a weight if there is a connection or a falsey value if there is no connection. This makes lookup time for a graph's edges O(|V|), which is much faster than the previous O(|E|)

10. If we were only concerned about time complexity, is an Adjacency Matrix efficient? Why/why not?
-Adjacency Matrix is more efficient for time complexity because if you want to find all the connected vertices for a specific vertex, you can just go to the row of the index of the vertex and check that. If you want to see if two vertices are connected, you can go to the corresponding row and column in the matrix. Both of these are O(|V|), assuming you are given a vertex and have to look up its index from the list. If given the index, this operation is constant time. This is faster than the edges list because that had lookup times of O(|E|)

11. If we were only concerned about space complexity, is an Adjacency Matrix efficient? Why/why not?
-Adjacency matrix is not efficient for space complexity because instead of taking up O(|E|) space, they take up O(|V|^2) space. If the graph was densely populated and had close to V^2 edges, this would be preferable, but most graphs are sparsely populated and so this would take up a lot of extra space with  unneeded falsey values

12. Give a high level overview of an Adjacency List
- An adjacency list is a way to store the edges of a graph as a linked list. The list would hold a pointer to a head node and those nodes will point to the connected nodes, in order

13. What benefits do we get from an Adjacency List?
- By only holding the data of edges that exist, an adjacency list takes up much less space than an adjaceny matrix (which holds values for edges that don't exist). But, because we are storing each node and it's connected nodes, finding the connected nodes or if there is an edge between nodes is reduced to O(|V|). Adding and deleting nodes is also made easy by inserting them into a list. This takes up less space than an adjacency matrix while giving faster lookup times than a single list.
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
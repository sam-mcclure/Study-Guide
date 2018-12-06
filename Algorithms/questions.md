# Graphs - W1

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

14. What are the steps for DFS on a graph?
-You take your starting node, visit it, and find the vertex connected to it that has the lowest value (ie if start was A, next lowest would be B). That vertex gets added to the stack and then you visit it. You find the lowest value node connected to that node and add it to the stack, repeating the process. When a node has no connected vertices that haven't been visited, you pop it off the stack and check the last node in the stack. Continue until the stack is empty or the given value is found

15. What supporting data structure might you use for BFS and DFS, respectively?
- DFS uses a stack (LIFO) and BFS uses a queue (FIFO)

16.  What are the steps for BFS on a graph?
- You will need to start with an empty queue and a visited array that holds a boolean value for each node, initialized to 0. You take the first node and add it to the queue and change its value in the visited array to 1. You visit it, then add all of its adjaceny nodes to the queue. Until the queue is empty, you visit those nodes, updating their value in the visited array and adding their adjacent nodes to the queue. This continues until each node has been visited or the value is found.

17. Give an example of a use-case for Topological Sort
- File dependencies in a build system. The computer needs to know in which order to download files

18. What is a difference between Topological Sort and DFS?
- For DFS, you print a vertex and then recursively call DFS for its adjacent vertices. In topological sorting, we need to print a vertex before its adjacent vertices. So, a vertex can only be added to the final stack if it has no dependencies.

19. On which types of Graphs can we do a topological sort?
- Directed Acyclic Graph (DAG)

20. What data structure do we use to assist with the topological sort algorithm?
- A set and a stack

21. Explain the steps of topological sort
- Start at a vertex and add it to the set. You then find its children and add them to the set. If a node has no children, it is added to the stack. We keep visiting the children of the nodes in the set until they have all been added to the stack. If there are no children left for the nodes in the set, we pick any other unexplored node and repeat the process. When there are no unvisited nodes, you pop items from the stack until empty and that is the topological order

22. Explain the steps of Djikstra shortest-path algorithm.
- You create a heap map that contains each vertex and a distance that starts at infinity. For the target vertex, you set the distance to 0. You also create an empty parent map and distance map. Use the extractMin method to extract the starting node, setting its parent to null and adding it to the distance map. Then, you find all nodes connected to the starting node and update their corresponding distance from the start and set parent to starting node. You extractMin from the heapMap again, adding the node to the distance map. For every connected node, if it is still in the heapMap, you set its distance to be the length from the current node to its child, plus the length of current node in the distance map. If this value is less than the current child node's distance, you update the distance in the heapMap and the parent node. You continue until there is nothing left in the heapMap.

23. What is the time complexity of Djikstra's algorithm?
- O(Elog(V)). Space complexity is O(V + E)

# Week 2

## Recursion

1. What is a base case in recursion? Why do we need one? Do we always need one?
- A base case returns a value without making any subsequent recursive calls. Recursive problems always need a base case, or else they will run inifinitely and cause a stack overflow. 

2. What exactly is a Stack Overflow?
- When executed, a function is stored in a computer's call stack. For a recursive function, each recursive call adds to the stack, taking up more and more memory. If a base case is never reached, the call stack would get infinitely large and crash the computer. A stack overflow occurs when too many stacks are added and the computer ceases the function in order to protect itself.

3. Describe direct and indirect recursion.
- Direct recursion is when a function directly calls itself. Indirect recursion is when a function calls another function that then calls the original function either directly or indirectly.

4. What is tail call recursion? Why is it helpful, if at all?
- A recursive function is tail recursive when the recursive call is the last thing executed by the function. They are considered better than non-tail recursive functions because tail-recursion can be optimized by a compiler. Since the recursive call is the last statement, there is nothing left to do in the current function, so there is no need to save the current function in the stack call

5. Discuss advantages/disadvantages of recursion
- Recursive programs take up more space and time than iterative solutions, but they are cleaner and simpler to read and write

6. How is memory allocated during recursive function calls?
- When any function is called, the memory is allocated to in on the stack. The memory for each successive call of a recursive function is added to the top of the stack. When the base case is reached, the function returns its value to the function that called it and memory is decallocated until the stack is empty and the function is finished
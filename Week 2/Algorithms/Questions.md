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

## Dynamic Programming

7. What is the difference between Memoization and Tabulation?
- Memoization is top down, you create an empty table at the start and set up the function so that it's broken into small recursive steps. At each step, you either grab the value from the table or calculate the value and then store it in the table. Tabulation is bottom up, you calculate every possible value of i and create a table, returning table[n] in the end. Memoization is generally easier to write and can be more efficient if you don't need to solve every subproblem to get the answer, but it can overall be slower because of many recursive calls. Tabulation can be harder to write, but if you have to calculate all the answers to every subproblem, it's more efficient because it doesn't rely on recursion

8. Why is memoization helpful?
- If you need to use the answer to a subproblem multiple times, like when solving a fibonacci sequence, memoization allows you to store the answers to the subproblems every time you calculate them, so the next time you need to use it, you can look it up in the table rather than calculating it again. This makes the function run much quicker.

9. What is an optimal substructure? When might a problem have one?
- Optimal substructure occurs when the solution to the given problem can be obtained using optimal solutions of its subproblems. This is used for dynamic program problems, such as finding the shortest path between nodes. If a node x lies in the shortest path from source node u to destination node v, then the shortest path from u to v is the combination of the shortest path from u to x and the shortest path from x to v
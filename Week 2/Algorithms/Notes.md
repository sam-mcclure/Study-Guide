# Week 2
## Recursion

* **Recursion** - The process in which a function calls itself directly or indirectly

* In a recursive program, the solution to a base case is provided and the solution of bigger problems is expressed in terms of smaller problems

* The idea of recursion is to represent a problem in terms of one or more smaller problems, and add one or more base conditions that stop recursion. 

* If the base case is not reached or defined, then a stack overflow may occur

* A function is called direct recursive if it directly calls the same original function. A function is called indirect recursive if it calls another function and that function calls the original function directly or indirectly.

* A recursive function is tail recursive when the recursive call is the last thing executed by the function

* When any function is called from main(), the memory is allocated to it on stack. A recursive function calls itself and the memory for the called function is allocated on top of the memory allocated to calling the first function and a different copy of local variables is created for each function call. When the base case is reached, the function returns its value to the function by whom it is called and memory is de-allocated and the process continues

* All problems that can be solved recursively can also be solved iteratively. Recursive programs have greater space and time requirements than iterative problems, but recursive solutions are cleaner and simpler

## Dynamic Programming

* Dynamic Programming is mainly an optimization over plain recursion. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimze it using dynamic programming. The idea is to simply store the results of subproblems, so that we do not have to re-compute them when needed later

* This simple optimization reduces time complexitites from exponential to ploynomial
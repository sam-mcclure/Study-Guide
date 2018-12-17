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

* Do not solve the same problem multiple times, just recall it from memory

* Steps to solve a Dynamic Programming problem:
1. Identify if it is a DP problem
2. Decide a state expression with least parameters
3. Formulate state relationship
4. Do tabulation (or add memoization)

* Typically, all the problems that require you to maximize or minimize a certain quantity or counting problems that say to count the arrangements under certain conditions or certain probability problems can be solved by using Dynamic Programming

* All dynamic programming problems satisfy the overlapping subproblems property and most of the classic dynamic problesm also satisfy the optimal sub-structure property

* Overlapping Subproblems: You need to use the result of the same problem multiple times

* A state can be defined as the set of parameters that can uniquely identify a certain position or standing in the given problem. This set of parameters should be as small as possible to reduce state space.

* In dynamic programming, computed solutions to subproblems are stored in a table so that these don't have to be recomputed. So, DP is not useful when there are no common (overlapping) subproblesm because there is no point in storing the solutions if they are not needed again.

* Memoization is top-down

* The memoized program for a problem is similar to the recursive version with a small modification that it looks into a lookup table before computing solutions. We initialize a lookup array with all initial values as NIL. Whenever we need the solution to a subproblem, we first look into the lookup table. If the precomputed value is there, then we return that value, otherwise, we calculate the value and put the result in the lookup table so that it can be reused later

* Tabulation is bottom up

* The tabulated program for a given problem builds a table in bottom up fashion and returns the last entry from a table. 

* Both tabulated and memoized store the solutions of subproblems. In the memoized version, the table is filled on demand while in the tabulated version, starting from the first entry, all entries are filled one by one. Unlike the tabulated version, all entries of the lookup table are not neccessarily filled in the memoized version

* A given problem has the Optimal Substructure Property if the optimal solution of the given problem can be obtained using optimal soluations of its subproblems.

* Tabulation means starting from the bottom and cumulating answers to the top. 

* For tabulation (bottom up), the state transition relationship is difficult to think about, code gets complicated when a lot of conditions are required, it is fast as we directly access previous state from the table, if all subproblems must be solved at least once, a bottom-up DP algorithm usually outperforms a top-dowm memoized algorithm by a constant factor, and starting from the first entry, all entries in the table are filled one by one

* For memoization (top down), state transition relation is easy to think about, code is easy and less complicated, it is slower due to a lot of recursive calls and return statements, if some subproblems in the subproblem space do not need to be solved, the memoized solution has the advantage of solving only those subproblems that are definitely required, and unlike tabulation, all entires of the lookup table are not neccessarily filled, the table is filled on demand.

* In memoization, initialize a lookup array/table with all of its elements as NIL (constant value). Then call, the recursive function to solve for 'n' using memoization.

* At every step, first check if the table[i] is NIL or not. If its not NIL, return the table[i]. Else, if i satisfies the base condition, we update the lookup table with the base condition and return. Else, f(i) splits the problem i into subproblems and recursively calls itself to solve them. After the recusive calls, return f(i) combines the solutions to subproblems and updates the lookup table and returns the solution

* Time and space complexity of memoization is O(n)

* For tabulation, you build the lookup table in bottom up fashion. After the table is built, simply return table[n]

* Begin with initializing the base values of 'i'. Next, we run a loop that iterates over the remaining values of 'i'. At every iteration i, f(n) updates the ith entry in the lookup table by combining the solutions to the previously solved subproblems. Finally, f(n) returns table[n].

* Memoization uses multiple recursive function calls while tabulation only uses a single function call

* Tabulation works in a bottom up fashion and avoids multiple lookups, this saving function call overhead time. Memoization works in top down fasion, sometimes avoids computing solutions to subproblems that aren't needed, and sometimes is more intuitive to write

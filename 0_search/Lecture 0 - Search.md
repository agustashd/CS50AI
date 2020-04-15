# Lecture 0 - Search

## Terminology
__Agent__: an entity that perceives it's environment and acts upon that environment.  
__State__: a configuration of the environment in which the agent is.  
__Initial state__: where the agent begins.  
__Actions__: a function that retuns the set of actions that can be executed in a state.  
__Transition model__: a function that returns a result based on an action and a state.  
__Goal test__: a way to determine whether a given state is a goal state. Could have multiple goals.  
__Path cost__: numerical cost associated with a given path.  
__Solution__: a sequence of actions that leads from the initial state to the goal state (a state that passes the goal test).  
__Optimal Solution__: the solution with the lowest path cost.  

__Search Problems__ have:
- Initial state
- actions
- Transition model
- goal test
- path cost function

__Nodes__ are data structures for running search programs that keep track of:
- a state
- a parent
- an action
- a path cost

__Frontier__: Data structure that contains all possible (and unexplored) nodes. Starts with a single node, the initial state.

## Search Approach
+ Start with a frontier that contains the initial state.   
+ *(revised)* Start with an empty explored set.  
+ Repeat:
    + If empty then no solution.
    + Remove a node from hte frontier.
    + If node contains goal state, return solution.
    + *(revised)* Add the node to the explored set.
    + Expand node, add resulting nodes to the frontier if they aren't already in the frontier or the explored set.

__DFS Depth-first search__: uses a __stack approach__ to explore nodes, it goes deep into the tree and back if no solution is found. Can always find a solution, given a finite space, but __could not be the optimal one__.

__BFS Breadth-first search__: uses a __queue approach__ to explore nodes, explores the shallowest node in the frontier. __Can find optimal solution__, given a finite space, but it could be __slower__ if the space is big.

__GBFS Greedy best-first search__: search algorithms that expands the node that thinks it's closest to the goal. __Uses a heuristic function__. Given a finite space, __could find optimal solution__ but it's not guaranteed.

__A* search__: search algorithms that expands node with lowest value of *g(n) + h(n)*. __Can find optima solution__, if *h(n)* is __admissible__ (never overestimate the true cost) and should be __consistent__ (for every node *n* and successor *n'* with step cost *c*, *h(n) <= h(n') + c*.  
- *g(n)* = cost to reach node.
- *h(n)* = estimated cost to goal.

__Uninformed serch__: search strategy that uses no problem specific knowledge. DFS and BFS.
Informed search: search strategy that uses problem-specific knowledge to find solutions more efficiently. GBFS

__Manhatan distance__: shortest path to the solution ignoring walls.

__MiniMax__: two agents based on score, one tries to maximize the score and the other wants to minimize it based on an action performed in a state.

>Game example:
>- *S0* -> initial state
>- *Player(s)* -> returns which player to move in state x
>- *Actions(s)* -> returns legal moves in state x
>- *Results(s, a)* -> returns state after action a taken in state x
>- *Terminal(s)* -> checks if state x is a terminal state
>- *Utility(s)* -> final numerical value for terminal state x

It keeps exploring the next state till it finds the optimal solution based on the best posible move the opponent agent is going to make next.

__Optimizations__: 
- **Alpha-Beta pruning**: prevents unnecesary state result checks by keeping track of the already know results from previous states. 
- **Depth-Limited Minimax**: stop looking ahead after x amount of moves and give a result using and evaluation function.
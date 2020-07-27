# Implementation-of-Route-planner
This project uses A star algorithm to find the nearest path from home point to goal point, it is a simple replica of the Google-maps routing algorithm 

A* is an informed search algorithm, or a best-first search, meaning that it is formulated in terms of weighted graphs: starting from a specific starting node of a graph, 
it aims to find a path to the given goal node having the smallest cost (least distance travelled, shortest time, etc.). It does this by maintaining a tree of paths originating 
at the start node and extending those paths one edge at a time until its termination criterion is satisfied.

At each iteration of its main loop, A* needs to determine which of its paths to extend. It does so based on the cost of the path and an estimate of the cost 
required to extend the path all the way to the goal. Specifically, A* selects the path that minimizes

f(n)=g(n)+h(n)

where n is the next node on the path, g(n) is the cost of the path from the start node to n, and h(n) is a heuristic function that estimates the cost of the cheapest path
from n to the goal. A* terminates when the path it chooses to extend is a path from start to goal or if there are no paths eligible to be extended. 
The heuristic function is problem-specific. If the heuristic function is admissible, meaning that it never overestimates the actual cost to get to the goal, 
A* is guaranteed to return a least-cost path from start to goal.

Implementation:
There are a number of simple optimizations or implementation details that can significantly affect the performance of an A* implementation. 
The first detail to note is that the way the priority queue handles ties can have a significant effect on performance in some situations. 
If ties are broken so the queue behaves in a LIFO manner, A* will behave like depth-first search among equal cost paths (avoiding exploring 
more than one equally optimal solution).

When a path is required at the end of the search, it is common to keep with each node a reference to that node's parent. 
At the end of the search these references can be used to recover the optimal path. If these references are being kept then it can be important that the 
same node doesn't appear in the priority queue more than once (each entry corresponding to a different path to the node, and each with a different cost).
A standard approach here is to check if a node about to be added already appears in the priority queue. If it does, then the priority and parent pointers are 
changed to correspond to the lower cost path. A standard binary heap based priority queue does not directly support the operation of searching for one of its elements, 
but it can be augmented with a hash table that maps elements to their position in the heap, allowing this decrease-priority operation to be performed in logarithmic time. 
Alternatively, a Fibonacci heap can perform the same decrease-priority operations in constant amortized time.

# CSC384 - Introduction to AI, Summer 2017

## Homework Assignment 1: Search

The goal of this assignment will be to program a robot to successfully build a snowman in a given spot using snowballs that are located in an obstacle course. The rules hold that only one snowball can be moved by the robot at a time, that snowballs can only be pushed by the robot and not pulled, and that neither the robot nor the snowballs can pass through obstacles (i.e. walls or other snowballs). While snowballs cannot pass through obstacles, smaller snowballs can be stacked atop larger snowballs. Small snowballs can be stacked on large and medium snowballs; medium snowballs can be stacked on large snowballs. In addition, a robot cannot push more than one snowball at a time, i.e., if there are two snowballs in a row, the robot cannot push the both of them simultaneously. The robot also cannot push a stack of snowballs; they must be pushed one at a time.

### Introduction

There are four parts to do in this assignment:

* implementation of a Manhattan distance heuristic. This heuristic will be used to estimate how many moves a current state is from a goal state,
* implementation of Anytime Greedy Best-First Search,
* implementation of Anytime Weighted A*,
* implementation of a non-trivial heuristic for the Snowman Puzzle that improves on the Manhattan distance heuristic.

### Anytime Greedy Best-First Search

Greedy best-first search expands nodes with lowest *h(node)* first. The solution found by this algorithm may not be optimal. Anytime greedy-best first search (which is called *anytime_gbfs* in the code) continues searching after a solution is found in order to improve solution quality. Since we have found a path to the goal after the first iteration, we can introduce a cost bound for pruning: if node has *g(node)* greater than the best path to the goal found so far, we can prune it. The algorithm returns either when we have expanded all non-pruned nodes, in which case the best solution found by the algorithm is the optimal solution, or when it runs out of time. We prune based on the *g_value* of the node only because greedy best-first search is not necessarily run with an admissible heuristic.

### Anytime Weighted A*

Instead of A*s regular node-valuation formula *f(node) = g(node) + h(node)*, Weighted A* introduces a weighted formula: *f(node) = g(node) +w x h(node)* where *g(node)* is the cost of the path to node, *h(node)* the estimated cost of getting from node to the goal, and w ≥ 1 is a bias towards states that are closer to the goal. Theoretically, the smaller w is, the better the first solution found will be. However, different values of w will require different computation times.
Since the solution that is found by Weighted A* may not be optimal when w > 1, we can keep searching after we have found a solution. Anytime Weighted A* continues to search until either there are no nodes left to expand (and our best solution is the optimal one) or it runs out of time. Since we have found a path to the goal after the first search iteration, we can introduce a cost bound for pruning: if node has a *g(node) + h(node)* value greater than the best path to the goal found so far, we can prune it.

## Test cases

The test files can be found in test_script.py file. Different functions can be tested by changing boolean variables in the file.

## Extra details

To get extra details about the specifications of the assignment, please read [Assignment Handout](A1.pdf).

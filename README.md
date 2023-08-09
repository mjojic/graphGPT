# graphGPT
Graph Search using GPT





INTRO: 
"GraphGPT" is an implementation of Breadth First Search (BFS) as a robust text prompt that can used by GPT3/GPT4 to find the shortest path from a certain node to any other reachable node in the environment. For a brief summary: when gpt executes my algorithm, it will look at and record all new nodes that are 1 step away from the start node, then it looks at all new nodes 2 steps away from the start, and so on and so forth until there are no more new nodes that can be reached. It stores all these nodes, their paths, and depths in an array as it traverses the graph, the final path and depth can be extrapolated very quickly at the end.



RELEVANCY:
The general statement I want to make by creating this project is to show that a tool like GPT which simply spits out words in a line is capable of "comprehending" and traversing a graph without error. All graphs are not created equal, so basic pattern recognition will not do the trick if we want something robust. Instead of trying to use my prompt to teach GPT to guess the path just by seeing the graph, I chose to use its pattern recognition to trick it into executing an algorithm. This general thought process is very well outlined in an article on Arxiv titled "GPT is becoming a Turing machine, here are some ways to program it".  https://arxiv.org/abs/2303.14310



NOTE:
Before every “ENDOFSEQUENCE” is a worked out test case that I have provided for GPT to use when it tries to do its graph search. Everything before the last “ENDOFSEQUENCE” is my prompt, but after that line, you can change the nodes of the adjacency list that I included for testing.



USER INTERFACE:
If you want to test my prompt, it is meant to be used on the OpenAI playground on either the "chat" or "complete" mode. The "temperature" should be set to 0, with at least 1600 token max length, and "ENDOFSEQUENCE" should be a stop sequence.
The first setup condition is an adjacency list where: “a = [b, c]” means you can go from point a to b or c. After you create this adjacency list for every node, you must ask gpt if there is a path between two nodes. It will then create a “master list” containing the shortest paths to any node reachable from the starting node in the graph. Finally it will use this list to tell you if the path exists between the nodes you’ve chosen and what the shortest path is. 


FUNCTIONALITY:
The most important part of this is the master list because from that we can find the shortest path to any node in the graph. An important aspect to note when reading my work is that I am adding lots of small sanity checks to force the algorithm to justify itself as it goes. Little things like having the program declare the depth before viewing and adding a new node help to capture the state and maintain some sense of position as it works through the breadth first search.



MASTER LIST:
The path to every reachable node from the starting point is stored within the "master list" which is a data structure I created for the purpose of this project. The master list has a few general rules which can be followed to find the path to any node within the list. 
1: All nodes are encapsulated within brackets depicting their depth. For example if we can reach nodes x and y in one step from node b, the list will look like A= b[1, x, y] where the brackets and the 1 indicate that the node is one step away from the start.

2: All paths of nodes must also be encapsulated again. For example, if we can reach nodes a and b from x, the list becomes A = b[1,[x,[2,a,b]], y]. In this case, x and y are still indicated as being in depth one, but all the paths going through x will now be encapsulated within the outside brackets of "[x,[2,a,b]]

3: In this case, x would be the "parent" node for a and b. because they are within the brackets denoting a path through x. We use this logic to extract the shortest path once all reachable nodes have been explored.

3a: For example: we want to find shortest path from n to y, and the master list for nodes starting from n is is "A = n [1, [x, [2, a]], [b, [2, [z, [3, m]], y]]]". In this case, we see that y is in the group of paths that go through b, as it is nested within those brackets. b is at depth 1, and its adjacent nodes are z and y, as seen by them being nested in the brackets of depth 2. Now we know that the path goes from b to y, and b is only one step away from the starting node n, so the path ends up as n->b->y which takes two steps.

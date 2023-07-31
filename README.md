# graphGPT
Graph Search using GPT


This is a project that I have been working on inspired by my Data Structures and Algorithms class at ASU. I have implemented a modified form of BFS using GPT to prove that these LLM’s can in fact traverse and “understand” a graph.

NOTE:
Before every “ENDOFSEQUENCE” is a worked out test case that I have provided for GPT to use when it tries to do its graph search. Everything before the last “ENDOFSEQUENCE” is my prompt, but after that line, you can change the nodes of the adjacency list that I included for testing.

USER INTERFACE:
The first setup condition is an adjacency list where: “a = [b, c]” means you can go from point a to b or c. After this adjacency list, you must ask gpt if there is a path between two nodes. It will then create a “master list” containing the shortest paths to any node reachable in the graph. Finally it will use this list to tell you if the path exists between the nodes you’ve chosen and what the shortest path is. 

FUNCTIONALITY:
The most important part of this is the master list because from that we can find the shortest path to any node in the graph. An important aspect to note when reading my work is that I am adding lots of small sanity checks to force the algorithm to justify itself as it goes. Little things like having the program declare the depth before viewing and adding a new node help to capture the state and maintain some sense of position as it works through the breadth first search.

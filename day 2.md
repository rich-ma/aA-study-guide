# week 1, day 2
Algorithms, Web, JS, CSS Grid

# Algorithms
---
## Graph Adjacency Matrix
![adjacency matrix](adjacency_matrix.jpg)
- Adjacency matrix takes up V^2 space, which is very memory intensive for something that is sparse, but very good for something that is dense. 
- for sparse maps., it is better to use an adjacency list instead of a matrix.
- basically impossible for all users in a social network to be friends with every other member, so if FB used an adjacency matrix, would be very intensive on memory.
- if you assume that web pages are nodes, and links are directed edges, web pages would have link to only a few other pages, so graph would be sparse, bad fit for matrix.
- if graph is unweighted, we can represent any Ai, Aj to 0 or 1, 0 as non existent, 1 as existent for the edge
- the matrix will be symmetric, for undirected since each edge goes both ways
  - for directed, it is not symmetric, since an edge from a -> b may not be reciprocated from b->a
- The time complexity:
  - Lookup: O(1) if we have the index of the nodes
    - O(V) + O(1) if we need to find the indices
  - finding adjacent nodes O(v), need to scan the entire list to find connections for that node
  - can store a hash table with names as the key, and index as the value
- Space complexity:
  - Space complexity is O(V^2) which can be very large
  - For large companies, this can be an issue, space complexity can be a problem with billions of nodes

- To represent a weighed graph
  - Aij can represent weight of value
    - we can place any value that may not be used to be a valid edge weight, 0, infinity, etc.
- For sparse graphs matrix is a bad idea since there are so many useless spaces
- Example facebook
  - no way that all nodes(users) are friends with all other nodes
  - if we had 10^9 users(a billion), the number of edges would be 10^18, which would take up 1000PB of memory
    - this is huge
    - if users only had 1000 friends on average, there are only 10^11 edges, but we represnt 10^18 possible
  - 

## Graph Adjacency List


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
- Can use a list, either linked list, or a binary search tree, which we can keep it balance
  - by keeping it balanced we can insert, search, and deleting in O(logN)
- many ways to store connections in a node
- using a matrix for sparse graphs stores lots of redundant information
- instead of storing all the connections in a matrix, can just store the connection
  - an array for each node, with values in the array representing the connections
  - just one possible representation
  - Can use linked lists, trees, arrays, etc
  - Binary Search tree is probably the best way, keeping it balanced will have O(logV) for insert, delete, search

### Representation of list
can create an array of pointers
- can keep each row as a pointer to an array 
- can create an array of pointers of size 8, where each pointer points to an array of differing sizes.
  - based on how many connections each node has
  - Space complexity would be O(E), compared to O(V^2) for matrix
  - since most real world graphs are sparse, no wasted space memory.
  - Time Cost:
    - Finding if two nodes are connected: O(V) since we know where the node is, could end up searching the entire array. LogV if we use a binary search tree
      - O(1) for matrix
      - Can use a hash object as well to store
      - keeping an array sorted, can be costly
    - Finding all adjacent nodes:
      - O(v) for matrix, and O(v) for list to find all connections as well.
    - if we assume we are dealing with a sparse graph, we know we will never hit O(v).
  - time complexity of search would be O(V) at worst, but can apply a binary search for O(logV)
  - need to keep rows sorted tho, but can amortize the payment, making it at worse O(V) again.

### Example
- if we were to try to find all friends of a user, assuming we have 1000 firends with a billion users, would be 10^9 cells, assuming we can scan 10^6 cells a second, would still take 16 minutes
- while using a list would take 10^4/10^6, assuming 1000 friends, would take 10ms.
- finding if two nodes are connected would take 1/10^6, which is 1microsecond, in a list, it would take 10ms
- is the tradeoff of 16 mins for finding adjacent nodes worth it for the faster lookup?
  - no, users cant wait that long
  - this assumes a sparse graph

### other operations
-  adding new edges
   -  to store a new edge in a matrix can happen at O(1) time
   -  in a list, hard to insert new edges in an array
   -  can use a linked list to make it better, easier to drop and add edges
      -  at worse O(V) for lookup
      -  would be called an adjacency list
      -  could store 3 values, the node, the weight, and pointer to next node
      -  space would still be O(E + V)
      -  Adding a new connection, or delete a new connection, would be O(V) at worse
      -  binary serach tree much better
      -  

# Flashcards
---

## Give a high level overview of an Adjacency Matrix
- an adjacency matrix is a possible represntation of a graph
- it utilizes a 2d array(matrix) where the rows and columns represent the indexed positions of each node in the array
-  corresponding value at Arr[col][row] represents the existence of an edge between those two
-  For an undirected graph, half the positions(V^2 - v) are wasted since it is mirrored over the diagonal
-  dor a directed graph, there is no reducndancy
-  can also represent a weighted graph with values instead of 0/1


## If we were only concerned about time complexity, is an Adjacency Matrix efficient? Why/why not?
- yes, we can look up an edge in O(1) time
- very fast compared to other models
- if we don't have the index of each node, we will have to search through the nodes and it will be O(V)
- Can create a hash object to store the index of each node, that way we dont need to search through the array each time.
- O(1) lookup, deletion, insertion

## If we were only concerned about space complexity, is an Adjacency Matrix efficient? Why/why not?
- It is poor in space complexity, will take up O(V^2), which obviously grows exponentially, with 10^9 users, takes up 10^18 space, which is 1000PB, giant
- can be very pricey depending on the size of the graph
- 

## Give a high level overview of an Adjacency List
- an adjacency list represents only the edges in a graph, but linked to the specific node vs storing all of them in an array or another object
- 


## What benefits do we get from an Adjacency List?
- saves alot of time on space 
- takes longer to lookup things, but finding all adjacent nodes would be much faster than a matrix would


## What are the benefits of a Javascript closure?


## Formally define a Javascript closure


## Give an example of a closure


## What is data encapsulation?

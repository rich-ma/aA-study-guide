# Algorithm notes

## A Gentle intro to graphs
### loosey-goosey graphs
![trees vs graphs](https://cdn-images-1.medium.com/max/1600/1*rguQ2Y2Z920IYGkO0cHHtQ.jpeg)

- "A Tree is nothing more than a restricted type of graph with more rules, tree will always be a graph, but not all graphs are trees"
- trees can only flow in one firection, from root node to leaf/child nodes, three can only have a one way connection, child nodes have one parent/root note.
- with **graphs**,nodes can be connected in any way possible, there is not one-directional flow like trees, but can be direct or undirected.
  - can have some with direction and some without


### directionality in graphs
![directed vs undirected edges](https://cdn-images-1.medium.com/max/1600/1*nXh55HVMJavGwzSB5jS_-Q.jpeg)
- every graph must have a**t least one node.**
  - considered a **singleton** graph.
- **edges**: (links) connect nodes in any way possible;
  - edges can have directionality/flow, or undirected.
- directed edges:
  - two nodes connected in a specific way, from a -> b, only one way to get from one to another
  - in undirected edges, the travel is bidirectional, can go from a->b->a
- if all edges in a graph are directed it is called a **directed graph(digraph)**
![directed vs undirected graphs](https://cdn-images-1.medium.com/max/1600/1*cS26jONjjQ5ACImJmHhtqg.jpeg)

### What are graphs
- Graphs come from math, graph theory
- In math graphs are: a way to formally represent a network, which is a collection of objects that are interconnected.
- We can consider graphs as ordered pairs, where there are vertices(nodes), and edges(connections)
- mathematical definition for a graph is Graph = (V, E), 
![math def of graph](https://cdn-images-1.medium.com/max/1600/1*zAmHaDww1A31Esup-Rmr-w.jpeg)
- vertices give us each of the nodes in the graph, and the edges give us the directionality or link between these nodes. 
![visualisation of an unordered graph](https://cdn-images-1.medium.com/max/1600/1*goT8sipQbDIoogV6Kc_3KA.jpeg)
- unlike trees, the nodes in a graph are unordered,
- Vertices and Edges are stored in objects, with each edge stored as its own object with two vertices when unordered.
- in **undirected graphs**, the edges are unordered as well
- in **directed graphs**, the ordering of the edges is important since there is directionality, we must know which one goes first.
 ![directed graph](https://cdn-images-1.medium.com/max/1600/1*ThD5bfLUyEx49s5S9qKKow.jpeg)

## Super Social Graphs
- The web is a massive graph structure
- clicking links and urls are going back between different nodes in a graph.
- Some are undirected, can go back and forth between two pages, some only go from one page to another.
- Better example is social networks
- Facebook is an undirected graph, friends go both ways, but snapchat/IG, are directed, users can follow others without being followed back.
  - if users suddenly follow each other, still stays as two seperate edges, since one user could unfollow the other, they are exclusive of each other
-

## intro to graphs video
- edges can connect nodes in any way
- trees are a special type of graph
- graph theory:
  - ordered pairs (a, b)
  - unordered: {a, b}
- web-crawling, browse the web to store data about the web, and search engines store this data to provide accurate results for these queries,
  - basically graph traversal, visiting all nodes in a graph
  -

### Weighted vs Unweighted graphs
- some connections preferable to others
- these edges can have weights that represent friendship level, length, strength, price, etc.
- unweighted graph can be assumed as a weighted graph where all the weights are equal
- undirected graphs can be drawn as directed(bi directional), but directional graphs cannot be converted to undirected. 

# Properties of graphs
- self loop/self edge: edge that points back to the same vertex,(node)
  - can be directed or undirected
  - interlinked webpages can have self loops, going back to the same page
- multi-edge: edge that exists twice in a graph, a->b, a->b
  - can be directed/undirected as well
  - Can reprsent flights between cities, can have multiple flights from city to city
  - can represent different airlines as well, representing flgiht numbers, etc.
- **Simple-Graph**: graph that contains no self-loops or multi-edges.
  - max edges: V(V-1) directed edges, /2 for undirected edges
- Graph is dense of edges ~= vertices, sparse if little edges
- Sparcity will determine what storage structer we will use if it is a very dense( usually an adjacency matrix)
- For sparse graphs, we usually adjacency list.

### Path
- sequence of vertices where each adjacent pair is connected by an edge.< a,b,c,d>
- a path is **simple** if no edge/vertices are repeated
  - also known as a walk
- Trail if vertices are repeated, but not edges
  - Trails are made up of simple paths/walks usually.
  - mutple paths to get to the same vertices

![paths](path.jpg)
- <A,B,E,H,D,A,C> represents a trail, where from A-C there are two seperate paths, <A,C>, or <A,B,E,H,D,A,C>

### Strength of Graph
- Strengly connected if there is a path from any vertex to and other vertex
- If **undirected** its called **Connected**
- if **directed**, its called **strongly connected**
- if a directed graph has edges between all elements, but each node cant go to every other node, its called weakly connected(if we turn the directional to undirected, it would be connected since there is an edge between each node)
![weakly connected graph](graph_strength.jpg)

- Intracity streets should be strongly connected, should be able to reach any street from any other street

## Cycle
- walk is a close walk if it starts and ends at the same vertex, length must be greater than 0, minimum 3.
  - cant go from A-> A, A -> B -> A
- cycle refers to a simple cycle, a closed walk where no other vertex or edge is repeated.
- Acyclic graph: graph with no repeating nodes, no cycles in trees
- **Directed Acyclical Graphs(DAG):** graph where there are no cycles and is directed
- cycles cause issues for algorithsm such as shortest path

# Edge List video
- Can store graph in two lists, one for Vertices, one for edges
- Can use a dynamic list
- vertex is identified by its name
- Can store vertex and edges as strings of the name of the vertex
- graph edges can have weight as well, can be stored in the edge object as another attribute/property
  - very slow, slow lookup,

## time complexity, space complexity
- vertex list by name, can assumes names will be reasonable, space will be basically )(|v|), number of nodes
- for edge list, could just pointers/references to the vertex, would be much more efficient, better to have index of the vertex
  - this way space complexity would be O(|E|), instead of taking up 2|v||e|, where each edge would also store two vertices
- time cost here is pretty high

- to find all adjacent nodes, it would be O(|E|), slow, want it to be O(1), constant
- to chedk if given nodes are connected, also O(|E|), have to check all edges
- O(|E|) is much worse than O(|V|) since edges can be the square of |V| 


- have array VxV, where we have the a matrix with each element as a row, and as a column, and 1 representing a edge between the two, and 0 representing no edge

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
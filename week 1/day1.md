# week 1 day 1, Graphs

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

# Edge List
- 

### Questions
1. How do we define graphs, where are they commonly used?

2. What are the specific attributes that graphs can have, and how do we talk about them?

3. What are some ways we might store a graph in memory? What space/time complexity problems might we face?


# flashcards
 ### How do we define a graph mathematically?
 - a way to formally represent a network, which is a collection of objects that are interconnected.
 - G = (V, E), where V = vertices/nodes, and E = Edges, links
 - 


 ### What is the difference between directed, undirected, weighted, and unweighted?
 - directed graphs have edges where order matters, can only traverse in one direction
 - undirected graphs are bidirectional, can go back and forth between nodes
 - weighted edges represent some attribute between two nodes, time, length, strength, etc.
 - unweighted edges represent a graph where all edges are equal in precedence.
 - 


 ## Give an example of various types of graphs (Weighted Undirected, Unweighted Directed, Unweighted Undirected, etc.)
 - Weighted Undirected: Friendships in facebook, where weight could represent how often users chat/post/interact with each other
  - can also represent freeways between cities where the weight is the distance/time to travel, and the nodes represent cities.

 - Weighted Directed: Can represent Instagram users where the weight is how often the first user interacts with the second, and the direction is from user1 to user2
  - can also represent a streets in a city where weight is the distance/time of travel, and direction represents whether or not the streets are one way or bi-directional

 - Unweighted Undirected: Social network like facebook where users can have friend with equal weight, and friendships go both ways.


 - Unweighted Directed: The world wide web is an unweight directed graph, where links bring you from node to node, and may not always have return edges.  Links have no precedence?(maybe with ads and sponsors, they could have a higher weight on a users search or something)

 ### What makes a graph a simple graph? What attributes would make it not simple?
 - have no self edges or multi edges


 ### What is the maximum number of edges in a directed simple graph? Undirected simple graph? Answer should be in terms of N
- directed: N(N-1), N = number of nodes
- undirected: (N(N-1))/2, half the number of directed edges


 ### Describe the levels of connectivity a graph can have (strongly connected, weakly connected).
 - 


 ### What are cycles?


 ### What are some naive ways we can store and traverse graphs? Be able to discuss time/space complexity of these approaches, and what issues we may face.


 ### What are the three primary Fielding constraints? (Bonus if you can say who Fielding is!)


 ### What sub-constraints make up a Uniform Interface


 ### Walk through an arbitrary example of a RESTful request/response cycle, and describe what makes it RESTful


 ### Give a high level overview of what an object's prototype represents
 
 
 ### What are the differences between the __proto__ and prototype attributes?
 
 
 ### What happens when we do or don't explicity set an object's prototype?
 
 
 ### What is an object's default prototype?
 
 
 ### What are the valid values for an object's prototype?
 
 
 ### Name 5 benefits of HTML5
 
 
 ### What is localStorage? How might you use it?
 
 
 ### Why are media queries useful?
 
 
 ### What is mobile-first design? Be as specific as possible.
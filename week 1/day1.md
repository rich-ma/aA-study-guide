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

### intro to graphs video
- edges can connect nodes in any way
- trees are a special type of graph
- graph theory:
  - ordered pairs (a, b)
  - unordered: {a, b}

### Questions
1. How do we define graphs, where are they commonly used?

2. What are the specific attributes that graphs can have, and how do we talk about them?

3. What are some ways we might store a graph in memory? What space/time complexity problems might we face?


# flashcards
 How do we define a graph mathematically?
 - a way to formally represent a network, which is a collection of objects that are interconnected.
 - G = (V, E), where V = vertices/nodes, and E = Edges, links
 - 


 What is the difference between directed, undirected, weighted, and unweighted?


 Give an example of various types of graphs (Weighted Undirected, Unweighted Directed, Unweighted Undirected, etc.)


 What makes a graph a simple graph? What attributes would make it not simple?


 What is the maximum number of edges in a directed simple graph? 
 Undirected simple graph? Answer should be in terms of N


 Describe the levels of connectivity a graph can have (strongly connected, weakly connected).


 What are cycles?


 What are some naive ways we can store and traverse graphs? Be able to discuss time/space complexity of these approaches, and what issues we may face.


 What are the three primary Fielding constraints? (Bonus if you can say who Fielding is!)


 What sub-constraints make up a Uniform Interface


 Walk through an arbitrary example of a RESTful request/response cycle, and describe what makes it RESTful


 Give a high level overview of what an object's prototype represents
 
 
 What are the differences between the __proto__ and prototype attributes?
 
 
 What happens when we do or don't explicity set an object's prototype?
 
 
 What is an object's default prototype?
 
 
 What are the valid values for an object's prototype?
 
 
 Name 5 benefits of HTML5
 
 
 What is localStorage? How might you use it?
 
 
 Why are media queries useful?
 
 
 What is mobile-first design? Be as specific as possible.
# day 3 notes, DFS

# Algorithms
---
## BFS Graph/DFS Graph explanation

### DFS
- requires a stack
- Starting at the first node, or however you determine where to start, you add that node on the stack, and mark it is visited.
- then you look at its adjacent nodes and visit the lowest/first alphabetically/however you determine to traverse.  
  - you mark that one as visited, then continue this step for this current node
- you continue to visit the lowest node of each node until there are no nodes left to go
- then you go back through the stack, popping them off the stack if there are no new nodes left to visit, and there are no nodes left on the stack, then you are done.
![DFS](DFS.jpg)
- in this example we would go from A-B-E-G
  - then since G has nowhere to go, we would go back to E, which has nowhere, back to B
  - from B we would go to F
  - from F we go to C, then to H, then back to C, F, and then to D
  - from there we should have visited every node and have finished the traversal
  - our result visit owuld have been:
    - A B E G F C H D

## BFS
- Breadth first search utilizes a queue rather than a stack, meaning it is FIFO, rather last LIFO
- guess is that we will visit:
  - A B D G E F C H
- will start at A, but this time, we stay working on A, instead of moving to the next one
- we will visit them in order by alphabetical order/lowest just like in DFS, except we dont move our current node to the next one, but we do visit them
- when we run out of other vertices/nodes to visit, we will dequeue the first one and make it our current vertex/node
![BFS](BFS.jpg)
- 

## DFS Search of graphs
- DFS similar to DF traveersal of a tree, except graphs could have cycles
![DFS](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/cycle.png)
- in this example, can end up in a cycle between 2-0 and 2-0-1 and 3-3
```css
// C++ program to print DFS traversal from 
// a given vertex in a  given graph 
#include<iostream> 
#include<list> 
using namespace std; 
  
// Graph class represents a directed graph 
// using adjacency list representation 
class Graph 
{ 
    int V;    // No. of vertices 
  
    // Pointer to an array containing 
    // adjacency lists 
    list<int> *adj; 
  
    // A recursive function used by DFS 
    void DFSUtil(int v, bool visited[]); 
public: 
    Graph(int V);   // Constructor 
  
    // function to add an edge to graph 
    void addEdge(int v, int w); 
  
    // DFS traversal of the vertices 
    // reachable from v 
    void DFS(int v); 
}; 
  
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 
  
void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v’s list. 
} 
  
void Graph::DFSUtil(int v, bool visited[]) 
{ 
    // Mark the current node as visited and 
    // print it 
    visited[v] = true; 
    cout << v << " "; 
  
    // Recur for all the vertices adjacent 
    // to this vertex 
    list<int>::iterator i; 
    for (i = adj[v].begin(); i != adj[v].end(); ++i) 
        if (!visited[*i]) 
            DFSUtil(*i, visited); 
} 
  
// DFS traversal of the vertices reachable from v. 
// It uses recursive DFSUtil() 
void Graph::DFS(int v) 
{ 
    // Mark all the vertices as not visited 
    bool *visited = new bool[V]; 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 
  
    // Call the recursive helper function 
    // to print DFS traversal 
    DFSUtil(v, visited); 
} 
  
int main() 
{ 
    // Create a graph given in the above diagram 
    Graph g(4); 
    g.addEdge(0, 1); 
    g.addEdge(0, 2); 
    g.addEdge(1, 2); 
    g.addEdge(2, 0); 
    g.addEdge(2, 3); 
    g.addEdge(3, 3); 
  
    cout << "Following is Depth First Traversal"
            " (starting from vertex 2) \n"; 
    g.DFS(2); 
  
    return 0; 
} 
```




# Web
---
## What happens when you type in www.google.com?
1. Browser checks cache for a DNS record to find corresponding IP address of google.com
2. If the request URL is not in the cache, ISP's DNS server initiates a DNS request to find the IP address of the server that hosts google.com
3. browser initiates a TCP connection with the server
4. the browser sends an http request to the web server
5. server handles the request and sends back a response
6. server sounds out an HTTP response
7. browser displays the HTML content(for html responses which is the most common)
8. 
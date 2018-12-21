# Web Architecture and System Design

# RESTful
---
- **RE**presetational **S**tate **T**transfer
- design principles for making network communication more scalable and flexible.
- Answer a few questions:
  - What are the components of the system? 
  - How should they communicate with each other?
  - How do we ensure that we can swap out different parts of the sytem at any time?
  - How can the system be scaled up to serve billions of users?

- Roy T Fielding coined the term in 2000, for his PhD dissertation


# Fielding Constraints
- These constraints are required for a system to be RESTful
## Client Server
  - The network must be made up of servers(source of data) and clients(requester of data)
  - Server is a computer with resource of interest, Client is computer that wants to itneract with the resource stored on the server
  - Client sends HTTP requests to server to access and manipulate information
  - Servers can sometimes act as clients(fetching information from other servers), and sometimes clients can act as servers.
  - NonRESTful alternative would be event-based integration architecture.
    - in this model each component broadcasts events while listening for pertinent information from other components.
    - No one-to-one interactions, only broadcasting and eavesdropping
    - **REST requires one to one communcication.**

## Stateless
  - Stateless means that servers and clients do not have to keep track of each others state
  - When a client is not interacting with server, it has no idea of its existence, only creates connection when necessary, dont need an ongoing link, request-response cycles
  - No record of previous requests either, only standalone requests.


## Uniform Interface
  - Common language between server and client that allows each part to be swapped out or modified without breaking the entire system.
  - Achieved through 4 sub constraints:
    1. Idenfication of resources
    2. manipulation of resources through representation
    3. self descriptive messages
    4. hypermedia
  
### 1. Identification of Resources
- for REST, resource can be anything, HTML document, image, info about a user, weather, etc.
- each resource must be uniquely identified by a stable identifier, meaning it does not change between interactions, and doesn't change when the state of the resource changes.
- Server should give an appropriate response if the request was bad, and give it a link to the new location
- web uses URI to identify resources and HTTP as its communication standard
- When you enter Google.com, your computer makes a GET request to the google servers and if you get a 200 OK response and HTML, your computer will render the response into the webpage so you can view it.
  
### 2. Manipulation of resources through representation
- Client manipulates resources through sending representations(HTTP requests, POST PUT PATCH DELETE, etc) to the server, usually through JSON in an object with the data they would like to add
- like JSON or AJAX
```javascript
{
    method: 'POST',
    url: 'api/likes/',
    data: {
      like: {
        user_id: userId,
        message_id: messageId,
      }
    }
  }  
```
- the user sends HTTP requests to the server, to create, delete, modify, etc
- server takes the request as a suggestion and decides what to do with it
- Vs a GET request, users can modify the page according to their desire, i.e. change the title, picture of a user instead of just getting the users information

### 3. Self-Descriptive Messages
- a message that contains all the information the recipient needs to understand it
- should not be more information in a seperate documentation or in another message.
- example
  - when a user goes to www.google.com the web browser will send a HTTP request like
``` html
GET / HTTP/1.1
Host: www.example.com
```
- this message is self-descriptive, has all the info the server needs to response correctly
- The server will return another self-descriptive response like:
``` html
HTTP/1.1 200 OK
Content-Type: text/html

<!DOCTYPE html>
<html>
  <head>
    <title>Home Page</title>
  </head>
  </body>
    <div>Hello World!</div>
    <a href= “http://www.recurse.com”> Check out the Recurse Center! </a>
    <img src="awesome-pic.jpg">
  </body>
</html>
```
- this response tells the client how to interpret the body, with Content-type: text/html
  
### 4. Hypermedia
- Fancy word for data sent from server to client containing information of what actions the client can do next, what further requests are possible
- in REST, servers should be sending only hypermedia to clients (HTML)
- HTML is a type of hypermedia
- <a href= “http://www.recurse.com”> Check out the Recurse Center! </a> tells the client that it should make a GET request to http://www.recurse.com if the user clicks on the link.
-<img src="awesome-pic.jpg"> tells the client to immediately make a GET request to http://www.example.com/awesome-pic.jpg so it can display the image to the user.


- a system has a **uniform interface** if it has an identifier for each resource, manipulates then through sending representations from the client to server, has self-descriptive messages and composed of hypermedia.
- most important aspect of RESTful systems, allows client to intelligently adapt to changes
- 
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


# HTML 5
## 10. Accessibility
- Using Semantics and ARIA, create accessible sites is easier now
- new HTML semantic tags
  - <article>
  - <aside>
  - <details>
  - <figcaption>
  - <figure>
  - <footer>
  - <header>
  - <main>
  - <mark>
  - <nav>
  - <section>
  - <summary>
  - <time>
- these allow for users to easily access concent, before was hard to determine what a specific div was, now its easier to examine HTML doc for those who use them
- ARIA is a W3C(World Wide Web Consortium) spec that is used to assign specific 'roles' to elements in an html doc
  - creating important landmarks on the page, header, footer, nav, article, using role attributes
  - HTML5 validates these attributes, and will have built in roles that can't be overwritten.

## 9. Video and Audio support
- Support for HTML5 <video> and <audio> tags, don't need to use flash player anymore.
- used to have to use <embed> and <object> tags to assign parameters to get videos to work properly
- now we can use inline styling to get video sizing<video src=”url” width=”640px” height=”380px” autoplay/>
- nowadays everyone is using HTML5, so don't need to embed, but might have to check every browser for its 

## 8. Doctype
- Can Easily decalre doctype now, don't need long lines of head tags with doctype attributes


## 7. Cleaner Code
- allows you to write cleaner, more descriptive, semantic code to seperate meaning fro style and content
- no more divs on divs on divs, and classitis, HTML headers and semantic tags fix this issue.
```html
<div id="header">
 <h1>Header Text</h1>
 <div id="nav">
  <ul>
   <li><a href="#">Link</a></li>
   <li><a href="#">Link</a></li>
   <li><a href="#">Link</a></li>
  </ul>
 </div>
</div>
```
vs. 
```html
<header>
 <h1>Header Text</h1>
 <nav>
  <ul>
   <li><a href="#">Link</a></li>
   <li><a href="#">Link</a></li>
   <li><a href="#">Link</a></li>
  </ul>
 </nav>
</header>
```

## 6. Smarter Storage
- Local storage allows a mix of old cookies and client side database. 
- allows for storage across multiple windows, has better security, and data persists after a browser is closed
- is essentially client side db, dont have to worry about user deleting cookings and is adopted by all popular browsers
- local storage allows for web apps that don't require third party plugins.
- allows you to store user info, cache data, and load previous stat.

## 5. Better Interactions
- allows for better interactions and dynamic websites.
- users can interact with a <canvas> that allows them to interact with, and for you to animate
- html5 also comes with new APIs that allow you to build better UX such as
  - drag and drop
  - offline storage db
  - browser history management
  - document editing
  - timed media playback

## 4. Game Development
- Can develop games using <canvas>. HTML provides mobile friendly way to develop fun interactive games

## 3. Legacy/Cross Browser Support
- HTML5 was developed so that all browsers can use it.
- even if a browser doens't like it, we can add a JS script that will convert it back.
- 

## 2. Mobile, Mobile, Mobile
- HTMl5 replaced mobile flash, is very mobile friendly
- mobile browsers fully adopted html5, and allow for easy responsive, mobile first design.
- great meta tags for mobile:
  - Viewports: allow you to define viewport widht and zoom setting
  - Full screen browsing: ios specific values that allow apple devices to display in full screen mode
  - home screen icons: like favicon on desktop, icons are used to add favirotes to the home screen of an ios and android device

## 1. Its the future(now?)
- use it

# Responsive web design - Media Queries
- Media Queries are something new to CSS3, it uses the @media rule to include css rules only if certain conditions are true
```css
@media only screen and (max-width: 600px) {
  body {
    background-color: lightblue;
  }
}
```
- this code will only exist if the max-width of the screen is 600px or smaller
- we can apply this to add breakpoints to rows and columns to look better on a smaller format, and be responsive if a user resizes
```css
/* For desktop: */
.col-1 {width: 8.33%;}
.col-2 {width: 16.66%;}
.col-3 {width: 25%;}
.col-4 {width: 33.33%;}
.col-5 {width: 41.66%;}
.col-6 {width: 50%;}
.col-7 {width: 58.33%;}
.col-8 {width: 66.66%;}
.col-9 {width: 75%;}
.col-10 {width: 83.33%;}
.col-11 {width: 91.66%;}
.col-12 {width: 100%;}

@media only screen and (max-width: 768px) {
  /* For mobile phones: */
  [class*="col-"] {
    width: 100%;
  }
}
```

- in this code, the columns will reorganize to one col if the size is too small.
- super common in modern websites

## Always design mobile first
- mobile first means designing for smaller format before desktop or other devices
- this allows for the site to load faster on mobile devices
- instead of putting the media query looking for a min size, you start with the columns and expand if the width is wider.
```css
/* For mobile phones: */
[class*="col-"] {
  width: 100%;
}

@media only screen and (min-width: 768px) {
  /* For desktop: */
  .col-1 {width: 8.33%;}
  .col-2 {width: 16.66%;}
  .col-3 {width: 25%;}
  .col-4 {width: 33.33%;}
  .col-5 {width: 41.66%;}
  .col-6 {width: 50%;}
  .col-7 {width: 58.33%;}
  .col-8 {width: 66.66%;}
  .col-9 {width: 75%;}
  .col-10 {width: 83.33%;}
  .col-11 {width: 91.66%;}
  .col-12 {width: 100%;}
}
```

## multiple breakpoints(media queries)
- you can add multiple breakpoints to be even more responsive, one for under 800px, and one for under 600px
- this will allow the page to change depending on different devices or user interaction
```css
/* For mobile phones: */
[class*="col-"] {
  width: 100%;
}

@media only screen and (min-width: 600px) {
  /* For tablets: */
  .col-s-1 {width: 8.33%;}
  .col-s-2 {width: 16.66%;}
  .col-s-3 {width: 25%;}
  .col-s-4 {width: 33.33%;}
  .col-s-5 {width: 41.66%;}
  .col-s-6 {width: 50%;}
  .col-s-7 {width: 58.33%;}
  .col-s-8 {width: 66.66%;}
  .col-s-9 {width: 75%;}
  .col-s-10 {width: 83.33%;}
  .col-s-11 {width: 91.66%;}
  .col-s-12 {width: 100%;}
}

@media only screen and (min-width: 768px) {
  /* For desktop: */
  .col-1 {width: 8.33%;}
  .col-2 {width: 16.66%;}
  .col-3 {width: 25%;}
  .col-4 {width: 33.33%;}
  .col-5 {width: 41.66%;}
  .col-6 {width: 50%;}
  .col-7 {width: 58.33%;}
  .col-8 {width: 66.66%;}
  .col-9 {width: 75%;}
  .col-10 {width: 83.33%;}
  .col-11 {width: 91.66%;}
  .col-12 {width: 100%;}
}
```
- in this code, there are two classes .col-# and .col-s-#, s probably meaning small
- can change the sizes to target certain devices:
  - phone, tablet, phone landscape, tablet landscape, laptop, wide screen
```css
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...} 

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...} 

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...} 

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...} 

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...}
```
- media queries can also be used to change based on orientation of the browser
```css
@media only screen and (orientation: landscape) {
  body {
    background-color: lightblue;
  }
}
```

- can use media queries to hide objects as well
```css
/* If the screen size is 600px wide or less, hide the element */
@media only screen and (max-width: 600px) {
  div.example {
    display: none;
  }
}
```
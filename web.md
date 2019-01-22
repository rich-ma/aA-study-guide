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

# CSS Grid
- fundmental to website design
- native support from major browsers
- Core ingredients are:
  - Wrapper(parent)
  - items(children)
- The wrapper is the actual grid, and the child elements are the content inside the grid.
```html
<div class="wrapper">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
```
- all we need to do is all display: grid; to the .wrapper class in css.
- then we need to define how we want to grid to look by adding columns and rows.
  - using 'grid-template-columns', and 'grid-template'rows'
  - the number of arguments you put into each one will dictate not only the number of those elements, but the respective widths as well.

```css
.wrapper {
    display: grid;
} 
```
![without_grid](no_grid.jpg)
- grid before setting the grid-template-columns/rows
- will just be regular block looking setup

```css
.wrapper {
    display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 50px 50px;
}
```
![grid](grid.jpg)
- from our css above, we get 3 columns of 100px each, and two rows of 50px height.

```css
.wrapper {
    display: grid;
    grid-template-columns: 200px 50px 100px;
    grid-template-rows: 100px 30px;
}
```
- this would create a grid where the first col is 250px, second 50px, and third 100px
- the first row would have a height of 100px, and second 30px, sign smaller.
![grid2](grid2.jpg)

## placing items
- if you create a grid that is larger than the number of elements, it will only fill the elements that you have.
- grids are indexed starting at 1, so regular counting
- if you want to resize/place an item, you can dictate its starting and ending position by using css
```css
.item1 {
    grid-column-start: 1;
    grid-column-end: 4;
}
```
- this tells the first item to start at the first position, and end on the 4th, 
- sounds like it would go down to the first col in the second row, but how CSS grid names its columns is a bit weird
![grid columns](grid_col.jpg)
- grid lines start at the beginning, and flank left and right of each column, meaning there are always column + 1 grid lines.
  - if we had 5 columns, and wanted an item to take up the middle 3, we would start at 2 and end at 5.
- instead of writing 'grid-column-start' and 'grid-column-end', we can use:
```css
.item1 {
    grid-column: 1 / 4;
}
```
- can even use 'grid-row-start' and 'grid-row-end' if we want to change its vertical representation on the grid.
- can you combine both?
```css
.item1 {
    grid-column-start: 1;
    grid-column-end: 3;
}
.item3 {
    grid-row-start: 2;
    grid-row-end: 4;
}
.item4 {
    grid-column-start: 2;
    grid-column-end: 4;
}
```
![custom_grid](custom_grid.jpg)

can use span to determine how many spaces to take up as well
- can combine grid-column and grid-row
- can use grid-area for more efficiency
  - grid-area: grid-row-start, grid-column-start, grid-row-end, grid-column-end.
    - ex: grid-area: 1/1/3/6;
- using 'order' allows us to determine the 'order' in which grids are placed.
- when creating the grid, can use grid-template-columns/rows and repeat(number, size/%) to repeat the code without having to type it all out. 
  - grid-template-columns: 20% 20% 20% 20% 20%;
  - grid-template-columns: repeat(5, 20%);
  - can use pixels, %, ems, and able to mix them
  - can use fractions as well, 1fr, 3fr will create 4 columns of equal size;
  - by using fr, you can take up remaining space as well, for example
    - 50px 1fr 2fr 50px, will split the space between the 50px into thirds.(1/3, 2/3 respectively)

- just like grid-area can be used to shorthand what position a box is in for both row and columns, grid-template does the same for the template
  - 
![grid-template](grid-template.jpg)
![grid-template](grid-template2.jpg)



## What happens when you type in www.google.com?
1. Type in Maps.google.com
   
2. Browser checks cache for a DNS record to find corresponding IP address of google.com
- DNS(Domain Name System) is a database that maintains name of websites(URL) and the IP address linked to it
- every URL has a unique IP address, which belongs to the computer that hosts the server of the website that we are visiting.
- for example, google's IP is http://209.85.227.104, which you can visit
   - DNS is like a phonebook for websites, listing URLs and their respective IP addresses
- Browser will check four caches to find the DNS records
  - First, checks browser cache to see if it is in our list of previously visited sites, which our browser stores for a fixed duration
  - Second, browser checks the OS cache, a system call(i.e. gethostname on Windows) to your computer OS, since your computer also has a cache of DNS records
  - third, it checks the router cache, which stores its own records as well
  - Fourth, it checks the ISP(Internet service provider), last one
- not the best in terms of security, but cache's are important to network traffic and improving data transfer time.

3. If the request URL is not in the cache, ISP's DNS server initiates a DNS request to find the IP address of the server that hosts google.com
   - If the URL is not in any of the four caches, ISP's DNS will intiate a DNS query to find the IP address at the server that hosts the site you are trying to go to(maps.google.com)
   - It will search multiple DNS servers on the internet until it finds the correct IP address for the URL(Website).
   - this is a **recursive search** since the search will continue repeatedly from DNS server to DNS server until it either finds the IP Address or returns an error saying it was unable to find it.
   - The ISPs DNS Server will now become the **DNS Recursor** whose job is to find the correct IP Address for the domain by asking other DNS Servers.
   - The other DNS servers would be called **name servers** since they would doing a DNS search based on the website domain name.
  ![DomainArchitecture](https://cdn-images-1.medium.com/max/1600/0*udK6jZ3PjlhjqW8U.png)
    - most sites today have a third-level domain, second, and a top level domain.
    - Each of these levels contain their own name servers which is queried during the DNS lookup
    - Ex. maps.google.com
      - First DNS Recursor(searching ISP DNS) will contact the root name server, which will redirect it to the top-level (.com) name server.
      - the top-level name server(.com) will redirect it to the second-level name server (google.com)
      - second-level(google.com) will now find the matching IP for maps.google.com in its DNS records and return it to the DNS Recursor from your ISP, which will send it back to your browser
    - These requests are sent using small data packages 
      - The contain information such as the content of the request, and the IP Address it is destined to(DNS Recursor/ISP DNS Server address)
      - The packets travel through multiple networking equipments before finding the correct DNS Server and going back to your DNS server and eventually your browser
      - They use routing tables to figure out the fastest way for the packet to reach its destination
      - If the packet gets lost, it will send a request failed error.
   
4. browser initiates a TCP connection with the server
  - once the browser receives the correct IP address it will build a connection with the server that matches IP address to transfer information
  - Browser uses internet protocol to build these connections, most common is TCP for HTTP requests.
  - to transfer data between your computer(client) and the server it is important to have a TCP connection.
    - uses the TCP/IP three-way handshake. Three set process where the client and server exchange SYN(sycnhronize) and ACK(Acknoledge) messages to establish a connection
  - The three steps are:
    1. Client machine sends a SYN packet to the server over the internet, asking the server if it is open to new connections
    2. If the server has open ports that can accept and initiate new connections, it will respond with a SYN/ACK packet in acknowledgement of the SYN packet.
    3. Client receives the SYN/ACK packet and will send an ACK packet to the server.
    4. TCP connection is established and ready for data transmission.


5. the browser sends an HTTP request to the web server
   - Once a TCP connection is made, you can transfer data.
   - Browser will send a GET HTTP request for maps.google.com web page
   - Can also be a POST request if you are entering credentials or submitting a form.
   - Request will contain other information such as browser identification(User-Agent Header), types of requests it will accept(Accept header), and connection headers asking it to keep the TCP connection alive for future requests.
   - Will also send data from the cookies stored on the browser.
 - Sample GET request header:
![get_request](https://cdn-images-1.medium.com/max/2000/0*SyxEqHOBZElX5laf.png)
- 
   
6. server handles the request and sends back a response
    - Server contains a web server(Apache, IIS, Rails, etc), which will receive the request from the browser and passes it to the request handler(router/controller in rails)
    - the hander that reads the request, its header, and cookies to see what is being requested and updates the information on the server if needed. 
    - it then assembles a response in a particular format(JSON, XML, HTML)
      - in Rails would send it out to the model and the model will hit the DB for the request and usually come back with some sort response


7. server sounds out an HTTP response
   - The server response contains the web page you requests and the status code, compression type(content encoding), how to cache the page(cache control), any cookies to set, privacy info, etc.
![HTTP_server_response](https://cdn-images-1.medium.com/max/1600/0*ifRt45gihG_AwR3Z.png)
- looking at the response, you can see the status code, indicating the status of the response
  - 1xx indicates informational message only
  - 2xx indicates success of some kind
  - 3xx is a **redirect** code for the client to go to another URL
  - 4xx indiciates an error on the clients end
  - 5xx indicates an error on the server end.

8. browser displays the HTML content(for html responses which is the most common)
    - the controller will send back the HTTP response and the browser will take in the data and display the HTML content
    - this happens in phases, first it will render the bare bone HTML skeleton
    - then it wil check HTML tags and set out get requests for additional elements on the page such as images, CSS stylesheets, JS files, etc.
    - The static files are cached by the browser so it doesn't have to fetch every time you visit the page.
    - Then you will finally see maps.google.com.  this process goes very quickly for modern internet and caching systems.
  
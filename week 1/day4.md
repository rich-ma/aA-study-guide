# Notes

# Algorithms
## BFS Reading and code


# DNS and how you can make it better
- Domain Name System(DNS) is the backbone of the internet.
- run by many engineers and their organizations, shapes future of the internet

## how does the internet work?
- If you go to freecodecamp.com what happens?
  1. Your browser doesn't know the IP of freecodecamp was, so it couldnt connect to and retrieve those files.  
  2. It looks at its browser cache for the IP, then the OS, then your router, then finally the ISP DNS cache
  3. if its in none of those, it will start a DNS request where the Server DNS becomes a DNS Recursor(queries a DNS Resolver) going to the top level domain, secondary, etc until the IP is found.
  4. then it will attempt to intiate a TCP/IP threeway handshake.
     1. Client sends a Synchnronize(SYN) request to the server
     2. server sends back a SYN/ACK response
     3. client sends back a ACK response
     4. handshake is now complete
https://www.verisign.com/en_US/website-presence/online/how-dns-works/index.xhtml

## Who makes it work?
- IANA, ICANN
- Internet works because of protocols and policies that have enough consensus to become universal norms.
- Internet Assigned Numbers Authority(IANA) control how domain names and IP addresses are mapped
- madate of making sure correct technical procedures are in place to have a safe and stable DNS.
- Internet Corporation for Assigned Names and Numbers(ICANN) provides technical operations of vital DNS resources, it also defines policies for how the "name and numbers" of the internet should run.
  - moves in a 'bottom up, consensus driven, multi stakeholder model'
  - Moved from US Department of Commerce to the autonomous control of ICANN.
  - has a board of directors and as a body, is divided up into seperate member groups
  - inclusive approach treats public sector, private sector, and tehcnical experts as peers.
  - in the ICANN community, you'll find registries, registrars, ISPs, Intellectual property advocates, commercial and business interests, non-commercial and non-profit interests, representation from over 100 govt's, and a global array of individual internet users.
![ICANN_members](https://cdn-images-1.medium.com/max/1600/1*bmNP6V25oKJkvCuQwEsshw.png)
- not all are represented equally
- those with more financial stake will try to lobby their way

## What can you do?
- Be more involved as an end user, billions of users whos voices are not heard.
- can join At-Large, a end user contingent of ICANN, 

# React 16 lifecycle methods
- 


# Javascript callstack, concurrency, event loop
- javascript is a single threaded non-blocking asynchronous, concurrent langauge
- has calls tack, event loop, callback queue, and other apis
- JS call stack functions like a regular call stack, LIFO(last in, first out)
![callstack](callstack.jpg)

- blocking
  - code that is slow, console.log is fast, network requests slow, etc
  - blocking is an issue becuase it locks you out from being able to do anything on the web.
    - big issue, which is why we are given concurrency and event loop

- Asychronous requests
  - code gets stuck, can't do other things until others are done
  - simplest solution is asychronous callbacks
    - run the code later after everything else is done
  - set timeout gets put on the stack, but just disappears, goes to event loop
  ![asych](asych_call.jpg)

## Concurrency and Event Loop
- Where does the settimeout go after the stack?
- JS lets us do concurrency since browser can do more than just the JS runtime(which can only do 1 thing at a time)
- browser gives us WebAPIs that let us access like threads, and where concurrency happens
- threading is hidden, run somewhere else
- setTimeOut gets called, goes on the stack, then goes to the API call for setTimeOut(External API)
![concurr1](concurr1.jpg)
- then browser will set the countdown for you, and since it is done, it will remove itself from the stack.
![concurr2](concurr2.jpg)
- now rest of code can be called, (console.log('JSConfEU')) 
- after the asynch call is done(setTimeOut), it will enter the queue(task queue), and wait for the stack to clear until it will be called
![concurr3](concurr3.jpg)

## Event Loop
- one job, look at the stack, and the stack queue
- if stack is empty, it will grab the first thing in the queue(first in first out, FIFO)
- now that stack is clear, will move the callbck to the js stack, and in this case, will call the console.log('there'), and put that on the stack as well
![concurr4](concurr4.jpg)


### ex. SetTimeOut(0)
- if you want to defer sometime until stack clears, use a time of 0 for setTimeOut, will complete immediately, but dont happen until the normal stack clears.
- setTimeOut isnt gaurantee to run in that time, that is the minimum time it will take to complete.

callback:
- any function that another function calls
- can be an asychnronous callback, that will be pushed onto callback queue in the future.
- by using asych we are able to not block the call stack, otherwise the browser will be 'blocked up' and unable to repaint, or allow user interactions.
- by using asynch we can give the browser a chance to repaint between event loop.

- can also flood the callback queue, only do slow work every few seconds, or until user stops scrolling, not during all user inputs.



# Flashcards

1. What are the steps for BFS on a graph?
  - Starting at the starting node, look and visit all adjacent nodes, then move to the lowest/first of those nodes and visit those in order as well,
  -  add these visited nodes to the queue in order
  - continue this until you get to a node that has no new nodes to visit
  - then go through the queue in this same process, dequeue from the front and add any new nodes when one has them.
  - once the queue is empty you are done.

2. How does DNS work?
   - 


3. UPDATE EXISTING CARD What's the event loop? How does it work?


4. What lifecycle methods get called in the mounting phase? What are the use cases for each of those methods?

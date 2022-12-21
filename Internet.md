# Internet

## HTTP

- Protocal designed to transfer info over networked devices
- Flow is usually client sends request, server handles request
- Proxies in between clients that serve various purposes such as caching, loadbalancing etc
- Each request has version type, url, method, headers
- Methods tell you what kind of request you are making for example
- > "get" expected no info from client, while "post" does
- Header provide meta data that tells servers various info such as format and method
- The request body is optional.  It is the main contant of the request.
- Response have a status code to tell the client how it went, headers and body
- 1XX info, 2XX success, 3XX redirect, 4XX client error, 5XX server error
- Since in older versions of http, tcp connection opens and close after each request.
- These leaves site vulnerable to DOS attacks since people can keep making requests and 
eventually trigger site crashes due to heavy resource use
- HTTP 1.0 seperate connection for each request
- HTTP 1.1 added pipelining and persistant connections, was hard to implement
- HTTP 2.0 multiplexing messages over a single connections, binary content for faster transmission but not human readable

## IP

- #.#.#.#  255 of each represents the IP address (v4)
- Your ISP gives you an IP
- Each device gets its own IP
- DHCP is software that ISP uses to get a unique address for your device
- The router may also support DHCP

## DNS

- Domain name is like google.com. This is a human readable address.
- DHCP provides access to DNS servers.
- DNS server converts domain to the IP.
- Its usually not one server but many that escalate up the tree of different servers to find the corresponding domain name.

## Packets

- All the data transmitted from server to client comes in small packets.
- Stores IP of devices and domain
- The request is made to DNS to get IP of where we send the packet to.
- It needs to send this in packets to not block traffic for other clients
- Server has to provide the number or packets
- Packets are part of IP.  Addressing, fragmentation but nothing about what to do if we have missing packets

## TCP/IP

- TCP will allow for sending back of any missing packets

## Ports

- Ports can help it determining what kind of request you are making.
- Which server do we send this to?
- Ports will be usually reserve for certain kinds of requests.
- 80 HTTP
- 25 Email
- FTP etc

## Protocols

- A standard or a set of rules
- HTTP protocol is the rule that if I make a request with right info I should get what I requested back

## UDP

- Does not guerantee delivery
- Video conference since buffering may cause performance issues
- Infer from the context, we trust that the user will make sense

## IPs in more detail

- (32 bit) 4 billion IP with v4 which is not enough to support the amount of devices we have.
- 128 bit address will have alot more
- Something with 10... is usually private
192.168...172.16
- These IP usually come from a router
- Subnet mask is used to see if another computer is on the same network as you

## Routers

- Router/Gateway - looks at the first few numbers of IP and makes sures to route it to the approprate network (next hop)
- 30 or fewer hops
- Internet is a network of a network

## Exploring trace routing
```bash
traceroute www.amazon.com
```
```bash
traceroute to www.amazon.com (13.35.150.53), 30 hops max, 60 byte packets
 1  LAPT-110.mshome.net (172.20.0.1)  0.364 ms  0.166 ms  0.151 ms
 2  router.sagemcom.net (192.168.1.1)  1.672 ms  4.649 ms  4.633 ms
 3  10.252.60.70 (10.252.60.70)  223.888 ms  231.300 ms  140.124 ms
 4  * * *
 5  * * *
 6  * * *
 7  * 203-219-106-141.tpgi.com.au (203.219.106.141)  40.278 ms syd-sot-ken-crt1-te-gi-0-4-0-9.tpgi.com.au (203.219.106.113)  50.912 ms
 8  60-240-241-130.s
```

Each number represents a hop
"*" mean the router is not responding
It usually starts with local then go to the gateways
Tells time with every hop

## Browsers

### Architecture of Browser

- UI - allows user to interact with visual elements on the page
- Browser engine - bridge btw UI and rendering engine.  Manages queries btw them
- Rendering engine - parses and interprets the HTML, CSS
- Networking - provides support for HTTP and FTP
- Javascript interpreter - parsing and executing javascript code
- UI-backend - draws basic widgets
- Data storage - local storage though stuff like cookies

Rendering engine steps
1. HTML parsed into chunks, along with css.  Elements converted to DOM nodes
2. Creates render tree.  Ensures content is provided in a certain order
3. Layout of the tree is determined.  Evauates exact coordinates
4. Each node is painted using the UI-backend





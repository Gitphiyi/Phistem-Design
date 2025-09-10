# Load Balancing
Role: distribute incoming client requests to computing resources such as application servers and databases
- Prevent requests from going to unhealthy servers
- Prevent overloading resources
- Help to eliminate a single point of failure

## Rules:
- Every server needs to be the same codebase. This is because if the code is different on each server then if a server falls down the work done on it can't be easily redirected by the load balancer to another machine. Thus all information on sessions (user data, profile pictures, etc) need to be stored on a centralized data store (Redis or DB).

## Types of Load Balancers:
- Random
- Least Loaded
- Round Robin
    - This can also be weighted where servers with higher weights receive a larger proportion of traffic
- Sticky Session Cookies
    - once a client starts a session with a server all future requests from the client go to the same server
    - Sets a special cookie to Server and Load Balancer looks at cookie to send to correct server
- Layer 7 Load Balancing
    - Routes based on URL, headers, cookies, etc
    - Loud Balancer can decrypt HTTPS and offload the decrypting from the server
    - For example it can be based on the path. all /API requests go to api servers and /images requests go to image servers
- Algorithmically Determined
- IP Hash
    - Routes based on a client IP to basically ensure cache affinity (cache hits)
- Network Load Balancers
    - BGP: network protocol used to determine the path packets take between networks
    - CDN: Edge server can serve as a place to prevent DDOSS, cache static assets, and receive requests from nearby clients 
- Least Response Time
    - Depending on how fast the app responds to a dummy request the load balancer chooses the app with the least amount of time to respond to send the packet to
## Reverse Proxy
- Serves as a web server that centralizes internal services and provides unified interfaces to the public. Requests from clients are forwarded to servers
- Will do things like hide info about backend servers, blacklist IPs, limit # of connections per client
- Increase Scalability as Client only sees reverse proxy's IP
- Decrypt incoming requests and encrypt server responses so backend servers don't have to do these tasks
- Can Compress server and client packets
- Cache packets and server static content directly
- Can deploy a load balancer on a reverse proxy
- Issue is it can act as a point of failure, so maybe more than one reverse proxy is needed


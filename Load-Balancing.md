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
- Sticky Session Cookies
- Layer 4 Load Balancing
    - Look at Transport layer and 
- Algorithmically determined
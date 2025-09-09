# Cracking System Design Notes
## Interview Template
### Scope Clarification:
- Who are the users? Where do they reside?
- What are we focused on? Main goal?
- How will users interface with our product?
- Everything I need to justify my decision
- Identify functional requirements (what system must do) and non-functional requirements (scalability, latency, reliability, security, etc)
    - Identify where my interviewer is more interested in one aspect or another
    - Non-Functional = identify if a system is read/write heavy, exact memory constraints, etc.
    - These are used for technological tradeoffs
- Scope down a design into something manageable if necessary

### Estimation:
- Estimate numbers to justify design choices
- Estimate stuff like # of writes and size of data to understand memory constraint, # of users and how many times they perform actions to estimate read/write states, and what are the # of requests sent per second.

### Design API:
- Show what API is exposed to the users as this will help lead to discussing the internals
- Choose API protocol: gRPC, graphQL, REST

### High Level Design:
- Sketch essential components: Load balancers, app servers, databases, caches, queues
    - Keep concise and avoid going deep into details
- Review data flow (request cycle)
- Database choices and schema at high level

### Deep Dive Design:
- Pick 1 or 2 interesting subsystems to deep dive into
    - My pick should be Databases and Load balancers as I often had to deal with this

### Bottlenecks & Tradeoffs:
- Identify possible bottlenecks (DB hot spot, cache thrash, queue backlog).
- Explain mitigation (replication, partitioning, load balancing, CDN).
- Mention reliability strategies: failover, retries, monitoring, alerts.
- Call out CAP theorem tradeoffs

### Summarize 
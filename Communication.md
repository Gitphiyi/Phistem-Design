# Communication

## Types of Communication
- REST
    #### When to use REST
    - Expose external API
    - Human readability and debugging
    - Interoperability across languages
- RPC
    #### What is RPC?
    A client causes a procedure to execute on a different address space. THe procedure is coded like a local procedure call, and the details of how it works is abstracted away. 

    #### RPC Request-Response Protocol
    - Client Program calls client stub procedure. Parameters are pushed onto the stack like local procedure call
    - Client Stub Procedure marshalls (packs) procedure id and arguments into a request message
        - Data structures and other arguments are converted to things like JSON, Protobuf, or Avro
        - HTTP request is built where the body is the serialized data
        -
    - Client Communication Module uses OS to send the message from client to server
    - Server Communication Module uses OS to pass incoming packets to Server Stub Procedure
    - Server Stub Procedure unpacks the packets, calls the server procedure matching the procedure id and passes the given arguments
    - The server response repeats steps above in reverse order

    #### When is RPC choosed over REST
    - Tight Coupling: the distributed components of a system are designed to work together and changing one will likely impact the other. It is unlikely the component will have to be adapted to communicate with other systems in the future
    - Reliable Communication: Components communicate on a network that is unlikely to experience latency issues, packet loss, etc.
    - Unform Language: components all written in a single language
    - High throughput and low latency (Serialization like Protobuf is smaller and faster than JSON)

    #### Disadvantages
    - Client is tightly coupled to service implementation
    - New API defined for every new operation or use case
    - Hard to debug RPC
    - Larger setup overhead
    - Browser support is weaker
- HTTP
- TCP
- UDP
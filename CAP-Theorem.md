# CAP Theorem
- You can only support 2 of the following guarantees
    - Consistency = Every read receives the most recent write or an error
    - Availability = Every request receives a response, without guarantee that it contains the most recent version of the info
    - Partition Tolerance = system continues to operate despite arbitrary partitioning due to network failures
**NOTE: Networks aren't reliable, so you'll need to support partition tolerance. You'll need to make a software tradeoff between consistency and availability**

### CP - consistency and partition tolerance  
Waiting for a response from the partitioned node might result in a timeout error. CP is a good choice if your business needs require atomic reads and writes.
### AP - availability and partition tolerance
Responses return the most readily available version of the data available on any node, which might not be the latest. Writes might take some time to propagate when the partition is resolved.

## Consistency patterns
### Weak Consistency
After a write, reads may or may not see it. A best effort approach is taken. This is like caching layer with no invalidation. You might  read something old, and there isn't a promise it will be updated anytime soon
### Eventual Consistency
After a write, reads will eventually see it (within MS). Data is replicated async. This approach is seen is systems such as DNS and email. For example, if you update your ig bio, some friends see old one, but eventually the feed will reflect the change.
### Strong Consistency
After a write, reads will see it. Data is replicated synchronously. This approach is seen in file systems and RDBMSes. Strong consistency works well in systems that need transactions
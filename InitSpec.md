# Project Specification

## Goals

Performance

Scalability

Reliability

Availability

## Research on existing products
Research work will start from GFS and HDFS because these projects are open-source and the design process of architecture is well documented in published paper.

### Google File System ('GFS')
#### Assumptions
1. The system needs to monitor, tolerate and recover from constant failure of the components.
2. The system will expect large files but doesn't need to optimize for smaller files.
3. Read operation consists of large stream read and small random reads.
4. Appending is more common than overwriting. The system should support concurrent appending to a single file.
5. High sustained bandwidth is more imporant than low latency.

#### Architecture
 - Single master
   - Assign chunk handle to each chunk
   - Maintain file system metadata (namespace, access conrol, mapping from files to chunks, current location of chunks)
   - Control system-wide activities (chunk lease management, garbage collection of orphaned chunk, chunk migration between chunkservers)
   - Periodically communicates with chunkservers in HeartBeat messages to give instructions and collect state

 - Chunkserver
   - Chunk size is 64MB.

 - Client
   - First, using the ﬁxed chunk size, the client translates the ﬁle name and byte oﬀset speciﬁed by the application into a chunk index within the ﬁle. Then, it sends the master a request containing the ﬁle name and chunk index. The master replies with the corresponding chunk handle and locations of the replicas. The client caches this information using the ﬁle name and chunk index as the key. 

 - Operation log
   - The operation log contains a historical record of critical metadata changes
   - The master checkpoints its state whenever the log grows beyond a certain size.

#### Key guarantees
1. File namespace is atomic and correct.
2. File content is consistent. Identify by defined and undefined data mutation state. Know stale chunks by chunk version number. Implement timeout for client-side chunk caches.
3. Detect component failure by regular handshakes and file corruption by checksumming.


### Hadoop Distributed File System ('HDFS')

### References
[1] Ghemawat, S., Gobioff, H., & Leung, S. T. (2003). The Google file system.
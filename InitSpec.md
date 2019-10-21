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

 - Client

### Hadoop Distributed File System ('HDFS')

### References
[1] Ghemawat, S., Gobioff, H., & Leung, S. T. (2003). The Google file system.
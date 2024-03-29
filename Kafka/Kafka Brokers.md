as we said earlier the data is organized by **topic** and stored in **partitions** on the brokers.
Let's see how a broker handles requests from a producer.

1. The producer sends a request to the broker which lands in the **socket receive buffer**
2. one network thread picks up the request and puts it in the **shared request queue** the thread is **bound** to the producer client.
3. Kafka's **I/O's** thread pool picks up the request from the request queue.
4. the **I/O** thread validates the **CRC** of the data and appends it to a **commit log** which is the commit organized on disk in **segments**. A segment has two parts the **data** and the **index**
5. the producer requests are stashed in a **purgatory** structure for replication so the thread can be freed up to pick up a new request
6. Once the replication of the request is done it is removed from the purgatory and a response is generated and put in the **response queue**
7. The network thread picks up the response from the response queue and sends it to the corresponding **socket** send buffer, the thread is bound to a certain client it's ready to pick up requests only when the response is sent out.
![[Broker.png]]

check [[Ordering Garantees]]

## Load Balancing
Kafka will assign a whole partition to each one of the consumer clients effectively balancing the load between the two it can detect failures and reroute the messages.
a **single partition can only ever be assigned to a single server instance** this is invariant implying that the order is guaranteed

## Compacted Topics
if the data is keyed (has a primary key) we can get rid off the old values if new keys are available this works like the **LSM-trees** so there is a way to optimize the disk space used

in practice we can mix regular Topics with compacted topics and link them via a **Kafka stream job** to get a pattern called the **latest-versioned pattern**
when used as a pub-sub messaging middleware we identify three high-level components :
1. **Producer**: the message sender
2. **Consumer**: the message receiver
3. **Broker**: deployed in a cluster mode handles incoming messages and writes them to broker partitions allowing consumers to read from them.

**Kafka** is a log-based message broker

![[Log-based_Message-Brokers.png]]
Producers send messages by appending them to a topic-partition file and consumers read these files sequentially.
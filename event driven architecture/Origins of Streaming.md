The application takes in streams of input data process them and derive useful data to serve as we can see in this simple example: 

[[streamingAppExample.png]]

## Key notes
- The streaming is clustered and **fault tolerant** if any node crashes another can take its place and continue where it left of (aka storing the intermediate stage) using a **Kafka changelog topic**
- Each streaming node can hold state in the local disk

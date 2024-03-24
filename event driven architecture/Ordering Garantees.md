Logs with the same key go to the same partition which is replicated across the cluster the Data within the same partition is **totally ordered**
see the example [[ordering.png]]

to maintain a **global** ordering for example when migrating a legacy system we could use a **single partition topic**

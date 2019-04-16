# SPARQL2Flink library evaluation
We setup an heterogeneous local cluster to run Flink programs with SPARQL2Flink library. The local cluster where the test are run is configured with one JobManager and ten TaskManager.

Flink’s configurations are done in the flink-conf.yaml file which is part of Job- Manager and TaskManagers. The *jobmanager.heap.mb: 8192m* parameter was configured in JobManager. The *taskmanger.numberOfTaskSlots: 1* and *taskmanager.heap.mb: 8192m* parameters in TaskManagers. Beside, the *io.tmp.dirs: /tmp*, *akka.ask.timeout: 60 min*, *akka.client.timeout: 40 min*, *slot.idle.timeout: 5000000*, *slot.request.timeout: 3000000*, and *heartbeat.timeout: 9900000* parameters were configured in both.

## Dataset
Different datasets were generated by using the BSBM data generator. For each dataset two files were generated. One in Turtle format (with .ttl extension) that was used to generate a query instance from the BSBM template query. Another in N-Triples format (with .nt extension) that was used to probe the query on Apache Flink local cluster.

## Queries from BSBM
Based on the dataset generated, the SPARQL queries templates Q1, Q2, Q3, Q4, Q5, Q7, Q8, Q10 and Q11 were instantiated.

## Flink programs
The above queries were transformed into a Flink program

## Results

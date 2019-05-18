# SPARQL2Flink library test
We evaluated the performance of the SPARQL2Flink library by reusing a subset of the queries defined in the BSBM(http://wifo5-03.informatik.uni-mannheim.de/bizer/berlinsparqlbenchmark/). On the one hand, experiments were carried out to empirically prove the correctness of the results of a SPARQL query transformed into a Flink program. On the other hand, experiments were carried out to show that our approach processes data that can scale as much as the technology on which we execute the query allows, in this case Apache Flink.

## Stand-alone environment setup
We setup Apache Jena(https://jena.apache.org) and Apache Flink(https://flink.apache.org) on a laptop with Intel Core Duo i5 2.8GHz, 8 GB RAM, 1TB solid state disk, and Mac Sierra operating system in order to run empirical correctness tests. We run 9 queries (Q1, Q2, Q3, Q4, Q5, Q7, Q8, Q10, Q11) using ds20mb.ttl dataset.


## Local cluster environment setup
We setup an heterogeneous local cluster to run Flink programs with [SPARQL2Flink library](https://github.com/oscarceballos/sparql2flink). The local cluster where the test are run is configured with one JobManager and ten TaskManager.

Flink’s configurations are done in the flink-conf.yaml file which is part of Job- Manager and TaskManagers. The *jobmanager.heap.mb: 8192m* parameter was configured in JobManager. The *taskmanger.numberOfTaskSlots: 1* and *taskmanager.heap.mb: 8192m* parameters in TaskManagers. Beside, the *io.tmp.dirs: /tmp*, *akka.ask.timeout: 60 min*, *akka.client.timeout: 40 min*, *slot.idle.timeout: 5000000*, *slot.request.timeout: 3000000*, and *heartbeat.timeout: 9900000* parameters were configured in both.

## Dataset
Different datasets were generated by using the [Berlin SPARQL Benchmark (BSBM)](http://wifo5-03.informatik.uni-mannheim.de/bizer/berlinsparqlbenchmark/) data generator. For each dataset two files were generated. One in Turtle format (with .ttl extension) that was used to generate a query instance from the BSBM template query. Another in N-Triples format (with .nt extension) that was used to probe the query on Apache Flink local cluster.

## Queries
Based on the dataset generated, the SPARQL queries templates Q1, Q2, Q3, Q4, Q5, Q7, Q8, Q10 and Q11 were instantiated.

## Flink program
The above queries were transformed into a Flink program

## Results
The main measure that was evaluated is the query execution time.

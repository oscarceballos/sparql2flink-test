# SPARQL2Flink library test
We evaluated the performance of the [SPARQL2Flink library](https://github.com/oscarceballos/sparql2flink) by reusing a subset of the queries defined in the [Berlin SPARQL Benchmark (BSBM)](http://wifo5-03.informatik.uni-mannheim.de/bizer/berlinsparqlbenchmark/). On the one hand, experiments were carried out to empirically prove the correctness of the results of a SPARQL query transformed into a Flink program. On the other hand, experiments were carried out to show that our approach processes data that can scale as much as the technology on which we execute the query allows, in this case Apache Flink.

## Stand-alone environment setup
We setup [Apache Jena](https://jena.apache.org) and [Apache Flink](https://flink.apache.org) on a laptop with Intel Core Duo i5 2.8GHz, 8 GB RAM, 1TB solid state disk, and Mac Sierra operating system in order to run empirical correctness test. We run 9 queries (Q1, Q2, Q3, Q4, Q5, Q7, Q8, Q10, Q11) of BSBM using ds20mb.ttl dataset.


## Local cluster environment setup
We setup an heterogeneous local cluster to run [Flink programs](https://github.com/oscarceballos/sparql2flink-test/tree/master/flink-programs) file with SPARQL2Flink library. Apache Flink local cluster need at least one JobManager and one or more TaskManagers. The JobManager is the master that coordinate and manage the execution of the program. The TaskManagers are the workers that execute parts of the parallel programs. Parallelism of task execution is determined by the Task Slots available on each TaskManager. In our case, there is one Task Slots for each TaskManager.

The scalability test of the SPARQL2Flink library was performed on three different local clusters C1, C2, and C3. We used the 9 queries (Q1, Q2, Q3, Q4, Q5, Q7, Q8, Q10, Q11) and ds300mb, ds600mb, ds1gb, and ds2gb datasets as described in https://github.com/oscarceballos/sparql2flink-test/tree/master/scalability-test/datasets. In particular, one test consisted of executed each query (as a Flink program) with one dataset on a cluster. For instance, query Q1 was executed on ds300mb dataset with 1.166.387 triples and cluster C1 with 3 nodes. Then, the test was repeated in the same way changing the dataset and the nodes number in the cluster (C2 with 6 nodes and C3 with 10 nodes). Hence, a total of 108 tests were conducted.

Flink’s configurations are done in the flink-conf.yaml file which is part of Job- Manager and TaskManagers. The *jobmanager.heap.mb: 8192m* parameter was configured in JobManager. The *taskmanger.numberOfTaskSlots: 1* and *taskmanager.heap.mb: 8192m* parameters in TaskManagers. Beside, the *io.tmp.dirs: /tmp*, *akka.ask.timeout: 60 min*, *akka.client.timeout: 40 min*, *slot.idle.timeout: 5000000*, *slot.request.timeout: 3000000*, and *heartbeat.timeout: 9900000* parameters were configured in both.

## Results
The empirical correctness test results can be see in https://github.com/oscarceballos/sparql2flink-test/tree/master/empirical-correctness-test/results. The main measure that was evaluated in scalability test is the query execution time and can be see in https://github.com/oscarceballos/sparql2flink-test/tree/master/scalability-test/results.

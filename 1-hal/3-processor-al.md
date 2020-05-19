# Processor Abstraction Layer

## NoC Interface

The NoC Interface exposes routines for querying general information about the NoC of the underlying processor. Overall the following interface is exposed:

**Constants**
-   `PROCESSOR_NOC_IONODES_NUM`: number of I/O capable nodes attached to the NoC
-   `PROCESSOR_NOC_CNODES_NUM`: number of computing dedicated nodes attached to the NoC
-   `PROCESSOR_NODENUM_MASTER`: logical ID of master NoC node

**Functions**
-   `processor_node_get_num()`: gets the logic number of the target node
-   `processor_noc_is_ionode()`: asserts whether a NoC node is attached to an I/O Cluster
-   `processor_noc_is_cnode()`: asserts whether a NoC node is attached to a compute cluster
-   `processor_noc_setup()`: initial configures of the NoC resources

## Clusters Interface
The Clusters Interface exposes a uniform numbering scheme across clusters of the processor. Overall the following interface is exposed.

**Constants**
-   `PROCESSOR_CCLUSTERS_NUM`: number of compute clusters
-   `PROCESSOR_IOCLUSTERS_NUM`: number of IO clusters
-   `PROCESSOR_CLUSTERNUM_MASTER`: logical ID of master cluster
**Functions**

-   `cluster_get_num()`: returns the logical ID of the underlying cluster
-   `cluster_is_ccluster()`: asserts if a cluster is a compute cluster
-   `cluster_is_iocluster()`: asserts if a cluster is an IO cluster

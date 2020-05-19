# Cluster Abstraction Layer

## Timer Interface
The Timer Interface exposes routines for configuring the hardware timer.

**Constants**

- `HAL_INT_TIMER`: hardware interrupt number for the timer device

**Functions**

- `timer_init()`: initializes the timer device
- `timer_reset()`: resets the timer of the timer device
- `clock_read()`: reads the clock value

# Cluster Interface
The Cluster Interface exposes routines for querying information of the underlying cluster. Overall, the following interface should be available.

**Constants**

- `CLUSTER_IS_MULTICORE`: evaluates to true if the cluster features multiple cores
- `CLUSTER_COMPUTE`: logic value for a compute cluster type
- `CLUSTER_IO`: logic value for an i/o cluster type
- `CORES_NUM`  number of cores in the underlying cluster
- `COREID_MASTER`: identifier of the master core in the underlying clsuter

**Functions**

- `cluster_get_num_cores()`  returns the number of cores in the underlying cluster
- `cluster_get_type()`: returns the type of the underlying cluster
- `cluster_is_compute()`: asserts if the underlying cluster is a compute cluster
- `cluster_is_io()`: asserts if the underlying cluster is an i/o cluster

## Memory Interface
The Memory Interface exposes a description of the memory layout in a cluster. Overall the following interface is exposed.

**Constants**

Sizes

- `MEMORY_SIZE`: memory size
- `KMEM_SIZE`: kernel memory size
- `UMEM_SIZE`: user memory size
- `KSTACK_SIZE`: kernel stack size
- `KPOOL_SIZE`: kernel page pool size

Physical Memory Layout

- `KBASE_PHYS`: kernel base physical address
- `KPOOL_PHYS`: kernel page pool base physical address
- `UBASE_PHYS`: user base physical address

Virutal Memory Layout

- `USTACK_VIRT`: user stack base virtual address
- `UBASE_VIRT`: user base virtual address
- `KBASE_VIRT`: kernel base virtual address
- `KPOOL_VIRT`: kernel page pool virtual address

**Functions**

- `cluster_mem_setup()`: initializes the memory interface
- `cluster_mem_info()`: prints information about virtual memory layout
- `cluster_mem_check_layout()`: asserts the layout of the memory
- `cluster_mem_check_align()`: asserts the alignment of the memory
- `cluster_mem_map()`: builds the memory layout

## MMIO Interface
The MMIO Interface exposes routines for issuing memory-mapped i/o operations. Overall, the following interface should be available.

**Functions**

- `mmio_get()`: returns an memory mapped I/O address


## Event Interface
The Event Interface enables cores within the same cluster to send, receive and wait for software events. Overall, the following interface is exposed.

**Functions**

- `event_notify()`: sends an event to a local core
- `event_wait()`  : waits for an event from a local core
- `event_drop()`: discard any pending events in the local core

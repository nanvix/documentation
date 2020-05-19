# Core Abstraction Layer

## Cache Interface
The Core Interface exposes routines for manipulating the memory caches. Overall the following interface is exposed.

**Constants**

- `CACHE_LINE_SIZE`: size of a cache line

**Functions**

- `dcache_invalidate()`: invalidates the data cache

## MMU Interface
The Memory Management Unit (MMU) Interface exposes routines for changing paging structures. Overall the following interface is exposed.

**Constants**

Page Shifts & Masks

- `PAGE_SHIFT`: page shift
- `PGTAB_SHIFT`: page table shift
- `PAGE_MASK`: page mask
- `PGTAB_MASK`:: page table mask

Page Sizes

- `PAGE_SIZE`: page size
- `PGTAB_SIZE`: page table size
- `PTE_SIZE`: page table entry size
- `PDE_SIZE`: page directory entry size

Bit-Length of Memory Types

- `PADDR_BIT`: bit-Length of a physical address
- `VADDR_BIT`: bit-Length of a virtual address

Byte-Length of Memory Types

- `PADDR_SIZE`: byte-length of a physical address
- `VADDR_SIZE`: byte-length of a virtual address

**Types**

Memory Types

- `frame_t`: used for referring to page frames
- `vaddr_t`: used for referring to virtual addresses
- `paddr_t`: used for referring to physical addresses

**Structures**

- `pte`: describes a page table entry
- `pde`: describes a page directory entry

**Variables**

- `root_pgdir`  root page directory
- `kernel_pgtab`  kernel page table
- `kpool_pgtab`  kernel page pool page table

**Functions**

Page Directory

- `pde_clear()`: clears a page directory entry
- `pde_frame_set()`: sets the frame of a page directory
- `pde_present_set()`: sets/clears the present bit of a page directory
- `pde_is_preset()`: asserts if the present bit of a page directory is set
- `pde_frame_get()`: gets the frame number of a page directory entry
- `pde_write_set()`: sets/clears the write bit of a page directory
- `pde_is_write()`: asserts if the write bit of a page directory is set
- `pde_user_set()`: sets/clears the user bit of a page directory
- `pde_is_user()`: asserts if the user bit of a page directory is set
- `pde_idx_get()`: gets the page directory index of a page
- `pde_get()`: gets a page directory entry

Page Table

- `pte_clear()`: clears a page table entry
- `pte_frame_set()`: sets the frame of a page table
- `pte_present_set()`: sets/clears the present bit of a page table
- `pte_is_preset()`: asserts if the present bit of a page table is set
- `pte_frame_get()`: gets the frame number of a page table entry
- `pte_write_set()`: sets/clears the write bit of a page table
- `pte_is_write()`: asserts if the write bit of a page table is set
- `pte_user_set()`: sets/clears the user bit of a page table
- `pte_is_user()`: asserts if the user bit of a page table is set
- `pte_idx_get()`: gets the page table index of a page
- `pte_get()`: gets a page table entry
- `page_walk()`: searches for a page

## TLB Interface

The TLB Interface exposes routines for manipulating the translation lookaside buffer (TLB). Overall the following interface is exposed.

**Constants**

- `TLB_INSTRUCTION`: identifies an Instruction TLB
- `TLB_DATA`: identifies a Data TLB

**Macros**

- `VADDR()`  casts something into a virtual address
- `PADDR()`  casts something into a physical address

**Structures**

- `tlbe`: describes an TLB entry

**Functions**

- `tlbe_vaddr_get()`: gets the virtual address encoded in a TLB entry
- `tlbe_paddr_get()`: gets the physical address encoded in a TLB entry
- `tlb_lookup_vaddr()`: looks up a TLB entry by virtual address
- `tlb_look_paddr()`: looks up a TLB entry by physical address
- `tlb_write()`: encodes a virtual address into the TLB
- `tlb_inval()`: invalidates a virtual address in the TLB
- `tlb_flush()`: flushes changes in the TLB

## Core Interface
The Core Interface exposes routines for startup, shutdown and querying information of cores, as well as starting, stopping, suspending and resuming instruction execution on them. Overall the following interface is exposed.

**Constants**

Bit-Length of Core Types

- `BYTE_BIT`: bit-Length of a byte
- `HWORD_BIT`: bit-length of half word
- `WORD_BIT`: bit-length of a word
- `DWORD_BIT`: bit-length of a double word

Byte-Length of Core Types

- `BYTE_SIZE`: byte-length of a byte
- `HWORD_SIZE`: byte-length of a half word
- `WORD_SIZE`: byte-length of a word
- `DWORD_SIZE`: byte-length of a double word

**Types**

Core Types

- `byte_t`: holds a byte
- `hword_t`  holds a half word
- `word_t`: holds a word
- `dword_t`: holds a double word

**Functions**

- `core_startup()`: starts up the underlying core
- `core_shutdown()`: shutdowns the underlying core
- `core_get_id()`: returns the identifier of the underlying core
- `core_start()`: starts instruction execution in a core
- `core_reset()`: stops instruction execution in the underlying core
- `core_sleep()`: suspends instruction execution in the underlying core`
- `core_wakeup()`: resumes instruction execution of a core

## Exception Interface
The Exception Interface exposes types and routines for manipulating exceptions. Overall the following interface is exposed.

**Constants**

- `EXCEPTION_SIZE`: size of exception structure in bytes

**Structures**

- `exception`: describes the information regarding an exception

**Types**

- `exception_handler_t`: signature of an exception handler

**Functions**

- `exception_get_num()`: gets the number of an exception
- `exception_get_addr()`: gets the address of an exception
- `exception_set_handler()`: sets a handler for an exception

## Execution Context Interface
The Execution Context Interface exposes types and routines for manipulating the execution context of a core. Overall the following interface is exposed.

**Constants**

- `CONTEXT_SIZE`: size of the context structure

**Structures**

- `context`: describes the execution context of a core

**Functions**

- `context_get_sp()`: retrieves the value of the stack pointer in an execution context
- `context_get_pc()`: retrieves the value of the program counter in an execution context
- `context_set_sp()`: changes the value of the stack pointer in an execution context
- `context_set_pc()`: changes the value of the program counter in an execution context

## Hardware Interrupt Interface

The Hardware Interrupt Interface exposes routines for hardware interrupts. Overall the following interface is exposed.

**Constants**

- `HAL_INT_NR`: number of hardware interrupts

**Types**

- `interrupt_handler_t`: signature of a hardware interrupt handler

**Functions**

- `interrupts_disable()`: enables all hardware interrupts
- `interrupts_enable()`: disables all hardware interrupts
- `interrupt_set_handler()`: sets a handler for an interrupt
- `hal_intlvl_set()`: sets the interrupt level of the underlying core
- `interrupt_ack()`: acknowledges an interrupt
- `interrupt_mask()`: masks an interrupt
- `interrupt_unmask()`: unmasks an interrupt
- `interrupt_register()`: registers an interrupt handler
- `interrupt_unregister()`: unregisters an interrupt handler
- `interrupt_setup()`: setups hardware interrupts

## Performance Monitoring Interface

The Performance Monitoring Interface exposes routines for monitoring the performance of the underlying core. Overall, the following interface is exposed.

**Constants**

- `PERF_MONITORS_NUM`: number of performance monitors
- `PERF_EVENTS_NUM`: number of performance events supported
- `PERF_CYCLES`: clock cycles
- `PERF_ICACHE_HITS`: instruction cache hits
- `PERF_ICACHE_MISSES`: instruction cache misses
- `PERF_ICACHE_STALLS`: instruction cache stalls
- `PERF_DCACHE_HITS`: data cache hits
- `PERF_DCACHE_MISSES`: data cache misses
- `PERF_DCACHE_STALLS`: data cache stalls
- `PERF_BUNDLES`: bundles executed
- `PERF_BRANCH_TAKEN`: branches taken
- `PERF_BRANCH_STALLS`: branches stalled
- `PERF_REG_STALLS`: register dependence stalls
- `PERF_ITLB_STALLS`: instruction TLB stalls
- `PERF_DTLB_STALLS`: data TLB stalls
- `PERF_STREAM_STALLS`: stream buffer stalls

**Functions**

- `perf_setup()`: initializes the Performance Monitoring Interface
- `perf_query():`  queries for the support of a performance event
- `perf_read()`: reads the value of a performance monitor
- `perf_start()`: starts a performance monitor
- `perf_stop()`: stops a performance monitor

## PMIO Interface

The PMIO Interface exposes routines for dealing with port-mapped input/output devices. Overall the following interface is exposed.

**Functions**

Output

- `output8()`: writes 8 bits to an i/o port
- `output8s()`: writes an 8-bit string to an i/o port

Misc

- `iowait()`: waits for an operation in an i/o port to complete

## Spinlock Interface

The Spinlock Interface exposes a spinlock abstraction. Overall the following interface is exposed:

**Constants**

- `SPINLOCK_UNLOCKED`: value for a n unlocked spinlcok

**Types**

- `spinlock_t`: spinlock data type

**Functions**

- `spinlock_lock()`: locks a spinlock
- `spinlock_unlock()`: unlocks a spinlock

## Trap Interface
The Trap Interface exposes wrappers for issuing kernel calls. Overall, the following interface should be available.

**Functions**

- `syscall0()`: issues a system call with no arguments
- `syscall1()`: issues a system call with one argument
- `syscall2()`: issues a system call with two arguments
- `syscall3()`: issues a system call with three arguments
- `syscall4()`: issues a system call with four arguments
- `syscall5()`: issues a system call with five arguments

## Upcall Interface
The Upcall Interface exposes routines for making upcalls. Overall the following interface is exposed.

**Constants**

- `NR_upcall_ret`  number of the system call reserved for calling  `upcall_ret()`

**Macros**

- `UPCALL_STACK_FRAME_SIZE()`: computes the stack frame of an upcall

**Functions**

- `upcall_forge()`: forges an upcall stack frame
- `upcall_ret()`: returns from an upcall

# HAL

1. [Core AL](1-core-al.md)
2. [Cluster AL](2-cluster-al.md)
3. [Processor AL](3-processor-al.md)

In order for an operating system to be ported from one particular
architecture to another, low-level routines and structures should be
re-written and re-design. While the efforts for carrying out such task
are inherently related to the new target to support, it is also greatly
impacted by the tightness of low-level routines and structures with the
kernel itself. The more modular is the design of the kernel, the easier
is to getting it running on new hardware.

A Hardware Abstraction Layer (HAL) is a lowest-level software layer of
an operating system kernel which is intended to address this portability
problem. The HAL abstracts away architectural differences between
several platfoms and exposes a standard interface for dealing with these
hardware. This way, higher-level portions of the kernel may be designed
and implemented in a platform-independent fashion, and thus kernel
portability may be achieved.

While on one hand a HAL promotes kernel portability, on the other hand,
it is hard to port a given HAL from one kernel to another. That is,
integrate it with several several kernels. Indeed, the rationale for
that is two-fold: (i) low-level interfaces of kernels have no standard
and may drastically vary, thus plug-and-play does not work at all; and
(ii) the source tree of the HAL is usual tighly coupled with the source
tree of a kernel, thereby requiring the great effot of actually
extracting it from there and make it stand-alone. The former point is
hard to address, since it requires inhenretly each kernel to be
approached separately. However, the second one may be tackled if from
its conception a HAL is kept separated from the overlying kernel.

Looking towards this second contribution, in this project we maintain
the HAL source tree of the  [Nanvix
Microkernel](https://github.com/nanvix/microkernel). We designed the
interface of this HAL as flexible and generic as possible, so that it
could be easily integrated into other kernels as well as extended to new
hardware. Currently, this HAL supports the multiple platforms, including
the ones based on the  Kalray-MPPA 256 and OpTiMSoC lightweight manycore
processors.

## HAL Structure

The HAL of Nanvix is structured in four layers, which of each exports
interfaces for dealing with a specific components of the underlying
platform:

-   Platform Abstraction Layer: exposes interfaces for managing device connectivity.
-   Processor Abstraction Layer: exposes interfaces for managing inter-cluster communication.
-   Cluster Abstraction Layer: exposes interfaces for managing local memory of clusters and inter-core communication.
-   Core Abstraction Layer: exposes interfaces for managing first-level memory structures and a single core.

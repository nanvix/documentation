Hardware Abstraction Layer (HAL) of Nanvix
==========================================
[![Build Status](https://travis-ci.com/nanvix/hal.svg?branch=unstable)](https://travis-ci.com/nanvix/hal)
[![Join us on Slack!](https://img.shields.io/badge/chat-on%20Slack-e01563.svg)](https://join.slack.com/t/nanvix/shared_invite/enQtMzY2Nzg5OTQ4NTAyLTAxMmYwOGQ0ZmU2NDg2NTJiMWU1OWVkMWJhMWY4NzMzY2E1NTIyMjNiOTVlZDFmOTcyMmM2NDljMTAzOGI1NGY)

What Is This Project About?
---------------------------

A Hardware Abstraction Layer (HAL) is the lowest-level software
abstraction in an operating system. Its role is to provide a uniform
view of the underlying architecture so as kernel portability is
achieved. This repository hosts the HAL source tree of the
[Nanvix Microkernel](https://github.com/nanvix/microkernel).  This HAL
is designed as flexible and generic as possible, so that it may be
easily integrated into other kernels as well as extended to new
platforms.  Currently, this HAL supports the multiple platforms,
	including the ones based on the
[Kalray-MPPA 256](https://github.com/nanvix/hal/wiki/Supported-Platforms#mppa-256)
and
[OpTiMSoC](https://github.com/nanvix/hal/wiki/Supported-Platforms#optimsoc)
lightweight manycore processors.

Building & Running
------------------

**1. Clone This Repository**

```
export WORKDIR=$HOME                                    # Change this at your will
cd $WORKDIR                                             # Go to working directory
git clone --recursive https://github.com/nanvix/hal.git # Clone the source tree
```

**2. Get the Development Toolchain**

Install build dependencies.

```
cd $WORKDIR/hal                                # Enter the source tree
sudo bash utils/nanvix-setup-prerequisites.sh  # Get essential tools for building
```

Export the name of the desired target:

```
export TARGET=qemu-x86      # QEMU x86
export TARGET=qemu-openrisc # QEMU OpenRISC
export TARGET=optimsoc      # OpTiMSoC
export TARGET=qemu-riscv32  # QEMU RISC-V 32-Bit (experimental)
export TARGET=unix64        # Virtualized Platform
```

if you choose `unix64` as a target, run the following command and go to step 3:

`sudo bash utils/nanvix-setup-unix.sh #configure virtual resources.`

Otherwise, Build the toolchain itself:

```
bash utils/setup-toolchain.sh
```

Build simulators:

```
sudo bash utils/setup-qemu.sh
```

Add simulators to your path:

```
export PATH=$PATH:$WORKDIR/hal/tools/dev/toolchain/qemu/bin
```

**3. Build the HAL**

```
make contrib   # Build Submodules
make distclean # Ensure a clean working directory.
make all       # Build the HAL.
```

**4. Run Regression Tests (optional)**

```
make run            # 
make run-ccluster   # Compute Cluster
make run-iocluster  # IO Cluster
```

License & Maintainers
---------------------

Nanvix is a free operating system that is distributed under the [MIT
License](https://raw.githubusercontent.com/nanvix/hal/master/LICENSE). It was
created by [Pedro Henrique Penna](mailto:pedrohenriquepenna@gmail.com),
but it is now maintained by many others. If you are interested in
contacting any of the contributors, take a look in the complete
[list of contributors of
Nanvix](https://raw.githubusercontent.com/nanvix/people/master/CREDITS).

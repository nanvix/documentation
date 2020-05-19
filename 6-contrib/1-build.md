# Building and Running
**1. Clone This Repository**

```
export WORKDIR=$HOME                                    # Change this at your will
cd $WORKDIR                                             # Go to working directory
git clone --recursive https://github.com/nanvix/hal.git # Clone the source tree

```

**2. Get the Development Toolchain**

Install build dependencies.

```
cd $WORKDIR/hal                             # Enter the source tree
sudo bash tools/dev/setup-prerequisites.sh  # Get essential tools for building

```

Export the name of the target:

```
export TARGET=qemu-x86      # QEMU x86
export TARGET=qemu-openrisc # QEMU OpenRISC
export TARGET=optimsoc      # OpTiMSoC
export TARGET=qemu-riscv32  # QEMU RISC-V 32-Bit (experimental)
export TARGET=unix64        # Virtualized Platform 

```

If you chose  `unix64`  as a target, run the following command and go to step 3:

```
sudo bash utils/nanvix-setup-unix.sh #configure virtual resources.

```

Otherwise, build the toolchain itself:

```
bash tools/dev/setup-toolchain.sh

```

Build simulators:

```
sudo bash tools/dev/setup-qemu.sh

```

**3. Build the HAL**

```
make contrib   # build dependencies
make distclean # ensure a clean working directory
make all       # build the HAL

```

**4. Run Regression Tests (optional)**

```
make test
```

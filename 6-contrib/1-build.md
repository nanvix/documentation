Building & Running
------------------

**1. Clone the Wanted Repository**

This process works for every repository. This example will be making use of the hal
one, but feel free to substitute "hal" with the name of the repository you want.

```
export WORKDIR=$HOME                                    # Change this at your will
cd $WORKDIR                                             # Go to working directory
git clone --recursive https://github.com/nanvix/hal.git # Clone the source tree
```

**2. Get the Development Toolchain**

Install build dependencies.

```
cd $WORKDIR'/hal/utils'                   # Enter the source tree
sudo bash nanvix-setup-prerequisites.sh   # Get essential tools for building
```

Export the name of the desired target:
```
export TARGET=qemu-x86      # QEMU x86
export TARGET=qemu-openrisc # QEMU OpenRISC
export TARGET=optimsoc      # OpTiMSoC
export TARGET=qemu-riscv32  # QEMU RISC-V 32-Bit (experimental)
export TARGET=unix64        # Virtualized Platform
```

If you chose `unix64` as a target, run the following command and go to step 3:

`sudo bash nanvix-setup-unix.sh #configure virtual resources.`

Otherwise, Build the toolchain itself:

```
bash nanvix-setup-toolchain.sh
```

Build simulators:

```
bash nanvix-setup-qemu.sh
```

Add simulators to your path:

```
export PATH=$PATH':'$WORKDIR'/hal/utils/toolchain/qemu/bin'
```

**3. Build**

```
cd $WORKDIR'/hal'
make distclean           # Ensure a clean working directory.
make contrib-uninstall   # Ensure clean submodules.
make contrib             # Build submodules.
make all                 # Build.
```

**4. Run Regression Tests (optional)**

```
make run
```

`You may need root privileges when running (normally for QEMU).`

```
sudo -E PATH=$PATH make run # Run as root preserving environment variables.
                            # PATH won't be preserved, so set it again.
```

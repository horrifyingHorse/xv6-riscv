# `xv6` for RISC-V
*RISC V*: Unlike the x86_64 arch, RISC V is an ISA for a RISC machine(x86 is a CISC). Also RISC V is Open Source!

### Using `qemu`
1. To cross compile xv6 for RISC V, we need the GNU RISCV Compiler Toolchain, takes a lot of time + space (nearly 11 gb). There are two flavors of this toolchain.
- *Newlib:* This allows the compiled prog to be lightweight enough to be cross compiled and be exported to an embedded system. Although if the program uses features like threading etc, idk what happens.
* *Linux:* basic x86 Linux to RISC V Linux compilation, uses the same libs (std lib etc) (ig?)

> $INSTALLATION_PATH=/opt/riscv
> 
> Add dir to path: `export PATH="$PATH:/opt/riscv"`

```bash
git clone --depth=1 https://github.com/riscv-collab/riscv-gnu-toolchain
cd riscv-gnu-toolchain
./configure --prefix=$INSTALLATION_PATH
make linux
```

2. To emulate RISC V, we need qemu:

```bash
sudo pacman -Syu
sudo pacman -S qemu # qemu-full contains the RISCV emulator
```

3. `xv6` compilation

```bash
git clone --depth=1 https://github.com/mit-pdos/xv6-riscv
cd xv6-riscv
TOOLPREFIX=$INSTALLATION_PATH/bin/riscv64-unknown-linux-gnu- make qemu
```
This now boots you into the xv6

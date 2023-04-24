## Compile with Fedora Workstation 38

```
toolbox create
toolbox enter
sudo dnf install arm-none-eabi-gcc arm-none-eabi-newlib make gcc dfu-util
git clone --recursive https://github.com/blackmagic-debug/blackmagic.git
cd blackmagic
git apply ../blackmagic-revp.patch
make PROBE_HOST=revp
```

## Bootstrap using BMP and GDB

```
target extended-remote /dev/ttyBmpGdb
monitor swdp_scan
attach 1
monitor option 0x1FFFF804 0x04
exec-file src/blackmagic_dfu.elf
load
compare-sections
kill
```

## Install Firmware Using DFU

```
dfu-util -d 1d50:6018,:6017 -s 0x08002000:leave -D src/blackmagic.bin
```

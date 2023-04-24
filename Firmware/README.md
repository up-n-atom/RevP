## Compile and Install with Fedora Workstation 38

```
toolbox create
toolbox enter
sudo dnf install arm-none-eabi-gcc arm-none-eabi-newlib make gcc dfu-util
git clone https://github.com/blackmagic-debug/blackmagic.git
cd blackmagic
git apply ../blackmagic-revp.patch
make PROBE_HOST=revp
dfu-util -d 1d50:6018,:6017 -s 0x08002000:leave -D src/blackmagic.bin
```

# How to build CircuitPython on Mac

## Pre-build

My Mac has git, make, python2 and python3.

```
git clone https://github.com/adafruit/circuitpython.git
cd circuitpython
git submodule sync
git submodule update --init --recursive

$brew install gettext
[brew found gettext 0.19.8.1 is already installed]

$brew link gettext --force

make V=2 -C mpy-cross

```

## Some message after the build for SAMD21

```
cd ports/atmel-samd
make V=2 BOARD=circuitplayground_express TRANSLATION=es

...
arm-none-eabi-size build-circuitplayground_express/firmware.elf | python3 ../../tools/build_memory_info.py boards/samd21x18-bootloader-external-flash-crystalless.ld

4940 bytes free in flash out of 253440 bytes ( 247.5 kb ).
25732 bytes free in ram for stack out of 32768 bytes ( 32.0 kb ).

Create build-circuitplayground_express/firmware.bin
arm-none-eabi-objcopy -O binary -j .vectors -j .text -j .data build-circuitplayground_express/firmware.elf build-circuitplayground_express/firmware.bin
Create build-circuitplayground_express/firmware.uf2
python3 ../../tools/uf2/utils/uf2conv.py -b 0x2000 -c -o build-circuitplayground_express/firmware.uf2 build-circuitplayground_express/firmware.bin

Converting to uf2, output size: 497152, start address: 0x2000

Wrote 497152 bytes to build-circuitplayground_express/firmware.uf2.
```

## Some messages after the build for nRF

```
cd port/nrf
make V2 BOARD=pca10056

...

rm-none-eabi-size build-pca10056/firmware.elf | python3 ../../tools/build_memory_info.py boards/adafruit_nrf52840_s140_v6.ld

784304 bytes free in flash out of 1048576 bytes ( 1024.0 kb ).
230756 bytes free in ram for stack out of 245760 bytes ( 240.0 kb ).

Create build-pca10056/firmware.bin
arm-none-eabi-objcopy -O binary build-pca10056/firmware.elf build-pca10056/firmware.bin
Create build-pca10056/firmware.hex
arm-none-eabi-objcopy -O ihex build-pca10056/firmware.elf build-pca10056/firmware.hex
Create build-pca10056/firmware.uf2
python3 ../../tools/uf2/utils/uf2conv.py -f 0xADA52840 -c -o "build-pca10056/firmware.uf2" build-pca10056/firmware.hex
Converting to uf2, output size: 528896, start address: 0x26000
Wrote 528896 bytes to build-pca10056/firmware.uf2.

```

## Reference

* [Adafruit](https://learn.adafruit.com/building-circuitpython/build-circuitpython)


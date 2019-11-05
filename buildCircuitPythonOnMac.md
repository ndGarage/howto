# How to build CircuitPython on Mac

```
git clone https://github.com/adafruit/circuitpython.git
cd circuitpython
git submodule sync
git submodule update --init --recursive

$brew install gettext
[brew found gettext 0.19.8.1 is already installed]

$brew link gettext --force

make V=2 -C mpy-cross

cd ports/atmel-samd
make V=2 BOARD=circuitplayground_express TRANSLATION=es
```

Some message after the build
```
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


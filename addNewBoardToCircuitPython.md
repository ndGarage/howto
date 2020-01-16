# How to add a new board to CircuitPython

## steps

* create a new branch

```
git checkout -b ndbit6
```

* create the necessary files for your board

```
cd circuitpython
cd ports/atmel-samd/boards
mkdir ndbits
cd ndbit6
cp ../sparkfun_samd21_dev/* .
```

* start to edit the following files

```
/ports/atmel-samd/boards/ndbit6/mpconfigboard.h
/ports/atmel-samd/boards/ndbit6/mpconfigboard.mk
/ports/atmel-samd/boards/ndbit6/pins.c
/.github/workflows/build.yml
```

* build your board

```
cd circuitpython/ports/atmel-samd
make V=2 BOARD=ndbit6
...
Converting to uf2, output size: 367616, start address: 0x2000
Wrote 367616 bytes to build-ndbit6/firmware.uf2.
```

## reference

* [AdaFruit-Add new board](https://learn.adafruit.com/how-to-add-a-new-board-to-circuitpython/overview)

* [Adafruit-Git](https://learn.adafruit.com/contribute-to-circuitpython-with-git-and-github/grab-your-fork)


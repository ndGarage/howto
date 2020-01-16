# Build with Sparkfun Artemis and Ambiq Apollo 3 Blue

## Setup (Bash, Make, and Python3)

The only things missing are as follows.
Python3 has the version 3.7.2.

```
pip3 install pycryptodome
pip3 install pyserial
```

pycryptodome-3.9.4
pyserial-3.4

## Setup toolchain (GCC and SDK)

For arm-none-eabi-gcc, the version is 2018-q4-major.

For Ambiq SDK, its version is 2.3.2. Use $AMB_ROOT to specify the root directory where the AmbiqSuite-R2.3.2 is unzipped.

### AmbiqSuite

```
AmbiqSuite-R2.3.2 $tree -L 2
.
├── AM-BSD-EULA.txt
├── Apollo3_Examples.txt
├── CMSIS
│   ├── ARM
│   ├── AmbiqMicro
│   └── version_cmsis_info.txt
├── Makefile
├── VERSION.txt
├── ambiq_ble
│   ├── apps
│   ├── em9304
│   ├── menu
│   ├── profile_appl
│   ├── profiles
│   └── services
├── boards
│   ├── Makefile
│   ├── apollo1_evb
│   ├── apollo2_blue_evb
│   ├── apollo2_evb
│   └── apollo3_evb
├── bootloader
│   ├── am_bootloader.c
│   ├── am_bootloader.h
│   ├── am_ios_boot_handlers.c
│   ├── am_multi_boot.c
│   ├── am_multi_boot.h
│   ├── am_multi_boot_private.h
│   ├── am_multi_boot_secure.h
│   └── am_uart_boot_handlers.c
├── devices
│   ├── am_devices.h
│   ├── am_devices_button.c
│   ├── am_devices_button.h
│   ├── am_devices_da14581.c
│   ├── am_devices_da14581.h
│   ├── am_devices_em9304.c
│   ├── am_devices_em9304.h
│   ├── am_devices_fireball.c
│   ├── am_devices_fireball.h
│   ├── am_devices_led.c
│   ├── am_devices_led.h
│   ├── am_devices_mb85rc256v.c
│   ├── am_devices_mb85rc256v.h
│   ├── am_devices_mb85rs1mt.c
│   ├── am_devices_mb85rs1mt.h
│   ├── am_devices_mspi_flash.c
│   ├── am_devices_mspi_flash.h
│   ├── am_devices_mspi_psram.c
│   ├── am_devices_mspi_psram.h
│   ├── am_devices_spiflash.c
│   └── am_devices_spiflash.h
├── docs
│   ├── apollo3_gpio
│   ├── apollo3_porting
│   ├── app_notes
│   ├── exactle
│   ├── getting_started
│   ├── licenses
│   ├── registers
│   ├── releasenotes
│   └── secure_bootloader
├── makedefs
│   ├── am_bsp.mk
│   ├── am_bsp_legacy.mk
│   ├── am_hal.mk
│   ├── example.mk
│   └── subdirs.mk
├── mcu
│   ├── Makefile
│   ├── apollo
│   ├── apollo2
│   └── apollo3
├── pack
│   └── SVD
├── third_party
│   ├── FreeRTOSv10.1.1
│   ├── Makefile
│   ├── exactle
│   ├── prime_mpi
│   └── uecc
├── tools
│   ├── Makefile
│   ├── amota
│   ├── apollo3_amota
│   ├── apollo3_scripts
│   ├── bootloader_scripts
│   ├── bsp_generator
│   └── emp2include
└── utils
    ├── am_util.h
    ├── am_util_ble.c
    ├── am_util_ble.h
    ├── am_util_debug.c
    ├── am_util_debug.h
    ├── am_util_delay.c
    ├── am_util_delay.h
    ├── am_util_faultisr.c
    ├── am_util_id.c
    ├── am_util_id.h
    ├── am_util_regdump.c
    ├── am_util_regdump.h
    ├── am_util_stdio.c
    ├── am_util_stdio.h
    ├── am_util_string.c
    ├── am_util_string.h
    ├── am_util_time.c
    └── am_util_time.h

47 directories, 61 files
```

### Clone [Sparkfun_Edge_BSP](https://github.com/sparkfun/SparkFun_Edge_BSP)

```
cd $AMB_ROOT/boards
git clone https://github.com/sparkfun/SparkFun_Edge_BSP
```

### Several corrections:

```
cd $AMB_ROOT/tools/apollo3_scripts/
mv keys_info0.py keys_info.py
```


```
cd $AMB_ROOT/boards/SparkFun_Edge_BSP/bsp/tools/
chmod 755 uart_wired_update_sparkfun.py
```

## Build the first example

Make sure that the ARM-GCC is in the $PATH
```
export ARMGCC_DIR="$HOME/opt/armDev/gcc-arm-none-eabi-8-2018-q4-major"
```

Edit gcc/Makefile to replace COM4 with the actual port while the Edge board is connected to. (On Windows COMx, on Mac/Linux /dev/cu.usbserialxxx.)

```
cd $AMB_ROOT/boards/SparkFun_Edge_BSP/examples/example1_edge_test/gcc/
make
```

## Flash code to board

Hold down Button14, press and release Reset

```
make bootload
```



## Ref

* [Sparkfun Tutorial](https://learn.sparkfun.com/tutorials/using-sparkfun-edge-board-with-ambiq-apollo3-sdk/all)


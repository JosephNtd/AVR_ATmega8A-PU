# AVR Programming with VSCode in Linux

## Install & Setup Environment

### Install AVR-GCC Compiler
```sh
    sudo apt-get install gcc build-essential
    sudo apt-get install gcc-avr binutils-avr avr-libc gdb-avr
```

### Install AVRDUDE
```sh
sudo apt-get install libusb-dev
sudo apt-get install avrdude
```
## Build the program
```sh
avr-gcc -mmcu=atmega328p -Wall -Os -o build/blink.elf src/blink.c
avr-objcopy -j .text -j .data -O ihex build/blink.elf build/blink.hex
```
or just go in to the Makefile
- change the Program name
- change the Src Name
 ```sh
make
```
## Upload the Program to Atmega328P
To ensure that the USBasp programmer is detected and connected to Atmega328, verify the device signature:

```sh
avrdude -c usbasp-clone -p m328p
```

Upload the program:

```sh
avrdude -c usbasp-clone -p m328p -U flash:w:build/blink.hex
```

or just use the `Makefile` and execute this command:

```sh
make upload
```

# If VSCode did not understand #include or DDRC | PORT 
 Go to Extension -> Setting -> 
 - Include Path -> usr/lib/avr/include
 - Define -> "__AVR_ATmega8A__"
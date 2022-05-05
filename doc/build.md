# Requirements
1. arduino uno (based on atmega328p)
2. 1 capacitor 1uF or grater (tested with 100uF)
3. resitor of 4k7 ohm


# BUILD on OSX
install avr tools: 

```
brew tap osx-cross/avr
brew install avr-gcc
brew install avrdude
```

check parameters in file make.sh

compile jtag2udpi

```
chmod 755 make.sh
./make.sh
```

# PROGRAM arduino with jtag2udpi firmware

Connect arudino and get serial port number

```
ls /dev/tty.usb*
```

for example serial can be /dev/tty.usbmodem141401

write jtag2udpi firmware in arduino

```
avrdude -C avrdude.conf.arduino  -c arduino -P /dev/tty.usbmodem141401 -p m328p -U flash:w:build/JTAG2UPDI.hex:i
```

# Connect Target to Arduino uno
1. PIN6 of arduino uno should be connected to UDPI interface with a 4k7 resistor
2. Connect Capacitor between Reset and Gnd arduino uno
3. Connect 3v3 or 5v to target board according to Target Specification
4. Connect GND to target board

# Program AtTiny402

to program attiny402 using arduino uno flashed with new firmware run

```
avrdude -C avrdude.conf -c jtag2updi -P /dev/tty.usbmodem141401 -p t402 -v -U flash:w:/Users/simone/Downloads/DesignVOC/designVOC.hex:i
```
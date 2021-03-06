stmbl
=====

###AC Servo Driver for STM32F4
##### Driving a Bosch Turboscara
https://www.youtube.com/watch?v=Ue98HE76paI
##### Drivetest
https://www.youtube.com/watch?v=sMeV4SCu4TA

####Things that work
* Synchronous AC servos with resolver or incremental encoder
* DC servos with encoder
* IRAMXv2 Hardware testet up to 320V

####TODO
* autophasing for Synchronous AC servos with encoder
* AC Async
* saving parameters to flash

####Directories
* hw/eagle/ Eagle board files and schematics
* hw/spice/ Spice simulation for resolver interface
* src/ STM32 code
* term/ Terminal with scope and local history. Supports UHU servo and stmbl.


####Building the firmware
##### Requirements
* gcc-arm-none-eabi-gcc https://launchpad.net/gcc-arm-embedded/+download
* stlink https://github.com/texane/stlink

##### Flashing
Add gcc and stlink to your $PATH

    make
    make burn

####Building Servoterm
##### Requirements
* cmake >= 2.8
* gcc >= 4.8 or clang
* wxwidgets >= 3.0
* libserialport http://sigrok.org/wiki/Libserialport

##### Compiling

    cd term/
    mkdir build/
    cmake ../
    make

####Using Servoterm
##### Testing HAL
HAL can be tested without any hardware connected to the STM32F4discovery.
* Flash STM32F4discovery(STlink and USB OTG must be connected)
* Launch Servoterm, Click refresh, and connecto to STM32 Virtual ComPort

entering ? prints a list of hal pins.
The current default config is for a 4 pole AC permanent magnet motor with resolver feedback, using an encoder for command. 

> net0.fb <= res0.pos = 0.000000

net0.fb is driven by res0.pos, and its current value is 0. Pins can be connected to other pins, or fixed values.

This example connects the sine wave generatror to wave view 0.
Offset and gain can be controlled with the sliders below Channel 1(black).
```
term0.wave0 = sim0.sin
sim0.amp = 10
sim0.freq = 5
```
To disconnect a pin, connect it to itself
```
term0.wave0 = term0.wave0
```

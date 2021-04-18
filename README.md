UNBRICK ARDUINO NANO 33 IOT WITH A ARDUINO MKR ZERO


The only way I could find to recover the board was by burning the bootloader.

You'll need:

An extra Arduino board that runs at 3.3 V.
An SD slot. This could be built into your Arduino board (e.g., MKR Zero), a shield (e.g., MKR SD Proto Shield), or one of the common SD modules.
An SD card that fits your SD slot.
A way to connect the SD card to your computer.
A way to make the connections to the SWD pins on your target Arduino board. I like to use a 0.1" pitch 2x3 POGO adapter. You could also solder wires to the test points if you prefer.
It is possible to use an Arduino board that runs at 5 V as the programmer, but you'll need to use level shifting circuitry on the programming lines to avoid exposing the target board to 5 V logic levels, which would damage it.

Instructions:

Connect an SD card to your computer.

Download https://github.com/arduino/ArduinoCore-samd/raw/master/bootloaders/nano_33_iot/samd21_sam_ba_arduino_nano_33_iot.bin

Rename the downloaded file to fw.bin

Move fw.bin to the SD card.

Eject the SD card from your computer.

Plug the USB cable of the Arduino board you will be using as a programmer into your computer.

(In the Arduino IDE) Sketch > Include Library > Manage Libraries

Wait for the download to finish.

In the "Filter your search..." field, type "Adafruit DAP library".

Press "Enter".

Click on "Adafruit DAP library by Adafruit".

Click the "Install" button.

Wait for the installation to finish.

Click the "Close" button.

File > Examples > Adafruit DAP library > flash_from_SD

Change these lines:

SWDIO 10
SWCLK 9
SWRST 11

#define SD_CS 4
according to the Arduino pin connected to the SD CS pin. If your board has a built-in SD slot (e.g., MKR Zero), then you can change this line:

if (!SD.begin(SD_CS)) {
to:

if (!SD.begin()) {
Select the correct board from the Tools > Board menu.

Select the correct port from the Tools > Port menu.

Sketch > Upload

Wait for the upload to finish successfully.

Unplug the programmer Arduino board from your computer.

Plug the SD card into the SD slot connected to your Arduino board.

Connect the programmer Arduino board to the target Arduino board as follows:

| Programmer | | Target | | - | - | | ----------- | |------- | | VCC | | +3V3 | | ----------- | |------- | | 10 | | SWDIO | | ----------- | |------- | | 9 | | SWCLK | | ----------- | |------- | | GND | | GND | | ----------- | |------- | | 11 | | RESETN | | ----------- | |------- |

Nano 33 IoT SWD pads: |500x377

Plug the USB cable of the programmer Arduino board into your computer.

Tools > Serial Monitor. You should now see the target board detected, and the bootloader file flashed to it successfully.

Unplug the programmer Arduino board from your computer.

Disconnect the programmer Arduino board from the target Arduino board.

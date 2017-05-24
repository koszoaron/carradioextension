# carradioextension
A microcontroller project to extend the features of my car radio.

For now this file functions as a requirements/design document.
The basis of the project is an STM32 microcontroller, preferably a "BluePill" STM32F103 because it's cheap, has 5V tolerant pins, has USB host support and enough peripherals (2 SPI, at least 2 UART, many timers, I2C).

The features that the project will have (in ordered by implementation step):
  0. Debug UART interface for command line input/output.
  1. CD changer emulator for VW radios. Based on vwcdcemu, uses one or two timers, optionally an SPI module. Emulates a CD changer to the radio, transmits the CD number (1-6), track number (1-99?) and playback time to the radio and receives the pressed button codes, such as CD number, seek, previous/next track, play/pause from the radio. Also used as the initial display, until LCD support is ready.
  2. Bluetooth A2DP/AVRCP receiver using an external IC (the BLK-MD-SPK-B module can be used). Should receive the audio stream using the A2DP protocol and output it as analog audio into the CDC input (galvanic isolation is probably needed). Also the button presses from the CDC module shall be forwarded to the BT module to transmit over AVRCP. When LCD support is available, display the song information on the LCD, until then just show the song progress (if available) on the radio display. When LCD/buttons are available, make a menu system that helps pairing/connecting phones. Support microphones so it can be used as a handsfree set. If the radio speakers make to much echo, install a separate speaker and use the mute pin of the radio to toggle between the speakers.
  3. MP3 playback. Using the USB host and an external MP3 decoder (such as VS1003) add MP3 support. FAT32 USB disk shall be read, traversed for directories and files. In the beginning supporting 6 directories with 99 songs each is enough, since it matches the CD changer capabilities. An empty directory (maybe with a special text file) could indicate a 'Bluetooth' disc. ID3 tags shall be read and displayed on the LCD screen.
  4. LCD display using a small OLED module. Show song information, playback progress, pairing options for Bluetooth. Add 3-4 buttons or an encoder with a button to make menu navigation easier.
  5. Interface to the car K-line diagnostic interface. Requires an adapter circuit and should have isolation. Could display some basic info on the LCD. If Bluetooth serial port works then it should make a bridge between the phone and the car diagnostic interface. Maybe an ELM327 IC is required.

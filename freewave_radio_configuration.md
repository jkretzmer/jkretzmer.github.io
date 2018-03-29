# FreeWave Radio Basic Configuration
## Overview

Swift Navigation distributes FreeWave 900 MHz or 2.4 GHz radios for use during evaluation of our GNSS receivers. Those radios need to be properly configured before using them in a receiver integration. This article describes configuration steps for RTK base and RTK rover radios.

Radios can be configured using a simple serial terminal program or FreeWave Tool Suite. This article uses terminal program. For details about Tool Suite go to FreeWave site here.

900 MHz and 2.4 GHz radio programming is identical. In examples below 900 MHz radios are used.

## Terminal Program

At Swift we recommend **CoolTerm** as a free terminal program. It can be downloaded from here and is available for Windows and OSX. For Linux, we use **GtkTerm** which can be installed on Ubuntu via apt.

```
sudo apt-get install gtkterm
```

Other terminal programs can also be used.

## Radio Hardware Setup

For configuration, radios should be connected to your computer via the RS-232 port using a straight RS-232 cable. If there is no RS-232 port on your computer, use a USB to RS-232 adapter. Freewave radios require a 12 V DC power supply. Use the wall power adapter included with the radios, or a 12 V battery, to power radio during configuration.



Fig 1. 900 MHz radio in programming mode

### Entering Radio Programming Mode
Follow this steps to set radio in the programming mode.

- Attach antenna to the radio board. Radio should be never powered without antenna attached.
- Connect radio's RS-232 port to PC, use a USB to RS-232 adapter if necessary
- Power up the radio
- Open terminal program and configure port parameters to 19200 bps, 8 bits, no parity, 1 stop bit, no flow control.
- In **CoolTerm**, click on Options button, set the parameters, then click Connect button.
- In **GtkTerm**, click on Configuration -> Port (Shift+Ctrl+s)
- Press radio Programming Button located next to the Power Input on the radio board (see Fig 1). All three LEDs on the board should show solid green and you will be presented with the following menu on the terminal screen:



Fig 2. 900 MHz radio programming screen on CoolTerm

GtkTerm_Freewave_main_menu.png

Fig 3. 900 MHz radio programming screen on GtkTerm

### Programming Radio for RTK Base Station
Follow this steps to program radio as a transmitter of RTK base station corrections. This radio will work as a Point-to-MultiPoint master. It will be able to transmit corrections to multiple rovers simultaneously.

- Enter radio programming mode as described in the Entering Radio Programming Mode section.
- Press 0 (Set Operation Mode)
- Press 2 (Point to MultiPoint Master)
- Press Esc to return to the Main Menu
- Press 1 (Set Baud Rate)
- Press 1 (115,200)
- Press Esc to return to the Main Menu
- Press 5 (Edit MultiPoint Parameters)
- Press 0 (Number Repeaters)
- Press 0
- Press 1 (Master Packet Repeat)
- Press 0
- Press 2 (Max Slave Retry)
- Press 0
- Press 6 (Network ID)
- Enter desired network ID value in range from 0 to 4095 except 255 and press Enter (value 255 will enable Call Book instead of Network ID). It is recommended to use the last three or four (when lower than 4095) digits of the base station Radio Number as the network ID.
- Press Esc to return to the Main Menu
- Press Esc to Exit Setup
- Power off the radio. Settings are saved in the radio's non-volatile memory. The radio is ready for RTK operation.

### Programming Radio for RTK Rover
Follow this steps to program radio as a receiver of RTK corrections. This radio will work as a Point-to-MultiPoint slave. It will not be able to transmit any data. Only receive it. Use the same radio settings for all rover radios in the system with multiple rovers.

- Enter radio programming mode as described in the above Entering Radio Programming Mode section.
- Press 0 (Set Operation Mode)
- Press 3 (Point to MultiPoint Slave)
- Press Esc to return to the Main Menu
- Press 1 (Set Baud Rate)
- Press 1 (115,200)
- Press Esc to return to the Main Menu
- Press 5 (Edit MultiPoint Parameters)
- Press 0 (Number Repeaters)
- Press 0
- Press 1 (Master Packet Repeat)
- Press 0
- Press 2 (Max Slave Retry)
- Press 0 (Note: if transmission from rover to base is also required, set Max Slave Retry to 1)
- Press 3 (Retry Odds)
- Press 0
- Press 6 (Network ID)
- Enter the same network ID value as set in RTK base station radio above and press <Enter>
- Press Esc to return to the Main Menu
- Press Esc to Exit Setup
- Power off the radio. Settings are saved in the radio's non-volatile memory. The radio is ready for RTK operation.

### LED Indicators
If the radio has been configured correctly, the LEDs should illuminate as shown in the table below.

CD

TX

CTS

Base





off

Rover



off



### Additional Information
For additional information about radio operation and programming read User Manual and Reference Guide available from FreeWave site (FreeWave site will require to register for downloading the document):

- MM2 (900 MHz)
- GXM (2.4 GHz)

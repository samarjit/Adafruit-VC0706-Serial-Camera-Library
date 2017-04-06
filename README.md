UPDATES:

### Baud Rate:
Camera Module vc0706 with baud rate 115200.
According an youtube video, I hardcoded 115200 in the Adafruit_VC0706.cpp directly and tested. The reason was somehow unit_16 was not holding the value 115200. It was getting converted to someother value.
For this baud rate, it does not work with SoftwareSerial. I mean it looks like it works like it will get first few bytes from serial interface. But then it downloads garbage.
Tested with Mega2560 with hardware serial and it works fine.

### Buffer Cleanup:
Important change `Adafruit_VC0706::cameraFrameBuffCtrl(uint8_t command)` I added true to clean up buffer. `return runCommand(VC0706_FBUF_CTRL, args, sizeof(args), 5, true);`
This change fixed most of my problems of downloading garbage before creating image. Before this the garbage was getting into image bytes and corrupting it.

### stepFrame function:
I added stepFrame() function in the library and used it in example just after taking picture. (I am not sure why I have put it after). It also stops current frame so we get clean output. This was much similar to replicating the camtool steps in code.



  This is a library for the Adafruit TTL JPEG Camera (VC0706 chipset)

  Pick one up today in the adafruit shop!
  ------> http://www.adafruit.com/products/397

  These displays use Serial to communicate, 2 pins are required to interface

  Adafruit invests time and resources providing this open source code, 
  please support Adafruit and open-source hardware by purchasing 
  products from Adafruit!

  Written by Limor Fried/Ladyada for Adafruit Industries.  
  BSD license, all text above must be included in any redistribution


To download. click the DOWNLOADS button in the top right corner, rename the uncompressed folder Adafruit_VC0706. Check that the Adafruit_VC0706 folder contains Adafruit_VC0706.cpp and Adafruit_VC0706.h

Place the Adafruit_VC0706 library folder your <arduinosketchfolder>/libraries/ folder. You may need to create the libraries subfolder if its your first library. Restart the IDE.
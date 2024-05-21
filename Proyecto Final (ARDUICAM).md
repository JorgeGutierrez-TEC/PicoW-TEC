```cpp
/*
  Programa: PROYECTO FINAL ARDUINOCAM
  Autor:    Noriega Hernandez Jorge Ivan / Gutierrez Pascual Jorge / Pelaez Flores Jhonatan
  Fecha: 20 / mayo / 2024

  Descripción:
  Programa Final Tomar Foto

  Licencia: Active Learning Labs
  Harvard University 
*/
```
**CODIGO ARDUINO CAM**
```c

#include <TinyMLShield.h>

bool commandRecv = false; // flag used for indicating receipt of commands from serial port
bool liveFlag = false; // flag as true to live stream raw camera bytes, set as false to take single images on command
bool captureFlag = false;

// Image buffer;
byte image[176 * 144 * 2]; // QCIF: 176x144 x 2 bytes per pixel (RGB565)
int bytesPerFrame;

void setup() {
  Serial.begin(9600);
  while (!Serial);

  initializeShield();

  // Initialize the OV7675 camera
  if (!Camera.begin(QCIF, RGB565, 1, OV7675)) {
    Serial.println("Failed to initialize camera");
    while (1);
  }
  bytesPerFrame = Camera.width() * Camera.height() * Camera.bytesPerPixel();

  Serial.println("Welcome to the OV7675 test\n");
  Serial.println("Available commands:\n");
  Serial.println("single - take a single image and print out the hexadecimal for each pixel (default)");
  Serial.println("live - the raw bytes of images will be streamed live over the serial port");
  Serial.println("capture - when in single mode, initiates an image capture");
}

void loop() {
  int i = 0;
  String command;

  bool clicked = readShieldButton();
  if (clicked) {
    if (!liveFlag) {
      if (!captureFlag) {
        captureFlag = true;
      }
    }
  }

  // Read incoming commands from serial monitor
  while (Serial.available()) {
    char c = Serial.read();
    if ((c != '\n') && (c != '\r')) {
      command.concat(c);
    } 
    else if (c == '\r') {
      commandRecv = true;
      command.toLowerCase();
    }
  }

  // Command interpretation
  if (commandRecv) {
    commandRecv = false;
    if (command == "live") {
      Serial.println("\nRaw image data will begin streaming in 5 seconds...");
      liveFlag = true;
      delay(5000);
    }
    else if (command == "single") {
      Serial.println("\nCamera in single mode, type \"capture\" to initiate an image capture");
      liveFlag = false;
      delay(200);
    }
    else if (command == "capture") {
      if (!liveFlag) {
        if (!captureFlag) {
          captureFlag = true;
        }
        delay(200);
      }
      else {
        Serial.println("\nCamera is not in single mode, type \"single\" first");
        delay(1000);
      }
    }
  }
  
  if (liveFlag) {
    Camera.readFrame(image);
    Serial.write(image, bytesPerFrame);
  }
  else {
    if (captureFlag) {
      captureFlag = false;
      Camera.readFrame(image);
      Serial.println("\nImage data will be printed out in 3 seconds...");
      delay(3000);
      for (int i = 0; i < bytesPerFrame - 1; i += 2) {
        Serial.print("0x");
        Serial.print(image[i+1], HEX);
        Serial.print(image[i], HEX);
        if (i != bytesPerFrame - 2) {
          Serial.print(", ");
        }
      }
      Serial.println();
    }
  }
}
```

**CODIGO PIXELES**
```cpp
/*
  This sketch reads a raw Stream of RGB565 pixels
  from the Serial port and displays the frame on
  the window.

  Use with the Examples -> CameraCaptureRawBytes Arduino sketch.

  This example code is in the public domain.
*/

import processing.serial.*;
import java.nio.ByteBuffer;
import java.nio.ByteOrder;

Serial myPort;

// must match resolution used in the sketch
final int cameraWidth = 176;
final int cameraHeight = 144;
final int cameraBytesPerPixel = 2;
final int bytesPerFrame = cameraWidth * cameraHeight * cameraBytesPerPixel;

PImage myImage;
byte[] frameBuffer = new byte[bytesPerFrame];

void setup()
{
  size(320, 240);

  // if you have only ONE serial port active
  //myPort = new Serial(this, Serial.list()[0], 9600);          // if you have only ONE serial port active

  // if you know the serial port name
  myPort = new Serial(this, "COM9", 9600);                    // Windows
  //myPort = new Serial(this, "/dev/ttyACM0", 9600);            // Linux
  //myPort = new Serial(this, "/dev/cu.usbmodem14401", 9600);     // Mac

  // wait for full frame of bytes
  myPort.buffer(bytesPerFrame);  

  myImage = createImage(cameraWidth, cameraHeight, RGB);
}

void draw()
{
  image(myImage, 0, 0);
}

void serialEvent(Serial myPort) {
  // read the saw bytes in
  myPort.readBytes(frameBuffer);

  // access raw bytes via byte buffer
  ByteBuffer bb = ByteBuffer.wrap(frameBuffer);
  bb.order(ByteOrder.BIG_ENDIAN);

  int i = 0;

  while (bb.hasRemaining()) {
    // read 16-bit pixel
    short p = bb.getShort();

    // convert RGB565 to RGB 24-bit
    int r = ((p >> 11) & 0x1f) << 3;
    int g = ((p >> 5) & 0x3f) << 2;
    int b = ((p >> 0) & 0x1f) << 3;

    // set pixel color
    myImage .pixels[i++] = color(r, g, b);
  }
 myImage .updatePixels();

}
```
**FOTO**

![fotoFinal](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/133905295/544468b5-5fc2-46bd-aca6-ec394a9648e5)



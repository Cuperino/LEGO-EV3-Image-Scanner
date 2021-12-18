# LEGO-EV3-Image-Scanner
Image scanner built using the LEGO Mindstorms EV3 Education set and an extra wheel. Includes source from Mindstorms EV3 Software and build instructions. Scans 8.5 inch wide paper but could be adapter to similar page sizes.

## Inputs
* Brick buttons – To control the configuration menus
* Ultrasound – Detect when paper is inserted
* Touch sensor – Reset color sensor position by collision
* Light sensor – Scan pixels to create image

## Output
* 44 by 32 pixels 8 bit grayscale image
* CSV file representative of grayscale 8-bit bitmap data values
* Dithered image on screen

## Parts
This build requires parts from one LEGO MINDSTORMS EV3 set and an additional big wheel, which could be obtained from another of the same sets or a car set.

## Build and sensor details
* This robot implements two force gear configurations, one to move the light sensor on the horizontal axis, through a monorail, the second one to provide a spooling mechanism for the paper that contains the image that is to be scanned.
* Both the spooling mechanism and the monorail use a large motor.
* A counterweight is used to align the monorail's wheel against with the normal force of exerted by the monorail's surface.
* Near the spool is an infrared sensor that allows detecting when the paper is inserted.
* Two touch sensors are placed on each corner of the scanner. They're used to detect when the monorail has reached a corner. Only the sensor at the right side is currently in use.

## Software Notes
The program consists of four stages: UI, Scan, Print Image, Save Image. The UI is built adapting the MVC paradigm to sequential brick programming. It allows n configuration screens, with one value to be configured per screen. Variables used later in the program correspond to a setting each.

### Configuration screens
* uiPrintScreen : bool – If true, a dithered 1-bit image will be printed on the EV3's Screen, to resemble the grayscale image in RAM.
* uiSaveState : bool – If true, a CSV file will be generated from the data in RAM. This file resembles a bitmap file and can be converted into bitmap using an external program like [A-VEKT Image CSV Converter](https://www.avekt.com/en-us/Software/ImageCSV).
* XStartPos : numeric – Indicates the start position in inches, on the X-axis.
* YStartPos : numeric – Indicates the start position in inches, on the Y-axis.
* width : numeric – Indicates the image’ s width in inches.
* height : numeric – Indicates the image’ s height in inches.

### Scanning Phase
* Before scanning, the user is prompted to insert the paper to be scanned and the light sensor’s position is reset to the initial position.
* Scanning consists of changing moving the image sensor across the monorail and the paper across the spool, to create a matrix of independently scanned dots.
* When scanning, one line is scanned from right to left and the next is scanned from left to right. This reduces scan time.
* Once scan is complete, the remaining paper is spooled off the back of the scanner.

### Print Phase
* This phase is optional and enabled by default. It consists of printing the image on the screen.
* The scanned image contains grayscale data, bu the EV3's screen 1-bit black and white. To compensate, each scanned pixel is turned into a 4 by 4 pixel pattern using Ordered (Bayer) dithering, which is then printed on the screen.

### Saving Phase
* This phase is optional.
* Because the EV3’s file block is limited to saving only printable characters, a bitmap image cannot be programmatically generated. Instead, a CSV file is used.
* The CSV can be converted into a bitmap using “A-VEKT Image CSV Converter” with the 8-bit alpha channel setting.
* When creating the CSV, the lines that were scanned in reverse are reordered in a second array.

## Improvements
* Scanner precision could be improved with a second set, which could be used to create a two-rail x-axis instead of a monorail.
* Due to forces exerted by the cables, the monorail is sometimes unstable, which leads to variable focus when capturing some pixels.
* The software can be improved. I release it as it was when I stopped working on it.
* I have no plans to continue developing this project until LEGO releases a version of LEGO MINDSTORMS EV3 for Linux Operating Systems or I find another compelling reason to buy a Mindstorms EV3 set of my own.

## Licensing and Copyright
* Source files are shared under the GNU General Public License 2.0
* Instruction pictures and additional contents are shared under the Creative Commons License Attribution 4.0 International
* Copyright is shared between the University of Puerto Rico at Arecibo and myself.

## Disclaimers
* I developed this for fun as part of an Introduction to Robotics class from the University of Puerto Rico at Arecibo.
* This scanner is loosely based on the printer from “[The Unofficial LEGO MINDSTORMS NXT 2.0 Inventor’s Guide](http://robotsquare.com/books/inventors-guide/)”.
* LEGO, MINDSTORMS, MINDSTORMS EV3, MINDSTORMS NXT are trademarks and/or copyrights of the LEGO Group. Use of them does not imply any affiliation with or endorsement by them.

![alt text width=50](https://github.com/javiercordero/LEGO-EV3-Image-Scanner/raw/master/Instructions/5.%20Final%20result/A1.jpg "Scanner, test and source blocks")
![alt text](https://github.com/javiercordero/LEGO-EV3-Image-Scanner/raw/master/Instructions/5.%20Final%20result/A6.jpg "Scan printed on screen")
![alt text](https://raw.githubusercontent.com/javiercordero/LEGO-EV3-Image-Scanner/master/Instructions/4.%20Cables/D4.jpg "Scanner close up")
![alt text](https://github.com/javiercordero/LEGO-EV3-Image-Scanner/raw/master/Instructions/5.%20Final%20result/A9.jpg "Scanning monorail")

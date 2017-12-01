# neje-laser-upgrades
How-to's and resources for upgrading NEJE (and similar) desktop USB laser
engravers to full GRBL compatibility by replacing the electronics.

Last updated November, 2017.

TODO:

* post wiring harness diagram
* post tip120 schematic

## Full grbl upgrade with Arduino CNC Shield

### Video

I have uploaded a video of the whole upgrade process at [youtu.be/2rbzI-d-bOA](https://youtu.be/2rbzI-d-bOA).

### Links to resources

#### Software-only upgrade

If you are lucky enough to have a machine that can be upgraded without replacing
the board, you can follow [these instructions](http://diyhpl.us/laser_etcher/NEJE_Laser_Etcher/)
to flash a new version of grbl to it.

#### Hardware

![NEJE DK-8-KZ Engraver](images/neje_1000w_laser_engraver_small.jpg "NEJE DK-8-KZ Engraver")

The engraver pictured above and in the video: [KKmoon NEJE DK-8-KZ 1000mW](https://www.amazon.com/gp/product/B01EACK7UG/ref=oh_aui_detailpage_o05_s02)

The Arduino shield used to control the steppers: [Arduino CNC Shield](http://blog.protoneer.co.nz/arduino-cnc-shield/).
I think I mistakenly referred to this as "grblshield" in the video.

[Arduino Uno](https://www.arduino.cc/en/Main/ArduinoBoardUno), the board that connects to the shield above.

[Laser focus adjustment ring](http://www.thingiverse.com/thing:1939313).

#### Software

[Universal Gcode Sender](https://github.com/winder/Universal-G-Code-Sender) -
Used to send commands to the laser.

[J Tech Photonics Laser Tool](https://jtechphotonics.com/?page_id=2012) -
Used to convert images to laser commands.

#### Wiring diagrams and schematics

TODO post tip120 connection schematic

TODO post wiring harness schematic

### Orientation

The origin (X/Y at 0) coordinates should be at the lower-left of the of the
stage. "Lower" here means nearest to front. Make sure moving each axis
negatively will move toward that point, and moving each axis positively will
move away from that point.

### configuring grbl to work in positive space

For J Tech Photonics Laser Tool (in Inkscape), make sure to set the machine
coordinates system to operate in positive space. You will do that by
uncommenting the following line in `config.h` before you upload the grbl
code to the Arduino:

```
#define HOMING_FORCE_SET_ORIGIN
```

### grbl 1.1 settings for Arduino CNC Shield upgrade

```
Grbl 1.1e [‘$’ for help]
$0=10
$1=25
$2=0
$3=0
$4=0
$5=0
$6=0
$10=1
$11=0.010
$12=0.002
$13=0
$20=0
$21=0
$22=0
$23=0
$24=25.000
$25=500.000
$26=250
$27=1.000
$30=1000
$31=0
$32=0
$100=108.000
$101=108.000
$102=250.000
$110=5000.000
$111=5000.000
$112=500.000
$120=500.000
$121=500.000
$122=10.000
$130=27.000
$131=37.000
$132=200.000
```

### Reset default work area

You will probably need to reset the default "work area". Do that with these
two commands:

```
G10 L2 P1 X0 Y0 Z0
G54 X0 Y0 Z0
```

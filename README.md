# Box-Turtle-Chamber-Heater
Box Turtle Chamber Heater

**CYA statement: You do this wrong and burn your house down you are on your own. I'm sharing this with the community in good faith that when you build one, you are doing so with adaquate knowledge with how to handle residential power and best practices for that sort of work.**

For Onshape Users:
[Box Turtle Chamber Heater](https://cad.onshape.com/documents/dbd5d31ea7fb0ca57772b749/w/0325d648209680854414dd13/e/a32dfda47fb2cff5c9efb53f?renderMode=0&uiState=68a8c7e056ba3b52407718ca)

Basic goal of this project is to have a remote accessible chamber heater for the Box Turtle. So it will use Klipper as the OS and Mainsail as the main interface. 

The macro is pretty simple. It's a basic heat soak macro to keep the heater on and at a stable target temp for 25 hrs (as a default). A NeoPixel LED with LED_EFFECTS provides basic status. Possible to use simpler LED controls as well (but not provided in the code). Should be simple to adapt the simpler default NeoPixel code for basic colors to show status. 

https://github.com/julianschill/klipper-led_effect

BOM
| Item  | Source |
| ------------- | ------------- |
| EBB36  | Your favorite vendor |
| 5015 24V DC blower  | Your favorite vendor |
| 24V 100W heater | [Amazon Link](https://www.amazon.com/dp/B081P58S9L) |
| 3950 Thermistor | For the heater |
| 120*C thermal fuse | [Amazon Link](https://www.amazon.com/dp/B08HMTC5GW) |
| HTU21D Sensor | [Amazon Link](https://www.amazon.com/dp/B0CZTXQX2L) |
| 24V power supply - 150 W min | Your favorite vendor |
| 5V buck - a way to power a Pi | Your favorite vendor |
| Rasp Pi | A three will work, but I used a 4b |
| IO2CAN Hat | Your favorite vendor |
| 4010 5v fan | Keep the Pi cool |
| Klipper Expander | Optional to run a 24V fan for the Pi |
| PG7 Gland Nut | Your favorite vendor |
| NeoPixel | Your favorite vendor |
| Mains inlet | I used a leftover one from a printer |
| Microfit 3.0 for CAN wire | 6 pin is used in CAD - Your favorite vendor |
| CAN wires | Your favorite vendor |

The build is straight forward. There's enough room to fish wires to the NeoPixel and the SHT21 through the main body. Leave some slack. Direct solder to the SHT and the NeoPixel. 

The heater pulls 100W so appropriate wires for that. Between the heater and the EBB36, plan on 5 amps max, so 22 AWG for the power. CAN signal can be 24 AWG. When in operation, it sits around 50% duty cycle at 70C heater and ~50C chamber. So 2-3 Amps for longer durations. 

Stuff the 3950 into some vanes of the heater, I used a hex key to open them up just a bit. Should be a press fit. 

Wire in the thermal fuse inline to one of the power feeds to the heater. There is a small gap to feed the thermistor and fuse wires into the heater elements. Those wires then feed down the hole to the EBB26. Run the wires around or under the blower. 

Wire up the EBB with CAN, etc. Get klipper installed on the PI and bring up the IO2CAN hat. Kiauh is a great way to do this from a PiOS lite installation. 

Note about the HTU21D / SHT21 sensors - there's a lot out there and they can be a pain in the ass to find the right combination of settings to use in the printer.cfg file. The one I used has been stable both in this and as a monitor for a filament dryer attached to another printer. Follow the Klipper resources guides for how to setup i2c and the assocated work there. 

When you bring this up for intiial startup, check that the thermistor works and the fan turns on. (much like the startup process for a printer). When that all works, do a PID tune on the heater. Assuming you used the same heater, the PID levels should be pretty close. Then enable the code for the temp/humidity sensor and make sure that works. Then the NeoPixel. 




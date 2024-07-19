## Embedded System-Communication Protocol III ##
*Relays*
Relays are a type of switch that can be turned on and off electronically. Internally they are actually made up of two physically and electrically separated circuits:
the input circuit, which does the switching, and the control circuit, which is what gets turned on and off.
Relays can also do more than just connect or disconnect a single path of electricity: they come with different combinations of 'Poles' and 'Throws' which enable you to do interesting things
when the input circuit is or is not activated - such as toggle between devices, or even completely invert the polarity or an entire circuit! A short-circuit, a low-resistance connection forms between two points in an electric circuit. As a result, the current tends to flow through this newly formed connection rather
than along the intended path. For example, if there is a direct connection between the battery’s negative and positive terminal, the current will flow through it rather than passing through the circuit.
In a short circuit current can flow at dangerously high levels that can damage electronic equipment and even cause explosions in some cases.
   *poles*
The number of Poles a Relay has defines how many switches there are in its control circuit. A Single Pole Relay has one switch, and a Double Pole has two switches. A Single Pole will let you switch only one device on/off, but a Double Pole will let you switch two devices on/off simultaneously. Note that Poles cannot be controlled independently, they are both controlled by the same single input signal.
Throw The number of Throws a Relay has (or more specifically a Pole has) defines how many output contacts each Pole in the Relay can switch between. A Single Throw has one output contact per Pole, and a Double Throw has two output contacts per Pole. A Single Throw can only switch its single contact from on to off and back again, whereas a Double Throw will alternate between its two contacts when the Relay is on or off. When Contact A is turned off, Contact B gets turned on, and when Contact A gets turned back on, Contact B gets turned back off. Pole/Throw Combinations We combine the Poles and Throws of a Relay together to define its Pole and Throw configuration, such as:

Single Pole Single Throw - SPST for short
Single Pole Double Throw - SPDT
Double Pole Single Throw - DPST
Double Pole Double Throw - DPDT

The contacts on a Double Throw Relay on a Double Throw Relay use the following terminology to describe the function of the contact:
Normally Open (or 'NO') - When the Relay is not powered or not activated, this side of the control switch is an Open Circuit with the Common Contact
A device connected to this contact will be OFF by default.

Normally Closed (or 'NC') - When the Relay is not powered or not activated, this side of the control switch is a Closed Circuit with the Common Contact.
A device connected to this contact will be ON by default.

Common (or 'C') - When the Relay is not powered or not activated, the NC contact is connected to this contact. When the Relay is activated the NO contact is connected to this contact.
![terminals](/MODULE%205/relays-module-terminal.png)
Input Power
First, we need to consider what input voltage the Relay requires to be activated and if your circuit can provide the required voltage to it.
Most DC Relays available to makers come as either 5V or 12V input voltages.
Most DC Relays available to makers come as either 5V or 12V input voltages.
If you are using a 5V or 3.3V microcontroller, such as an Arduino or Raspberry Pi Pico, you will have an easier time working with a 5V Relay

Furthermore, if you are using a 3.3V microcontroller, you must check that your relay is compatible with 3.3V power and logic using the datasheet.
![RelLighting](/MODULE%205/Relay+LED.png)

*Switching an LED*
>from machine import Pin
import utime
relay=Pin(16,Pin.OUT)
led=Pin(15,Pin.OUT)
while True:
relay.value(1)
# led.value(1)#Set relay turn on
utime.sleep(5)
relay.value(0) #Set relay turn off
utime.sleep(5)
# led.value(0)

* Switching a Higher Voltage (12V Fan)*
![RelFan](/MODULE%205/relays-12v-fan-.png)
Remove the LED and Resistor from the previous example, and wire up the 12V Fan and Power Supply to the Relay so that it is switching the Negative side of the circuit.

Connect 12V Negative to the Common terminal of the Relay
Connect the Normally Open terminal to the Negative wire of the 12V Fan
Connect the Positive wire of the Fan to 12V Positive.
*Conclusion*
Relays are useful devices that can do a lot more than you might first think!

If your next project needs to control something that runs on a higher power, or you like the idea of having hardware-level fail safes, then look no further than the Relay.

**RC522 RFID Module**
![RFID](/MODULE%205/RC522-RFID-module.jpg)
The RC522 RFID module is a popular and versatile tool for reading and writing data to RFID tags. It's widely used in applications such as access control systems, inventory management, and automated identification due to its affordability and ease of integration with microcontrollers like Arduino and Raspberry Pi.
*Working Principles of RC522 RFID Module*
Electromagnetic Induction:

The RC522 module operates on the principle of electromagnetic induction. It generates an electromagnetic field through its antenna when powered on.
When an RFID tag enters this field, it gets energized and sends back its unique identifier and other data to the reader.
Communication Protocol:

The module communicates with the microcontroller via the Serial Peripheral Interface (SPI) protocol, though it can also use I2C or UART in some configurations.
Commands and data are exchanged between the microcontroller and the RC522 module to read or write data to the RFID tag.
Data Reading:

When an RFID tag is within range, the RC522 detects the tag and reads its unique identifier (UID).
The UID and any additional data stored on the tag are transmitted to the microcontroller for processing.
Data Writing:

The RC522 can also write data to writable RFID tags.
The microcontroller sends a command to the module to write specific data to the tag, which is then stored in the tag's memory.
Operating Frequency:

The RC522 operates at a frequency of 13.56 MHz, which is standard for many RFID applications.
This frequency allows for a read range of a few centimeters to a couple of meters, depending on the tag and antenna used.
**Electric strike**
![elecstrike](/MODULE%205/ELECstrike.webp)

**Access Control System with Raspberry Pi Pico, RGB LED, Electric Strike, Buzzer and RFID**
In this project, we will create a sophisticated access control system using a Raspberry Pi Pico, an RGB LED, an electric strike, a buzzer, and an RC522 RFID scanner. The system will authenticate users based on their RFID cards, providing visual and auditory feedback and controlling access through the electric strike.

Components Required:
Raspberry Pi Pico
RC522 RFID Scanner
RGB LED
Electric Strike Lock
Buzzer
Resistors
Jumper wires
Breadboard
Power supply

Overview
Authentication:

When an RFID card is scanned, the system will check if the card is registered.
If the card belongs to Member 1, the RGB LED will turn green.
If the card belongs to Member 2, the RGB LED will turn yellow.
If the card is unrecognized, the RGB LED will turn red and the buzzer will beep twice.
Access Control:

If a recognized card is scanned, the electric strike lock will be activated to allow entry.
If the card is unrecognized, access will be denied.
Feedback:

A green LED indicates access granted to Member 1.
A yellow LED indicates access granted to Member 2.
A red LED indicates access denied, accompanied by two buzzer beeps.
Circuit Diagram
 (Imagine a circuit diagram showing the connections between Raspberry Pi Pico, RFID scanner, RGB LED, buzzer, and electric strike.)

Wiring Instructions
RFID Scanner:

Connect the SDA pin to GP2 on the Pico.
Connect the SCK pin to GP3.
Connect the MOSI pin to GP4.
Connect the MISO pin to GP5.
Connect the IRQ pin to GP6 (optional).
Connect the RST pin to GP7.
Connect VCC to 3.3V and GND to GND.
RGB LED:

Connect the red pin through a resistor to GP8.
Connect the green pin through a resistor to GP9.
Connect the blue pin through a resistor to GP10.
Connect the common cathode (or anode) to GND (or 3.3V if using common anode).
Buzzer:

Connect the positive pin to GP11.
Connect the negative pin to GND.
Electric Strike:

Connect the control wire to a relay module controlled by GP12.
Power the electric strike as per its specifications.

 
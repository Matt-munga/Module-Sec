## Microcontroller Programming and Access Control Systems I ##
**Communication Protocol in Embedded Systems**

Embedded electronics is all about interlinking circuits (processors or other integrated circuits) to create a symbiotic system. In order for those individual circuits to swap their information,
they must share a common communication protocol.The main focus will be on SPI,UART,I2C. Serial communication is divided into two that is asynchrnous and synchronus serial communication
In serial communication, data is sent one bit at a time using one signal line, so in order for the receiving side to accurately receive the data, the sending side must know at what speed it is sending each bit.

*Serial Communication*
![serialcomm](/MODULE%204/Serailcomm.png)
Sends data bit by bit at one clock pulse
Requires one wire to transmit the data
Preferred for long distance communication
Communication speed is slow.

*Rules of Serial*

The asynchronous serial protocol has a number of built-in rules - mechanisms that help ensure robust and error-free data transfers. These mechanisms, which we get for eschewing the external clock signal, are:

Data bits,
Synchronization bits,
Parity bits,
and Baud rate.
Through the variety of these signaling mechanisms, you'll find that there's no one way to send data serially. The protocol is highly configurable. The critical part is making sure that both devices on a serial bus are configured to use the exact same protocols.

*Baud Rate*

The baud rate specifies how fast data is sent over a serial line. It's usually expressed in units of bits-per-second (bps). If you invert the baud rate, you can find out just how long it takes to transmit a single bit. This value determines how long the transmitter holds a serial line high/low or at what period the receiving device samples its line.

Baud rates can be just about any value within reason. The only requirement is that both devices operate at the same rate. One of the more common baud rates, especially for simple stuff where speed isn't critical, is 9600 bps. Other "standard" baud are 1200, 2400, 4800, 19200, 38400, 57600, and 115200.

The higher a baud rate goes, the faster data is sent/received, but there are limits to how fast data can be transferred. You usually won't see speeds exceeding 115200 - that's fast for most microcontrollers. Get too high, and you'll begin to see errors on the receiving end, as clocks and sampling periods just can't keep up.

Framing the data

Each block (usually a byte) of data transmitted is actually sent in a packet or frame of bits. Frames are created by appending synchronization and parity bits to our data.
![framing](/MODULE%204/framing.jpg)

Data chunk

The real meat of every serial packet is the data it carries. We ambiguously call this block of data a chunk, because its size isn't specifically stated. The amount of data in each packet can be set to anything from 5 to 9 bits. Certainly, the standard data size is your basic 8-bit byte, but other sizes have their uses. A 7-bit data chunk can be more efficient than 8, especially if you're just transferring 7-bit ASCII characters.

After agreeing on a character-length, both serial devices also have to agree on the endianness of their data. Is data sent most-significant bit (msb) to least, or vice-versa? If it's not otherwise stated, you can usually assume that data is transferred least-significant bit (lsb) first.

*Synchronization bits*:

The synchronization bits are two or three special bits transferred with each chunk of data. They are the start bit and the stop bit(s). True to their name, these bits mark the beginning and end of a packet. There's always only one start bit, but the number of stop bits is configurable to either one or two (though it's commonly left at one).

The start bit is always indicated by an idle data line going from 1 to 0, while the stop bit(s) will transition back to the idle state by holding the line at 1.

Parity bits

Parity is a form of very simple, low-level error checking. It comes in two flavors: odd or even. To produce the parity bit, all 5-9 bits of the data byte are added up, and the evenness of the sum decides whether the bit is set or not. For example, assuming parity is set to even and was being added to a data byte like 0b01011101, which has an odd number of 1's (5), the parity bit would be set to 1. Conversely, if the parity mode was set to odd, the parity bit would be 0.

Parity is optional, and not very widely used. It can be helpful for transmitting across noisy mediums, but it'll also slow down your data transfer a bit and requires both sender and receiver to implement error-handling (usually, received data that fails must be re-sent).

9600 8N1 (an example)
9600 8N1 - 9600 baud, 8 data bits, no parity, and 1 stop bit - is one of the more commonly used serial protocols. So, what would a packet or two of 9600 8N1 data look like? Let's have an example!

A device transmitting the ASCII characters 'O' and 'K' would have to create two packets of data. The ASCII value of O (that's uppercase) is 79, which breaks down into an 8-bit binary value of 01001111, while K's binary value is 01001011. All that's left is appending sync bits.

1.*UART*
![UART](/MODULE%204/UARTpic.png)

A universal asynchronous receiver/transmitter (UART) is a block of circuitry responsible for implementing serial communication. Essentially, the UART acts as an intermediary between parallel and serial interfaces.
On one end of the UART is a bus of eight-or-so data lines (plus some control pins), on the other is the two serial wires - RX and TX.
As the R and T in the acronym dictate, UARTs are responsible for both sending and receiving serial data. On the transmit side, a UART must create the data packet- appending sync and parity bits -
and send that packet out the TX line with precise timing (according to the set baud rate). On the receive end, the UART has to sample the RX line at rates according to the expected baud rate, pick out the sync bits, and spit out the data.

2.* I2C*
![I2C](/MODULE%204/I2C-Block-Diagram.jpg)

The Inter-Integrated Circuit (I2C) Protocol is a protocol intended to allow multiple "peripheral" digital integrated circuits ("chips") to communicate with one or more "controller" chips.
It is only intended for short distance communications within a single device. Like Asynchronous Serial Interfaces (such as RS-232 or UARTs), it only requires two signal wires to exchange information.
It can support a multi-controller system, allowing more than one controller to communicate with all peripheral devices on the bus (controller devices take turns using the bus lines to talk to each other).
Data rates fall between asynchronous serial and SPI; most I2C devices can communicate at 100kHz or 400kHz. There is some overhead with I2C; for every 8 bits of data to be sent, one extra bit of meta data
(the "ACK/NACK" bit, which we'll discuss later) must be transmitted.

3.*SPI*
![SPI](/MODULE%204/SPI_CS.png)

The Serial Peripheral Interface (SPI) is a widely used interface bus for transmitting data between microcontrollers and peripheral devices such as shift registers, sensors, and SD cards. Unlike other communication protocols, SPI employs separate clock and data lines, along with a select line to designate the target device. It operates as a "synchronous" data bus, meaning it maintains synchronization between the communicating devices using a clock signal. This clock signal, oscillating at a predetermined rate, precisely coordinates data transfer by indicating when to sample bits on the data line. The timing can be synchronized to either the rising (low to high) or falling (high to low) edge of the clock signal.

Advantages of SPI include its faster data transmission compared to asynchronous serial communication, its ability to utilize simple shift register hardware for reception, and its support for communication with multiple peripherals simultaneously. Additionally, SPI is widely supported by microcontrollers and offers flexibility in terms of data format and clock frequency, making it suitable for a wide range of applications in embedded systems and IoT devices.
*Oled display using SPI*
Interfacing SSD1306 OLED Display with Raspberry Pi Pico MicroPython code is interfaced to the OLED display with the Pico board using Thonny IDE.Thonny IDE requires an SSD1306 driver code which must be written before displaying any text or graphics on the OLED display.
he programming process is divided into two main parts. writing the SSD1306.py driver code and the main.py code. The SSD1306.py code should be written and uploaded first, and then the main.py code can be uploaded and run.
The code for the SSD1306.py file is responsible for setting up the OLED display and configuring it to work with the Raspberry Pi Pico. It includes library imports, initialization commands, and functions for displaying text
and graphics on the OLED screen.The main.py code, on the other hand, is where the main logic of the program resides. It also includes commands for controlling the OLED display and updating the displayed information.
Below is code for Raspberry and Oled
'from machine import Pin, SPI
 from ssd1306 import SSD1306_SPI import framebuf from time import sleep
 from utime import sleep_ms 
 spi = SPI(0, 100000, mosi=Pin(19), sck=Pin(18)) oled = SSD1306_SPI(128, 64, spi, Pin(17),Pin(20), Pin(16)) 
 #oled = SSD1306_SPI(WIDTH, HEIGHT, spi, dc,rst, cs) use GPIO PIN NUMBERS
  while True: oled.text("My name is:",25,25) 
              oled.text("Vallary", 25, 40)
              oled.show() #sleep_ms(10)'

*AHT10 Temperature and Relative Humidity and I2C*
The AHT10 is an accurate temperature and humidity sensor in a very small package that can be accessed via an I2C interface. While it has a temperature measurement range of between -40°C and 85°C, its typical error of ± 0.3 is achieved between around 0°C and 55°C.
![AHT10](/MODULE%204/4-AHT10.webp)
*Connecting the AHT10 to the Pico*
The connection is fairly simple with only four connections being required. Power, ground, Serial CLock line (SCL) and Serial DAta line (SDA). The following connections are used for this example;
AHT10 GND to Ground (pin 38) on the Pico (Black)
AHT10 VIN to the 3V3(OUT) (pin 36) on the Pico (Red)
AHT10 SCL to I2C1 SCL (pin 32, or GPIO27) on the Pico (Orange)
AHT10 SDA to I2C1 SDA (pin 31, or GPIO26) on the Pico (Brown)
>code:
'import time
from machine import Pin, I2C
import ahtx0
 //Create I2C object
sda = Pin(26)
scl = Pin(27)
i2c = I2C(1, scl=scl, sda=sda)
 //Create the sensor object using I2C
sensor = ahtx0.AHT10(i2c)
temperature = round(sensor.temperature, 2)
humidity = round(sensor.relative_humidity, 2)
while True:
print("Temperature: ", temperature, "C")
print("Humidity: ", humidity, "%")
print()
time.sleep(5)'

**Raspberry pi pico + Esp32 communication**
In this project, we established communication between a Raspberry Pi Pico and an ESP32 using the UART protocol. The Raspberry Pi Pico sends a character to the ESP32, which toggles an LED if the expected character is received. Conversely, the ESP32 sends a character back to the Raspberry Pi Pico, which also toggles its onboard LED if the expected character is received.
Procedure
Step 1: Wiring the UART Connections
Connected the TX pin of the Raspberry Pi Pico to the RX pin of the ESP32.
Connected the RX pin of the Raspberry Pi Pico to the TX pin of the ESP32.
Connected the ground (GND) pins of both devices together.
Step 2: Code for Raspberry Pi Pico
The following code was used on the Raspberry Pi Pico:
>import machine
import utime

uart = machine.UART(0, baudrate=9600, tx=machine.Pin(0), rx=machine.Pin(1))
led = machine.Pin(25, machine.Pin.OUT)  # Onboard LED on Raspberry Pi Pico

expected_char = b'A'  # Expected character from ESP32

while True:
    # Send character 'B' to ESP32
    uart.write(b'B')
    utime.sleep(1)
    
    # Check if character is received
    if uart.any():
        received_char = uart.read(1)
        if received_char == expected_char:
            led.toggle()
            print("Received expected character, toggling LED")

Step 3: Code for ESP32
The following code was used on the ESP32:
>char expectedChar = 'B';  // Expected character from Raspberry Pi Pico
char sendChar = 'A';  // Character to send to Raspberry Pi Pico
int ledPin = 2;  // Onboard LED pin for ESP32

void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // Check if character is received
  if (Serial.available() > 0) {
    char receivedChar = Serial.read();
    if (receivedChar == expectedChar) {
      digitalWrite(ledPin, !digitalRead(ledPin));  // Toggle LED
      Serial.println("Received expected character, toggling LED");
    }
  }
  // Send character to Raspberry Pi Pico
  Serial.write(sendChar);
  delay(1000);
}

Step 4: Serial Output
For Raspberry Pi Pico:

The serial output was viewed using the built-in serial monitor in Thonny IDE.
The correct COM port was selected to ensure proper communication.
For ESP32:

The serial output was viewed using the built-in serial monitor in Arduino IDE.
The correct COM port and baud rate (9600) were selected.
Conclusion
This project successfully set up a communication channel between the Raspberry Pi Pico and the ESP32 using the UART protocol. The Raspberry Pi Pico sends a character to the ESP32, which toggles its LED and responds with another character. The Raspberry Pi Pico, in turn, toggles its onboard LED upon receiving the expected character from the ESP32. This setup effectively demonstrates UART communication between two microcontrollers.
**ESP32 Web Server: Controlling LED Lights**
Under the same local area network, different devices can achieve simple communication through the HTTP protocol. The following article introduces a project, that ESP32 realizes remote control by web browser, to control local LED On/Off, by building web server. The status of the LED is displayed on the OLED (Driver: SSD1306).

The web server built by ESP32 plays the following roles:

Enter the IP address of the ESP32 in the browser to access the ESP32 web server;
Click the button on the web browser to change the On/Off of the LED light;
The web server controls the two LEDs by GPIO26 and GPIO27 connected to the ESP32.
![dataflow](/MODULE%204/DATAflo.webp)
After the ESP32 is connected to the wireless LAN through STA mode, ESP32 can obtain a local IP address. After opening the web server, Press the button of the webpage to send a different GET request, and the ESP32 Web server will respond after receiving the request by passing Html Strings to the client, these Html Strings will build the web page and present it to the client (browser).

Note that the ESP32 and the PC need to be in the same WIFI LAN.





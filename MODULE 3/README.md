## Introduction to Embedded System III ##
This module mainly focuses on ESP32 and Arduino microcontrollers as platforms for developing embedded systems. ESP32 is a low-cost, low-power microcontroller with built-in Wi-Fi and Bluetooth connectivity.
The Arduino IDE uses a simplified version of the C++ programming language and is open-source.Some of the key areas will be writing,testing and debugging the firmware for your embedded system and finally deploying it.
We will also carry out various projects using Esp32 and arduino IDE as the programming software.
ESP32 is the platform in use while nodemcu-32s as the board type.
ESP32-DevKit is a small-sized ESP32-based development board produced by Espressif. Most of the I/O pins are broken out to the pin headers on both sides for easy interfacing.
It can either connect peripherals with jumper wires or mount ESP32-DevKit on a breadboard.
![Esp32Pinout](/MODULE%203/ESP-32-Pinout.jpg)

**Development Board Overview**

ESP32 is the platformin use while nodemcu-32s as the board type.
ESP32-DevKit is a small-sized ESP32-based development board produced by Espressif. Most of the I/O pins are broken out to the pin headers on both sides for easy interfacing.
can either connect peripherals with jumper wires or mount ESP32-DevKit on a breadboard

| Key Component | Description |
| ----------- | ----------- |
| ESP32-WROOM-32 | A module with ESP32 at its core. For more information, see ESP32-WROOM-32 Datasheet |
| EN  | Reset button. |
| Boot| Download button. Holding down Boot and then pressing EN initiates Firmware Download mode for downloading firmware through the serial port. |
| USB-to-UART Bridge | Single USB-UART bridge chip provides transfer rates of up to 3 Mbps. |
| I/O | Most of the pins on the ESP module are broken out to the pin headers on the board. You can program ESP32 to enable multiple functions such as PWM, ADC, DAC, I2C, I2S, SPI, etc. |
| 5V Power On LED| Turns on when the USB or an external 5V power supply is connected to the board. For details see the schematics in Related Documents |

*Blinking onboard LED*
>code :void setup() {  
    pinMode(2, OUTPUT);
}  
void loop() {  
  digitalWrite(2, HIGH);  
   delay(1000);  
   digitalWrite(2, LOW);  
   delay(1000);
   }


**LED Based Project**

*Traffic light controller*🚦

The traffic light🚦controller is a specially built system that changes the lights on the timer, to help pedestrians who want to cross, and can even adjust the timing of the light depending on the traffic.
A traffic light, traffic signal, or stop light is a signaling device positioned at a road intersection, pedestrian crossing, or other location in order to indicate when it is safe to drive, ride, or walk using a universal color code.

This project makes use of LED lights for indication purpose and a microcontroller is used for auto changing of signal at specified range of time interval. LED lights gets automatically turns on and off by making corresponding port pin of the microcontroller “HIGH”.

 Analogue inputs are used in control systems with input sensors that produce a voltage, current or resistance change in response to an environmental variation or system measurement and instead of only reading the values of 1 and 0 (on and off),
it can read values in between.The signals from sensors that measure surrounding natural factors such as temperature, pressure, and flow rate are often analog signals, and most control actuators move according to analog signals.
On the other hand, only digital signals can be handled by computers. For this reason, in order to input a signal from a sensor using a computer, or to output a signal to an actuator, it's necessary to have a device that can bridge the analog signal
and the digital signal handled by the computer. That bridge is called an analog I/O interface.
A potentiometer is the perfect analogue device for this activity. Once the potentiometer is turned on the maximum and minimum values are approximately between 0 and 65025.These values are used to control the duty cycle for PWM on the LED.

>code : 'from machine import Pin, PWM, ADC  
pwm = PWM(Pin(15))  
adc = ADC(Pin(26))  
pwm.freq(1000)  
while True:   
duty = adc.read_u16()  
pwm.duty_u16(duty)
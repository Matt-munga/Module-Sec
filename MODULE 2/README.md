## Introduction to Embedded System II ##
**Electronic Circuits and Components**
An electronic circuit is a structure that directs and controls electric current to perform various functions including signal amplification, computation, and data transfer. It comprises several different components such as resistors,
transistors, capacitors, inductors, and diodes. The simplest circuit consists of three elements, including a conducting path, a voltage source, and a load.The following are electronic circuits;

*1.Open Circuit*

An open circuit is one in which the current can’t flow as one or more components are disconnected either intentionally (by using a switch) or accidentally (broken parts).
One can also say it has an incomplete loop.

*2.Closed Circuit*

A closed circuit is one that forms a loop without any interruptions.Currents finds a complete path to follow within a complete loop.

*3.Short Circuit*

A short-circuit, a low-resistance connection forms between two points in an electric circuit. As a result, the current tends to flow through this newly formed connection rather
than along the intended path. For example, if there is a direct connection between the battery’s negative and positive terminal, the current will flow through it rather than passing through the circuit.
In a short circuit current can flow at dangerously high levels that can damage electronic equipment and even cause explosions in some cases.

**Sensors and Actuators**

A sensor is an electrical instrument that monitors and measures physical aspects of an environment and sends an electrical signal to a control center when certain pre-determined conditions are detected.
Sensors turn physical inputs into electrical signals that are output to the control center. They can monitor the health of equipment or the status of a sensitive environment.Sensors turn a physical input into an electrical output,
and actuators do the opposite.They take electrical signals from control modules and turn them into physical outputs. They can perform a wide range of functions, from turning rotors and valves to virtually anything else.
![button](/MODULE%202/button.jpg)

**Physical Computing With Python**

It involves interactive systems that can sense and respond to the world around them. While this definition is broad enough to encompass systems such as smart automotive traffic control systems or factory automation processes,
is not commonly used to describe them. In a broader sense, physical computing is a creative framework for understanding human beings' relationship to the digital world.It puts into use embedded microcontroller-based interactive systems
that can sense the world around them and/or control outputs such as lights, displays and motors. Assembling the hardware elements of a physical computer and programming it to give desired behavior.

**Pulse Width Modulation**

Allows you to give analogue behaviours to digital devices, such as LEDs. This means that rather than an LED being simply on or off, you can control its brightness.For this activity, you can use the circuit from the last step.
>code :   
'from machine import Pin, PWM
from time import sleep   
pwm = PWM(Pin(15))     
pwm.freq(1000)   
while True:   
for duty in range(65025):  
pwm.duty_u16(duty)  
sleep(0.0001)  
for duty in range(65025, 0, -1):  
pwm.duty_u16(duty)  
sleep(0.0001)'

**Analog signals**

Analogue inputs are used in control systems with input sensors that produce a voltage, current or resistance change in response to an environmental variation or system measurement and instead of only reading the values of 1 and 0 (on and off),
it can read values in between.The signals from sensors that measure surrounding natural factors such as temperature, pressure, and flow rate are often analog signals, and most control actuators move according to analog signals.
On the other hand, only digital signals can be handled by computers. For this reason, in order to input a signal from a sensor using a computer, or to output a signal to an actuator, it's necessary to have a device that can bridge the analog signal
and the digital signal handled by the computer. That bridge is called an analog I/O interface.
A potentiometer is the perfect analogue device for this activity.Once the potentiometeris turned on the maximum and minimum values are approximately between 0 and 65025.These values are used to control the duty cycle for PWM on the LED.
>code:'from machine import Pin, PWM, ADC      
pwm = PWM(Pin(15))  
adc = ADC(Pin(26))  
pwm.freq(1000)  
while True:  
duty = adc.read_u16()  
pwm.duty_u16(duty)'

**PIR**

![PIR sensor](/MODULE%202/PIR.jpg)
A passive infrared sensor (PIR sensor) is an electronic sensor that measures infrared (IR) light radiating from objects in its field of view. They are most often used in PIR-based motion detectors. PIR sensors are commonly used in security
alarms and automatic lighting applications. It can detect changes in the amount of infrared radiation impinging upon it, which varies depending on the temperature and surface characteristics of the objects in front of the sensor.
When an object, such as a person, passes in front of the background, such as a wall, the temperature at that point in the sensor's field of view will rise from room temperature to body temperature, and then back again. The sensor converts the resulting
change in the incoming infrared radiation into a change in the output voltage, and this triggers the detection. Objects of similar temperature but different surface characteristics may also have a different infrared emission pattern, and thus moving them
with respect to the background may trigger the detector as well.
You can detect motion and trigger a sound, with the use of a buzzer,with the PIR using the code below:
>code:'from machine import Pin  
from time import sleep
pir = Pin(15, Pin.IN, Pin.PULL_DOWN)  
sleep(1)  
print('Ready')  
while True:  
if pir.value():  
print('Motion Detected')  
sleep(1)


**Ultrasonic Sensor**

![Ultrasonic sensor](/MODULE%202/Ultrasonic.jpg)
An ultrasonic distance sensor sends out pulses of ultrasound which are inaudible to humans, and detects the echo that is sent back when the sound bounces off a nearby object. It then uses the speed of sound to calculate the distance from the object.
Ultrasonic transducer is energized by high voltage pulses and starts to emit an ultrasonic signal. The ultrasonic signal is reflected by the target towards the sensor.Trigger circuit measures the time between the emission and the detection of the signal.
Since the speed of the ultrasonic beam in air is known, it is easy to have not only an indication of the presence of the target, but also a measure of the distance between sensor and target.

*Ultrasonic Sensor Working Principle*

Ultrasonic sensors emit short, high-frequency sound pulses at regular intervals. These propagate in the air at the velocity of sound. If they strike an object, then they reflected back as an echo signals to the sensor, which itself computes the distance
to the target based on the time-span between emitting the signal and receiving the echo. An ultrasonic sensors are excellent at suppressing background interference. Virtually all materials which reflect sound can be detected, regardless of their colour.
Even transparent materials or thin foils represent no problem for an ultrasonic sensor. microsonic ultrasonic sensors are suitable for target distances from 20 mm to 10 m and as they measure the time of flight they can ascertain a measurement with pinpoint accuracy.
If you need to measure the specific distance from your sensor, this can be calculated based on this formula: We know that, Distance= Speed* Time.
The speed of sound waves is 343 m/s. So, Total Distance= (343 * Time of hight(Echo) pulse)/2 Total distance is divided by 2 because signal travels from HC-SR04 to object and returns to the module HC-SR-04. Use the following code to read the Distance;
>code:'from hcsr04 import HCSR04  
from time import sleep
sensor = HCSR04  (trigger_pin=3,echo_pin=2)  
while True:  
distance = sensor.  distance_cm()  
print('Distance: ', distance, 'cm')  
sleep(.25)


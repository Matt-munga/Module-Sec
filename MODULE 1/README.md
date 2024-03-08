## Introduction to Embedded Systems ##
# Project manegement and documentation
In this module, I embarked on a comprehensive journey into the fundamental concepts and practical applications of embedded systems. This module served as a foundational stepping stone, equipping me with essential skills and knowledge necessary for navigating the intricacies of embedded systems development.
I learnt how to use git in order to document my progress and communicating my learnings with peers and instructors. Regular updates and reflections allowed me to track my growth and identify areas for improvement, fostering a collaborative learning environment within the academy. Through mastering version control protocols, particularly Git, I gained proficiency in creating repositories, branching, merging, and resolving conflicts, ensuring seamless collaboration and efficient management of project files.
 I delved into the realm of web development, acquiring skills in HTML and CSS. Through hands-on exercises and projects, I explored website development tools, honing my ability to create visually appealing and functional web page; that is used to portray the work done through the course.
 # Integrated development environment #
An integrated development environment (IDE) is a software suite that consolidates basic tools required to write and test software.It contains a code editor, a compiler or interpreter, and a debugger,
through a single graphical user interface (GUI). The user writes and edits source code in the code editor. The compiler translates the source code into a readable language that is executable for a computer.
And the debugger tests the software to solve any issues or bugs, e.g:

**Thonny IDE**

MicroPython is a programming language that runs directly on embedded hardware, for example,Raspberry Pi Pico. It is a full implementation of the Python (3) programming language.Programming Raspberry Pi Pico is a very easy process.
Users can program the board by connecting it via USB port, and then just drag and drop the file into Raspberry Pi Pico.Added micropython UF2 file - Used for creating a software substrate able to directly transform your Python-like scripts
into machine language code without the need to re-compile your code every time.
To download the Thonny Python IDE follow the given link: https://thonny.org/

**Arduino IDE**

Arduino IDE is an open source software that is mainly used for writing and compiling the code into the Arduino Module.The IDE environment mainly contains two basic parts: Editor and Compiler where former is used for writing the required code
and later is used for compiling and uploading the code into the given Arduino Module.
This environment supports both C and C++ languages. Whenever you’re using Arduino, you need to declare global variables and instances to be used later on. In a nutshell, a variable allows you to name and store a value to be used in the future
while a class is a collection of functions and variables that are kept together in one place.

**Raspberry Pi Pico**

Raspberry Pi Pico is a low-cost, high-performance microcontroller board with flexible digital interfaces.The Raspberry Pi Pico series is a range of tiny, fast, and versatile boards built using RP2040.Programmable in C and MicroPython,
Pico is adaptable to a vast range of applications and skill levels, and getting started is as easy as dragging and dropping a file. Raspberry Pico is a wide range of flexible I/O options includes I2C, SPI, and - uniquely - Programmable I/O (PIO).
These support endless possible applications for this small and affordable package.Below is Raspberry pinout:
![pico-pinout](/MODULE%201/Pico-pinout.jpg)


**MicroPython**

MicroPython is a full implementation of the Python 3 programming language that runs directly on embedded hardware like Raspberry Pi Pico. You get an interactive prompt (the REPL) to execute commands immediately via USB Serial, and a built-in filesystem.
The Pico port of MicroPython includes modules for accessing low-level chip-specific hardware.Pico is programmed by connecting it to a computer via USB, then dragging and dropping a file onto it and adding a downloadable UF2 file to install MicroPython more easily.
The UF2 file is suitable for flashing microcontrollers over MSC (Mass Storage Class; aka removable flash drive).

*Project 1.1:Blink Onboard Led*

Raspberry Pi Pico comes with an Onboard LED that is connected to GP25.I created a micropython program to blink the led on and off in a loop:
>code:.
'from machine import Pin   
 from time import sleep    
 led = Pin(25,Pin.OUT)   
 while True:   
 led.toggle()    
 sleep(1)'

Right now the LED is turning on and off.To stop the code simply click on the Stop button.For practical demonstration watch the video.

*Project 1.2:Controlling Brightness of LED using a potentiometer*

A potentiometer is a manually adjustable variable resistor with 3 terminals. Two of the terminals are connected to the opposite ends of a resistive element, and the third terminal connects to a sliding contact,
called a wiper, moving over the resistive element.
![rotary potentiometer p/o](/MODULE%201/Rot.pot-pinout.jpg)

A potentiometer is a type of position sensor. The primary function of a potentiometer is to measure or monitor displacement. They can be used to measure either linear or rotary displacement and are available in different types depending on the application.

The components used include:

Breadboard
Jumper Wires
Potentiometer
Raspberry Pico
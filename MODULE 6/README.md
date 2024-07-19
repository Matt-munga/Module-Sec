## STUDENT PROJECT##
## RFID and Keypad-Based Access Control System##
This project sets up an access control system using a Raspberry Pi Pico, an OLED display, an RFID reader (RC522), an RGB LED, a buzzer, and a keypad. The system allows access through two methods: RFID card or keypad input, and provides visual and auditory feedback based on the input received.

Components and Initialization
SPI and OLED Display:

Initializes the SPI interface for the SSD1306 OLED display with a resolution of 128x64 pixels.
The OLED is connected via SPI, with pins defined for communication (MOSI, SCK) and control (DC, RES, CS).
LEDs and Buzzer:

Configures pins for the red and green LEDs and the buzzer, setting them as output pins.
Keypad:

Initializes row pins as outputs and column pins as inputs with pull-down resistors.
Defines a 4x4 keypad layout with keys labeled '1'-'9', '0', '*', '#', and 'A'-'D'.
RFID Reader:

Configures the SPI interface for the RC522 RFID reader, with specific pins for communication (SCK, MOSI, MISO) and control (CS, RST).
Access Methods
The system provides two access methods, which are selected through the keypad:

RFID Card:

Displays a menu on the OLED prompting the user to scan an RFID card.
If the scanned card is recognized (in this case, with ID 1497380928), access is granted, the green LED lights up, the buzzer sounds briefly twice, and a welcome message with the current date and time is displayed on the OLED.
If the card is unrecognized, access is denied, the red LED lights up, the buzzer sounds for a longer duration, and an "access denied" message is shown on the OLED.
Keypad:

Prompts the user to enter a passcode on the keypad.
If the correct passcode (2205) is entered, access is granted, the green LED lights up, the buzzer sounds briefly, and a success message is displayed on the OLED.
If an incorrect passcode is entered, the red LED lights up, the buzzer sounds for a longer duration, and an "access denied" message is shown on the OLED.
The code was quite challenging especially when reverting the system after access is other denied or granted . Also the filtering of keypad inputs as instructions and the actual passkey also was a challenge.
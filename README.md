Raspberry Pi Pico Rubber Ducky
This project demonstrates how to use a Raspberry Pi Pico as a USB Rubber Ducky — a device that simulates a keyboard and executes pre-programmed keystrokes to automate tasks or execute payloads on a target computer.

Features
Emulates USB HID (Human Interface Device) like a keyboard.
Allows uploading custom scripts to simulate keystrokes and commands.
Can be used for ethical hacking, security testing, and educational purposes.
Easily programmable via Python (using CircuitPython or MicroPython).
Components Required
Raspberry Pi Pico or Pico W
Micro USB Cable
Computer (for programming the Pico)
CircuitPython or MicroPython installed on the Raspberry Pi Pico
Installation and Setup
1. Install CircuitPython on Raspberry Pi Pico
Download the CircuitPython UF2 file for the Raspberry Pi Pico from CircuitPython Downloads.
Put the Raspberry Pi Pico into bootloader mode by holding the BOOTSEL button and plugging it into your computer.
Drag and drop the downloaded UF2 file onto the Pico's drive.
The Pico will reboot and appear as a CircuitPython device.
2. Setting Up the HID Library
Download the necessary HID libraries for CircuitPython from the Adafruit CircuitPython Bundle.
Copy the adafruit_hid library folder to the lib/ directory on the Raspberry Pi Pico.
3. Writing a Rubber Ducky Script
Create a code.py file in the root of the Pico drive with the following sample script:

python
Copy code
import time
import board
import usb_hid
from adafruit_hid.keyboard import Keyboard
from adafruit_hid.keycode import Keycode

# Initialize keyboard
kbd = Keyboard(usb_hid.devices)

# Delay before starting the script
time.sleep(2)

# Simulate pressing Windows + R to open Run dialog
kbd.press(Keycode.WINDOWS, Keycode.R)
kbd.release_all()

time.sleep(0.5)

# Type 'notepad' to open Notepad
kbd.send(Keycode.N)
kbd.send(Keycode.O)
kbd.send(Keycode.T)
kbd.send(Keycode.E)
kbd.send(Keycode.P)
kbd.send(Keycode.A)
kbd.send(Keycode.D)

# Press Enter to open Notepad
kbd.send(Keycode.ENTER)

# Wait for Notepad to open
time.sleep(1)

# Type a message
for char in "Hello from Raspberry Pi Pico Rubber Ducky!":
    kbd.send(getattr(Keycode, char.upper()))
    time.sleep(0.1)

# Release all keys
kbd.release_all()
4. Deploying and Running the Script
Save your code.py file on the Raspberry Pi Pico drive.
Safely eject the device and plug it into the target machine.
The Pico will automatically execute the programmed keystrokes.
Usage
Create a Payload: Write a keystroke script in Python that simulates the desired input (e.g., opening programs, typing commands).
Deploy: Connect the Raspberry Pi Pico to a target computer. The Pico will act as a HID device, executing your script as soon as it is plugged in.
Test Payloads: You can use this for testing automation tasks, penetration testing, or ethical hacking.
Example Payloads
1. Opening Notepad and Typing Text
Open Notepad by simulating Windows + R, typing notepad, and pressing Enter.
Type "Hello from Raspberry Pi Pico."
2. Opening Command Prompt and Executing Commands
Open Command Prompt by simulating Windows + R, typing cmd, and pressing Enter.
Execute commands like ipconfig or whoami.
3. Browser URL Injection
Open a browser window and inject a URL by simulating Windows + R, typing chrome or firefox, and pressing Enter, followed by a URL.
Customization
Modify Keystrokes: You can edit the code.py file to send different key sequences for your specific use case.
Add Delays: Add time.sleep() between actions if the target computer needs more time to process.
Legal Disclaimer
This project is intended for educational purposes and ethical hacking only. Do not use this tool for malicious purposes. Ensure that you have permission to test any device you use this on.

References
CircuitPython for Raspberry Pi Pico
Adafruit HID Library

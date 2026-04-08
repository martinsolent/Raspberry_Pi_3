---
title: Blinking LED Project
layout: default
has_toc: false
nav_order: 3
---

# Raspberry Pi Project – Blinking LED  

Switching an LED on and off is often considered the **“Hello World”** of hardware programming. It introduces the basics of controlling a GPIO output and helps confirm that your wiring is correct. As your projects grow, you will reuse this same approach when working with motors, relays, sensors, and more advanced embedded systems.

[**NERDCAVE, 2026**. Tutorial 2 - LED Control](https://nerdcave.xyz/docs/raspberry-pi/module-and-sensors/raspberry-pi-module-and-sensors-hello-led)

![all_led_parts]({{ '/img/led_project/all_led_parts.jpg' | relative_url }})

| **Hardware Required:**       | **Installed on the Pi:** |
| ---------------------------- | ------------------------ |
| Raspberry Pi                 | Python 3                 |
| Pi T‑Cobbler Plus            | Visual Studio Code       |
| Breadboard                   |                          |
| 2× Male-to-Male jumper wires |                          |
| 1× LED                       |                          |
| 1× 220 Ω resistor            |                          |


This is what the final set-up of the project should look like:  

![end_led_set_up]({{ '/img/led_project/end_led_set_up.jpg' | relative_url }})

### Hardware Set-up

We will connect the **Breadboard** to the **40-way GPIO connectors** on the **Pi** highlighted below

![end_led_set_up]({{ '/img/led_project/pi_pins.png' | relative_url }})

Using a **Ribbon Cable**

![end_led_set_up]({{ '/img/led_project/ribbon.jpg' | relative_url }})

The Ribbon Cable has notches on both off the connectors to help connect them the right way around

![end_led_set_up]({{ '/img/led_project/ribbon_notch.png' | relative_url }})

The issue you will face is that the **GPIO connector** block on the **Pi** does not have a notch cutout to align the cable correctly – if it is not connected the right way around it will not work or worst damage the **Pi** and/or the components attached to it

![end_led_set_up]({{ '/img/led_project/pi_pins_close_up.png' | relative_url }})

**Tip:** The **Ribbon cable must run straight** between the two boards **with no twist**. Both connectors orient the same way, notches outward from their respective Printed circuit boards (PCBs)

![end_led_set_up]({{ '/img/led_project/ribbon_straight.png' | relative_url }})

First carefully add the **T-Cobbler** to the top of the **Breadboard** making sure you do not bend or break the pins

![end_led_set_up]({{ '/img/led_project/bread-board.png' | relative_url }})

On the **T-Cobbler** the notch cutout is at the top, so connecting the **Cable Ribbon** to this first and the **Pi** second – making sure the cable runs straight between the two devices.

![end_led_set_up]({{ '/img/led_project/cobbler_pins_2.png' | relative_url }})

**Ribbon Cable** connected to the **T-Cobbler**

![end_led_set_up]({{ '/img/led_project/cable_on_breadboard.jpg' | relative_url }})

Then connect the other end to the **Pi**

![end_led_set_up]({{ '/img/led_project/ribbon_on_Pi.jpg' | relative_url }})

#### Wiring the Breadboard  

**Blinking LED Schema**
![end_led_set_up]({{ '/img/led_project/schema_led_project.png' | relative_url }})

Get ready the **2x Jump wire M-M, 1x LED** and **1x Resister (220 Ω)** to connect to the **Breadboard**

![end_led_set_up]({{ '/img/led_project/LED_flash_parts.jpg' | relative_url }})

Connect one end of a **Jump wire** to the left **Power Rail** on the **+ Column** to **Row 5** this aligns to the **GND (Ground)** on the **T-Cobbler**

![end_led_set_up]({{ '/img/led_project/bread_wire_1.png' | relative_url }})

Then attach the other end to **Row 5** in **Column A** in the main component area (the centre grid)

![end_led_set_up]({{ '/img/led_project/bread_wire_2.png' | relative_url }})

Connect the other **Jump Cable** to **Row 6** in **Column A** in the main component area (the centre grid) this aligns to the **GPIO17** on the **T-Cobbler**

![end_led_set_up]({{ '/img/led_project/bread_wire_3.png' | relative_url }})

Connect the other end of **Jump Cable** to **Row 26** on **Column A** in the main component area (the centre grid)

![end_led_set_up]({{ '/img/led_project/bread_wire_4.png' | relative_url }})

We will now add the **Resister;** one end goes into the left **Power Rail** on the **+ Column in Row 27** and the other end to **Row 27 on Column B**

![end_led_set_up]({{ '/img/led_project/bread_wire_6.png' | relative_url }})

And finally, we will add the **LED light** (The longer leg is **+** and the shorter one is **-**)

![end_led_set_up]({{ '/img/led_project/led_plys_minus.png' | relative_url }})


Place the **+** (long) leg in **Column E Row 26** and the **–** (short) leg in **Column E Row 27**

![end_led_set_up]({{ '/img/led_project/bread_wire_7.png' | relative_url }})

### Software set-up on Raspberry Pi

Now we have set up the hardware components we need to set up the software on the **Raspberry Pi** itself which needs to be installed with the current version of **Python and Visual Studio Code** text editor.

Boot up the **Raspberry Pi** and open the **Terminal**

Make sure you have **Python** installed on the **Pi,** normally on a Mac or PC you would Type:

```python --version``` but on a **Raspberry Pi OS** Python 3 is usually pre-installed, so if you type the python command (without a version number) often points to nothing. As below:

![end_led_set_up]({{ '/img/led_project/python_v_1.png' | relative_url }})

So, on a **Raspberry Pi** you need to use ```python3 --version``` instead. This will print the version if **Python** is installed:

![end_led_set_up]({{ '/img/led_project/python_v_2.png' | relative_url }})

If **Python** is not installed or is not the current version go to: <https://www.python.org/downloads/>

**Install Microsoft Visual Studio code**

Install Microsoft Visual Studio code: <https://code.visualstudio.com/docs/setup/raspberry-pi>

**Open Microsoft VS code** make sure the Python extensions are added. <https://code.visualstudio.com/docs/languages/python>

### Create the LED Script

This code creates a simple blinking **LED** effect by turning the **LED** on for **0.5 seconds**, turning it off for **0.5 seconds**, and repeating the cycle indefinitely. Using **led.on(), led.off()** and **sleep(0.5)**  

Create a new project folder

Create a **Python** document and call it **led.py**, add the following code and Save

```
from gpiozero import LED
from time import sleep

# Initialize an LED connected to GPIO pin 17 using the GPIO Zero library.
led = LED(17)


while True:
    # Turn on the LED and print a message to the console.
    led.on()
    print('LED ON')

    # Wait for 0.5 seconds with the LED on.
    sleep(0.5)

    # Turn off the LED and print a message to the console.
    led.off()
    print('LED OFF')

    # Wait for 0.5 seconds with the LED off.
    sleep(0.5)

```



**VS Code** will look like this:

![end_led_set_up]({{ '/img/led_project/vs_code_final.png' | relative_url }})

Now **Run Python File** 

![end_led_set_up]({{ '/img/led_project/run_python_VS.png' | relative_url }})

The **LED** light will now flash 

![end_led_set_up]({{ '/img/led_project/breadboard_flash.gif' | relative_url }})


and **On** and **Off** progress will be printed in the **terminal**

![end_led_set_up]({{ '/img/led_project/Blink_led_VS_code_final.gif' | relative_url }})

To stop it running: mouse click in the **terminal** and then **ctrl+C** on the keyboard

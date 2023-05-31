---
layout: post
title:  "Book and Micropython updates"
date:   2023-05-31 01:35:00
img: 
description: Updates on my book and MicroPython
categories: [Python, PAGE, Tkinter, GUI, Book, Full Circle Magazine]
sitemap: true
---

# Update on my book and MicroPython

Well there's good news.  On Monday, May 29 2023, My book was finally released.

A good friend, a professor from Mexico purchased the very first copy!  Here is the scoop on the costs.

From the publishers site, the paperback version is \$29.95 USD, the kindle Ebook is \$9.95 USD, and they offer a paperback + kindle bundle for \$34.95 USD.

Over on Amazon, both the paperback and kindle Ebook are available.  The paperback is  available for \$32.95 USD and the kindle version is available at \$9.95 USD.

The total page count eventually ended up at 320 pages and it weighs 1.53 pounds.  So even if you don't like the book itself it would make a good door stop!



## MicroPython update

The Pico/Pico-W port of 1.20 has been out for just over a month now, and things are looking up.

### I2C

The I2C problem has gotten better, but not completely settled.  Right now, the default pins have changed from pins 8 and 9 for I2C(0) and 10 and 11 for I2C(1) to 4 and 5 for I2C(0) and 6 and 7 for I2C(1).  It seems that this will be the default for the foreseeable future.

### PWM

PWM (Pulse Width Modulation) has changed a bit as well.  You can still use all the "normal" pin assignments that you could before, but the big change is that there is now a way to set the frequency (which you must have) at the same time that you declare your pins.  So for example, let's say that you are using a motor driver that requires PWM signals to turn on the motor and the pulse cycle of the PWM signal to control the speed.  You would define the pin specifications like this.

```python
class motor_driver():
    def __init__(self,M1A,M1B,M2A,M2B):

        self.M1A = machine.PWM(machine.Pin(M1A),freq=1000)
        self.M1B = machine.PWM(machine.Pin(M1B),freq=1000)
        ...
# Initialize motor object
motor = motor_driver(4,5)
```

Then you can make the motor run forward by using something like this...

```python
def motor_forward():
    motor.speed(50)
```

which will run the motor forward at 50% speed.  Driving the motor backward is just as easy...

```python
def motor_back():
    motor.speed(-50)
```

### BLE

Ble (or Bluetooth Lite) is still not available for the Pico-W, but the MicroPython team is doing their best to get things running.  Things should be available soon.  How long is soon?  As my father would say, "how long is a piece of string?".  Seriously, they really are working hard on getting this important part of the Wireless suite running.

Until next time, be safe.

Greg

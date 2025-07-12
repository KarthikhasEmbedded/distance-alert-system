# distance-alert-system #
A Raspberry Pi Pico-based distance measurement and alert system using an ultrasonic sensor and buzzer.

# 📏 Ultrasonic Distance Alert System

This project is a simple distance measurement and alert system using an **ultrasonic sensor** (HC-SR04) and a **buzzer**, built on the **Raspberry Pi Pico**. When an object comes closer than a preset distance (e.g., 30 cm), the buzzer is activated to warn the user.


# 🔧 Components Used #

- Raspberry Pi Pico
- HC-SR04 Ultrasonic Sensor
- Buzzer
- Breadboard & Jumper Wires
- Power Source (USB)
- Optional: LED (for visual alert)


# ⚙️ Working Principle #

- The **ultrasonic sensor** emits a sound wave and listens for the echo.
- The **time delay** is used to calculate the distance to the object.
- If the object is **closer than 30 cm**, the **buzzer turns ON**.
- If the object is farther away, the buzzer stays OFF.


## 💻 MicroPython Code

from machine import Pin
import utime

trigger = Pin(20, Pin.OUT)
echo = Pin(21, Pin.IN)
buzzer = Pin(15, Pin.OUT)

def ultra():
    trigger.low()
    utime.sleep_us(2)
    trigger.high()
    utime.sleep_us(5)
    trigger.low()

    while echo.value() == 0:
        signaloff = utime.ticks_us()
    while echo.value() == 1:
        signalon = utime.ticks_us()

    timepassed = signalon - signaloff
    distance = (timepassed * 0.0343) / 2
    print("The distance from object is", distance, "cm")

    if distance < 50:
        buzzer.high()
        utime.sleep_ms(100)
        buzzer.low()

while True:
    ultra()
    utime.sleep(0.5)

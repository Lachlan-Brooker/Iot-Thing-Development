# Iot-Thing-Development

The Iot device we created is a Raspberry Pico W Pi that consists of a buzzer and a pentometer. The
point of the device is that the readings of the pentometer will be read by the board and turned
into a value for the buzzer to respond to. Anything past the value of 65535 the buzzer will turn on 
and play a sound. The device was not too hard as it was just code but the development of the 
breadboard is where most of the challenges came, trying to properly align wires and make sure
all components were in the right pin number is where most troubles had occured, none the less 
we were still able to get it working. Later on we experimented with adding an led on that would
change its brightness depending on how far past the value of 65535 it was, the further past the
value the pentometer is the brighter the light got. I contributed to this project through my 
use of ai and online diagram's to guide the construction of the breadbox and the assitance in 
writing code.


Code for IOT thing -->

from machine import Pin, ADC, PWM
import time

potentiometer = ADC(Pin(26))

buzzer = PWM(Pin(15))
buzzer.freq(1000) 
buzzer.duty_u16(0)

    while True:
        pot_value = potentiometer.read_u16()
        frequency = int(500 + (pot_value / 65535) * 1500)
        
        buzzer.freq(frequency)
        buzzer.duty_u16(32768)

        print("Frequency:", frequency)

        time.sleep(0.1)

except KeyboardInterrupt:
    buzzer.duty_u16(0)
    print("Program stopped by user")

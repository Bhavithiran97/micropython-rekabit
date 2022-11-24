
**Python  editor  for micro:bit**

**Step 1: Open  Python Editor**

Open Python editor at: [https://python.microbit.org/v/3](https://python.microbit.org/v/3)

**Step  2:  Add module**

Download MicroPython module from GitHub: [https://github.com/Bhavithiran97/micropython-rekabit](https://github.com/Bhavithiran97/micropython-rekabit)

Click on the Project button in the editor
![1](https://user-images.githubusercontent.com/34527010/195674941-f7cca26e-814f-4e15-af7b-da824efa4423.png)


Click Open button and Add file
![2](https://user-images.githubusercontent.com/34527010/195674959-892eac9e-5b54-4c1d-b6bf-6d901b2cd8a1.png)


Add rekabit.py to the editor
![3](https://user-images.githubusercontent.com/34527010/195674968-d6c444c1-cf62-42a9-b3ce-6906e658193f.png)


## **Add `from rekabit import *` at the top of your program**

## Neopixel

 - This kit has 2 NeoPixels (WS2812B programmable RGB LEDs)
   built-in.
 - REKA:BIT's built-in neopixel works with the default neopixel module that comes with 	  MicroPython on the BBC micro:bit.
 - Use `import neopixel` at the top of your program

Create a NeoPixel strip at pin P8 with 2 LEDs
```python
from rekabit import *
import neopixel

np = neopixel.NeoPixel(pin8, 2)
```
Show color red on all RGB pixels
```python
from rekabit import *
import neopixel

np = neopixel.NeoPixel(pin8, 2)
for LED in range(2):
	np[LED] = (255,0,0)
np.show()
```
Show specific color on each RGB pixels
```python
from rekabit import *
import neopixel

np = neopixel.NeoPixel(pin8, 2)
#rainbow color
np[0]= 255,0,0    #red
np[1]= 255,255,0  #yellow

```
clear all RGB pixels
```python
np.clear()
```
**RGB values for commonly used colors**
 - red = 255,0,0
 - orange = 255,164,0
 - yellow = 255,255,0
 - green = 0,255,0
 - blue = 0,0,255
 - indigo = 75,0,130
 - violet = 138,43,226
 - purple = 255,0,255
 - white = 255,255,255
 - black = 0,0,0

Find more information about Neopixel's MicroPython module here: [https://microbit-micropython.readthedocs.io/en/latest/neopixel.html#module-neopixel](https://microbit-micropython.readthedocs.io/en/latest/neopixel.html#module-neopixel)


## Music
 - REKA:BIT's built-in piezo buzzer works with the default music module that comes with 	  MicroPython on the BBC micro:bit.
 - Use `import music` at the top of your program

Play built-in melodies
```python
from rekabit import *
import music

music.play(music.DADADADUM)
```
Play custom notes
```python
from rekabit import *
import music

#starting tune of "Twinkle Twinkle Little Star"
tune=["C4:1","C4:1","G4:1","G4:1","A4:1","A4:1","G4:1"]
music.set_tempo(ticks=2)
music.play(tune)
```
Find more information about music MicroPython module here: [https://microbit-micropython.readthedocs.io/en/latest/music.html](https://microbit-micropython.readthedocs.io/en/latest/music.html)

## Digital IO

Read digital pin 9
```python
from rekabit import *

while True:
    if pin9.read_digital():
        display.show(Image.HAPPY)
    else:
        display.show(Image.SAD)
```

Write digital on pin 12
```python
from rekabit import *

while True:
    pin12.write_digital(1)
    sleep(500)
    pin12.write_digital(0)
    sleep(500)
```
Find more information about analog MicroPython module here: [https://microbit-micropython.readthedocs.io/en/v1.0.1/pin.html#module-microbit](https://microbit-micropython.readthedocs.io/en/v1.0.1/pin.html#module-microbit)

## Analog IO

Read analog pin 1
```python
from rekabit import *

while True:
    if pin1.read_analog() > 500:
        display.show(Image.HAPPY)
    else:
        display.show(Image.SAD)
```
Write analog on pin 2
```python
from rekabit import *

while True:
    pin12.write_analog(511)
```
Find more information about analog MicroPython module here: [https://microbit-micropython.readthedocs.io/en/v1.0.1/pin.html#pulse-width-modulation](https://microbit-micropython.readthedocs.io/en/v1.0.1/pin.html#pulse-width-modulation)

## DC Motors

```python
from rekabit import *

while True:
	#Move forward at full speed
	run_motor(Motor_All, Direction_Forward, speed=255) 
	sleep(1000)
	
	#Move backward at half speed
	run_motor(Motor_All, Direction_Backward, speed=128) 
	sleep(1000)
	
	#Turn left at full speed
	run_motor(Motor_M1, Direction_Backward, speed=255 )
	run_motor(Motor_M2, Direction_Forward, speed=255 )
	sleep(1000)
	
	#Turn right at half speed
	run_motor(Motor_M1, Direction_Forward, speed=128 )
	run_motor(Motor_M2, Direction=Backward, speed=128 )
	sleep(1000)
	
	#Brake both motors
	brake_motor(Motor_All)
	sleep(1000)
```

## Servos

Rotate Servo 1 to 0 degree when button A is pressed, rotate Servo 1 to 180 degrees when button B is pressed, disable Servo 1 when button A+B pressed
```python
from rekabit import *

while True:
	#Disable all servo when button A and B pressed
	if button_a.is_pressed() and button_b.is_pressed():
		disable_servo(Servo_All)
		
	#Set servo 1 to position 0 degree (min)
	elif button_a.is_pressed():
		sets_servo_position(Servo_S1, position=0 )
		
	#Set servo 1 to position 180 degree (max)
	elif button_b.is_pressed():
		sets_servo_position(Servo_S1, position=180 )
```


## Power Monitoring
This section is for advance user who interested in monitor the power of REKA:BIT. 

Show input voltage
```python
from rekabit import *

while True:
	display.scroll(read_Vin())
```
Show sad face if the voltage is low
```python
from rekabit import *

while True:
	if is_low_batt():
		display.show(Image.SAD)
```
Show sad face if over voltage
```python
from rekabit import *

while True:
	if is_overvoltage():
		display.show(Image.SAD)
```
**Reset REKA:BIT**
Add `power_monitor()` function in a *while loop* to reset the REKA:BIT. 
The motors will not be reset after toggling if this function is not used because the PIC microcontroller in REKA:BIT will not reset without this function.
```python
from rekabit import *

while True:
	power_monitor()
	run_motor(Motor_All, Direction_Forward, speed=255) 
	sleep(1000) 
```


**Python  editor  for micro:bit**

**Step 1: Open  Python Editor**

Open Python editor at: [https://python.microbit.org/v/2.0](https://python.microbit.org/v/2.0)

**Step  2:  Add module**

Download MicroPython module from GitHub: [https://github.com/Bhavithiran97/micropython-edubit](https://github.com/Bhavithiran97/micropython-edubit)

Click on the Load/Save button in the editor
![1](https://user-images.githubusercontent.com/34527010/195673850-9ecde70e-60f3-431c-9133-80c03c9de58f.png)


Click Show File (1) and Add file button

![](https://hackster.imgix.net/uploads/attachments/1164091/7_VLW2b9g3nf.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Add edubit.py to the editor
![16](https://user-images.githubusercontent.com/34527010/92342562-c6b9b580-f0f3-11ea-8cae-24990d6f5fc3.PNG)


## Music Bit
 - REKA:BIT's built-in piezo buzzer works with the default music module that comes with 	  MicroPython on the BBC micro:bit.
 - Use `import music` at the top of your program

Play built-in melodies
```python
import music
music.play(music.DADADADUM)
```
Play custom notes
```python
import music
#starting tune of "Twinkle Twinkle Little Star"
tune=["C4:1","C4:1","G4:1","G4:1","A4:1","A4:1","G4:1"]
music.set_tempo(ticks=2)
music.play(tune)
```
Find more information about music MicroPython module here: [https://microbit-micropython.readthedocs.io/en/latest/music.html](https://microbit-micropython.readthedocs.io/en/latest/music.html)

***Add these lines for the following modules***
 - Use `from rekabit import *` at the top of your program
 - Use `init()` inside a `while True` loop to monitor the power switch and reset microbit when power cycled.


## DC Motors

Run Motor 1 forward at 50% speed when button A is pressed, brake the motor when button B is pressed.
```python
from rekabit import *
while True:
	init()
	if button_a.is_pressed():
		run_motor(M1,Forward, speed=128 )
	elif button_b.is_pressed():
		brake_motor(M1)
```

## Servos

Rotate Servo 1 to 0 degree when button A is pressed, rotate Servo 1 to 180 degrees when button B is pressed, disable Servo 1 when button A+B pressed
```python
from rekabit import *
while True:
	init()
	if button_a.is_pressed() and button_b.is_pressed():
		disable_servo(S1)
	elif button_a.is_pressed():
		sets_servo_position(S1, position=0 )
	elif button_b.is_pressed():
		sets_servo_position(S1, position=180 )
```

## Power

Show power input voltage
```python
from rekabit import *
while True:
	init()
	display.scroll(read_Vin())
```
Show sad face if the voltage is low
```python
from rekabit import *
while True:
	init()
	if is_low_batt():
		display.show(Image.SAD)
```
Show sad face if over voltage
```python
from rekabit import *
while True:
	init()
	if is_overvoltage():
		display.show(Image.SAD)
```

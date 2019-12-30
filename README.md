# BlueDot-for-RC-Car
This is just my file to use the good app BlueDot with my RC Car.
Thanks to the creator of this app! 

Code for RC Car
```python
from bluedot import BlueDot
from gpiozero import Motor
from signal import pause

#moving pins 23,24; steering pins 17,22

bd = BlueDot()
bd.border = True
motoras = Motor(forward=23, backward=24)
servo = Motor(forward=17, backward=22)

def move(pos):
    if pos.angle > -22.5 and pos.angle < 22.5:
        motoras.forward()
    elif pos.angle > 22.5 and pos.angle < 67.5:
        motoras.forward()
        servo.backward()
    elif pos.angle > 67.5 and pos.angle < 112.5:
        servo.backward()
    elif pos.angle > 112.5 and pos.angle < 157.5:
        motoras.backward()
        servo.backward()
    elif pos.angle > -157.5 and pos.angle < 157.5:
        motoras.backward(1)
    elif pos.angle > -157.5 and pos.angle < -112.5:
        motoras.backward()
        servo.forward()
    elif pos.angle > -112.5 and pos.angle < -67.5:
        servo.forward()
    elif pos.angle > -67.5 and pos.angle < -22.5:
        motoras.forward()
        servo.forward()        

def stop():
    motoras.stop()
    servo.stop()

bd.when_pressed = move
bd.when_moved = move
bd.when_released = stop

pause()
```
Thank you!

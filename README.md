# Useless Box

## 3D Printing

<img src="https://i.imgur.com/L8R6NpN.jpg"><BR>Top view of two 3D printed parts: the servo holder and the bopper.<BR><BR>
<img src="https://i.imgur.com/XR51Rlk.jpg"><BR>Side view of aforementioned parts.<BR><BR>

Bopper .stl file can be viewed <a href="">here</a>, and comes sourced from the Thingiverse listing <a href="https://www.thingiverse.com/thing:46289">here</a>. 

## Laser Cutting

<img src="https://i.imgur.com/OqCcntJ.jpg">

## Electronics

**c. Upload code & a photo of your electronic circuit here.**

<img src="https://i.imgur.com/EoExAaL.jpg"><BR>Photo of electronic circuit<br><br>

I used the instructor-provided code to control my useless box. Code is copied below for reference:

```
// Useless Box Lab 5
//
// If we see a voltage change on pin 2 the toggle switch on top of the useless box has 
// changed position and we need to react!
//    A HIGH value on pin 2 means we should activate the servo to open the useless 
//    box and attempt to return the switch to the "off" position.
//    A LOW value on pin 2 means the switch is off and we should return to our 
//    inital (closed box) state.

#include <Servo.h> 

#define servoPin  10
#define switchPin 2

#define closePos  0
#define openPos   180

Servo servo;
int switchState;
int previousSwitchState;

// call this when the input on pin 2 changes (LOW to HIGH *or* HIGH to LOW)
void ToggleSwitch(int switchState)
{    
  if (switchState == HIGH)
  {
    servo.write(openPos);
    //Serial.println("switch state is HIGH.  servo.write(openPos) called to open useless box");
  }
  else
  {
    servo.write(closePos);
    //Serial.println("switch state is LOW.   servo.write(closePos) called to close useless box");
  }
  previousSwitchState = switchState;  // remember that the switch state has changed 
}

void setup()
{
  //Serial.begin(9600);
  //Serial.println("Useless Box Lab 5");

  // start with the box closed and the switch in the off postion
  switchState = LOW;
  previousSwitchState = LOW;

  // connect to our servo and make sure it is in the closed position
  servo.attach(servoPin);
  servo.write(closePos);

  // we should probably pay attention to the switch
  pinMode(switchPin, INPUT); 
}

void loop()
{ 
  int switchState = digitalRead(switchPin);
  if (switchState != previousSwitchState)
    ToggleSwitch(switchState);

  delay(20);
}
```

## Putting it All Together

<a href="https://youtu.be/moohreKvdjw"><b>Video of Useless Box in Action</b></a>

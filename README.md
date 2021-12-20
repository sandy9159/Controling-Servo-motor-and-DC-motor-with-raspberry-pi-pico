# Control DC Motor With L298N Motor Driver And Raspberry Pi Pico

![image](https://user-images.githubusercontent.com/19898602/146796464-22c8d2b2-bc4c-435a-98c9-dc898d9092d2.png)


Hello,

In this article we are going to see how to control 2 DC motor with L298N motor driver and Raspberry Pi Pico. So let’s make it.
We can control DC motor in each direction by pressing push button.

If you are new to Raspberry Pi Pico and wants to get started then click here, it is all about getting started with Raspberry Pi Pico.

For this you will required some components, list is given below.

# Video for DC motor control with raspberry PI Pico

https://youtu.be/P8xXpI5jGPg

# Required Components

> Raspberry Pi Pico

> L298N Motor driver

> DC motor

> Push Button

> Jumper Wires

> Resistor(Above 220 Ohm)

> 12 Volt Adaptor


# Schematic Diagram for DC motor control with Raspberry Pi Pico

![image](https://user-images.githubusercontent.com/19898602/146796688-a5332b32-7f25-4bfe-96d1-9b006f8e3ada.png)


Follow this schematic diagram and make connections.

Connect IN1 pin of L298N with GP0 Pin of Raspberry Pi Pico

Then Connect IN2 pin of L298N with GP1 Pin of Pico

Connect IN3 pin of L298N with GP2 Pin of Pico

Now Connect IN4 pin of L298N with GP3 Pin of Pico

Then Connect GND pin of L298N with GND Pin of Pico, Make comman connection between 12V GND and raspberry pi pico’s GND

Connect push button as shown in schematic diagram.

You can use any value of resistor above 1K Ohm.

To power motors, I connected 12v DC adaptor.

# Coding

To write and upload program here i used Thonny IDE. You can download from here.

Here i write code in micropython.

My code logic is when I press one button, motor will rotate clock wise and when I release that button motor will stop and when I press another button motor will rotate counter clock wise and when I release button motor will stop rotating.

Code is given as below


````

from machine import pin
from time import sleep

IN1 = Pin(0, Pin.OUT)
IN2 = Pin(1, Pin.OUT)
IN3 = Pin(2, Pin.OUT)
IN4 = Pin(3, Pin.OUT)

Button1 = Pin(16, Pin.IN)
Button2 = Pin(17, Pin.IN)

while True:
    
    if Button1.value() == 1:
        IN1.high()
        IN2.low()
        IN3.high()
        IN4.low()
        
    elif Button2.value() == 1:
        IN1.low()
        IN2.high()
        IN3.low()
        IN4.high()
        
    elif Button1.value() == 0:
        IN1.low()
        IN2.low()
        IN3.low()
        IN4.low()
        
    elif Button2.value() == 0:
        IN1.low()
        IN2.low()
        IN3.low()
        IN4.low()
        
        
 ````
 
 Save this code in Raspberry Pi Pico and name it main.py

Now press run button.

Before moving fuurther I would like to tell you something about PCB

Yes PCB are the heart of the electronics based project usually we hesitate to try custom PCB and opt to homemade solutions

like breadboard or Zero PCB earlier I also was in the same boat, I hesitate to try custom PCB my belief was they are much expensive.

but then I came to know about [JLCPCB.com](https://jlcpcb.com/IAT) and I was totally surprised how low price PCB's are they offering 

there PCB quality is best in market, now I always go with PCB for my project and [JLCPCB.com](https://jlcpcb.com/IAT) is my trusted 

PCB manufacturer, you can also try there PCB service for more details you can visit their website [JLCPCB.com](https://jlcpcb.com/IAT)
![image](https://user-images.githubusercontent.com/19898602/134224512-bea8d1c8-9ebe-448d-bbba-0cbecb42d528.png)


![image](https://user-images.githubusercontent.com/19898602/130722577-c30b7b43-ea89-4847-9c6b-058f9fabeda3.png)![image](https://user-images.githubusercontent.com/19898602/130722585-b5268db1-5f17-428f-ba60-b823140f2a70.png)




# Raspberry Pi Pico Servo Motor Control

![image](https://user-images.githubusercontent.com/19898602/146796960-f95ac44a-3fc2-45fe-9593-a76a4e190e0a.png)

Hello,

In this article we are going learn how to control Servo Motor using Raspberry Pi Pico. Here, we are going to control servo by rotating  potentiometer.

So, let’s make it.

# Video

Here you can watch full video or continue to read the post

https://youtu.be/amwoQneE8ZQ

# Require Components

>  Raspberry Pi Pico : https://amzn.to/3fIN7ZQ

>  Servo Motor : https://amzn.to/3rT8iuq

>  Potentiometer : https://amzn.to/2QYAY8A

>  Micro USB cable for programming

# Schematic Diagram

To control Servo Motor using Raspberry Pi Pico please follow the circuit diagram below

![image](https://user-images.githubusercontent.com/19898602/146797148-626bf53b-8596-474a-b57e-c9e7d7563e13.png)


> Connect PWM pin of servo motor with GP0 pin of Raspberry Pi Pico

> Connect Vcc pin of pico with 3.3 Volt of pico

> Connect ground with ground

> Connect terminal 1 of potentiometer with Ground

> Connect output pin of pico with GP28

> Connect terminal 2 of potentiometer with 3.3 volt

> Now connect USB cable with Raspberry Pi Pico and open ThonnyIDE for coding.


# Code

![image](https://user-images.githubusercontent.com/19898602/146797269-f0a90345-6567-44e8-99e9-e5d607d7ef42.png)


To write and upload code, Here i used ThonnyIDE and for coding i used micropython language.


Code Explanation:-
from machine import Pin, PWM

This will import Pin and PWM from machine library

analogvalue = machine.ADC(28)

Here, I defined object named as analogvalue and set analog to digital pin 28 as analogvalue

pwm = PWM(Pin(0))

Another object named pwm set PWM at pin 0 of raspberry pi pico, our servo motor will connect to the pin 0

pwm.freq(50)

This will define frequency

below is the while loop which run continuously it check the analog input from potentiometer and move servo accordingly.

while True:
    reading = analogvalue.read_u16()
    pwm.duty_u16(int(reading/6))

This is main command, it is written in while loop so in run continuously.

In a object named reading, analog read will value store then pwm signal given to same pin on which servo motor connected.

Here, We divide analog read signal by 6, because we get more value and our required value we can get by divide it by 6.


# Full Code

````
from machine import Pin, PWM
analogvalue = machine.ADC(28)
pwm = PWM(Pin(0))
pwm.freq(50)
while True:
    reading = analogvalue.read_u16()
    pwm.duty_u16(int(reading/6))
    
````

Now, save this code in Raspberry Pi Pico and name it main.py

And rotate the knob of potentiometer to change the position of servo motor.



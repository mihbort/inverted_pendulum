# inverted pendulum
### Made by Misha Bortnikov in 2017
### Lego Mindstorms EV3 inverted pendulum implementation

This project represents implementation of classical control theory task — be able to control unstable dynamical system with center of mass above its pivot point.
It is a home task #4 of System Identifiaction and Symulation course. See video with detailed explanation.

[![video explanation](https://img.youtube.com/vi/axrLSOYgsuM/0.jpg)](https://www.youtube.com/watch?v=axrLSOYgsuM)

### Work process
It is possible to program Lego Mindstorms robots using a few instruments:
- LEGO MINDSTORMS EV3 Home Edition
- LEGO C IDE
- Special Python Package
- Matlab

It was interesting for me to implement this task in way close to that intended by the manufacturer, so I choosed *LEGO MINDSTORMS EV3 Home Edition*.

##### Building robot
Before build this robot I had searched the net and found that this task is already solved on LEGO robots, but there is no concise way to do it. Moreover, constructions of this robot is different for each project and usualy contains not used components. So I build my own minimalistic structure.

![Photo of robot](pics/IMG_1316.JPG)

##### PID controller impelmentation
At first glance it seems impossible to implement PID controller in this graphical blocks user interface. Thanks to this [video](https://www.youtube.com/watch?v=AMBWV_HGYj4) it is not so hard task if you know PID theory.
Also is better not to use simple green colored motor controllers. PID control works better with blue colored advanced motor controllers from program.
Tuning of this controllers was implemeted by hands. I get the following coefficients:
- Kp = 3
- Ki = 0.1
- Kd = 0.3

Actually, system works even without Differential part, but Integrator is vital.

##### Gyroscope
LEGO contain only one-axis gyro. It is enough to build this pendulum task, but restricts from doing more interesting things.
The main problem for the gyro is its drifting of zero. It is well known [problem](https://bricks.stackexchange.com/questions/7115/how-can-ev3-gyro-sensor-drift-be-handled).
To overcome it I used only "rate" mode. It gives deriviation of angle form gyro. Unfortunately, this method still have significant drifting, so in best attempts this robot could stand only half a minute.
How to oevercome it completely? The best solution is to make outer feedback loop for the system by speed of wheels.

##### Studying on structure of the pendulum
My first implementation of the robot structure showed rather good results, but there stil was relatively strong vibrations. There are two approaches to get rid of them: more precisely tune PID controller, or change mechanical structure. 
Let's consider what is possible to do with structure to make system more stable:
- increase length of pendulum
- decrease mass of pendulum
- decrease inertia of wheels

I started with changing wide car wheels to small narrow wheels. Result was totatlly not as I expected. Pendulum starts falling almost immediately. First, this wheels have smaller diameter, so motor reached it's maximum speed and it wasn't enough to run. And moreover, I discovered, that slow reaction time caused not because of inertia of wheels, but because of speed reducer inside the drive. Mechanical losses of the reducer are so big, so there is no reason to do anything with wheels inertia. In LEGO exist wheels with bigger diameter and they are also narrow then standart wheels. It would be great to have such wheels on this robot, but unforunately, they are not included in *mindstorms core set*.

Reducing the mass is impossible procedure, because i alredy build minimalistic structure.

And the last machanical way to make the system more stable is to increase length of the pendulum. To do so I put motors on long beams and increase hight on ≈ 30%. This innovation also increased slashes, so gyro data become more noisy, and I believe this noise caused decreaing of stability and increasing drifting of gyro sensor.

##### Video with work of robot
See the last minute of this video to see how it works https://youtu.be/axrLSOYgsuM?t=6m44s

![Photo of robot's screen at work](/pics/screen_of_robot.jpg)

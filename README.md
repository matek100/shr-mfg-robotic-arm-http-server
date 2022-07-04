# Shared Manufacturing Robotic Arm HTTP API

## Jetmax Robotic Arm
Hiwonder JetMax JETSON NANO Robot Arm ROS Open Source robot, more info: https://www.hiwonder.hk/collections/jetson/products/hiwonder-jetmax-jetson-nano-robot-arm-ros-open-source-vision-recognition-program-robot

## HTTP API basic info
* **retrieve robotic arm state**
    * x, y, z coordinates of the robotic arm end effector
    * positions of 3 servo motors
    * positions of 3 joints
    * valuess of 2 PWM signals
    * state of the end effector sucker
* **move robotic arm to a specific location (x, y, z coordinates)**
    * absolute move
* **move robotic arm from a specific state**
    * relative move: dx, dy, dz
    
## Server-side application setup
* download the code to the JetMax Ubuntu computer
* open terminal window and move to the folder where the application code was downloaded
* run <code>npm install</code> to install the required Node.js modules
* open config.json file and define the address of the JetMax Ubuntu computer and the port for the Node.js application
* run <code>nodejs index.js</code> to start the application

## Client-side application usage

| API endpoint | description | parameter(s) | returns |
| ------------ | ----------- | ------------ | ------- |
| /basic/state | retrieve full JetMax Robotic Arm data | / | JSON object |
| /basic/moveTo | absolute move to a specific location | msg={"x": a, "y" = b, "z" = c} | /
| /basic/move | relative move from current location | msg={"x": a, "y" = b, "z" = c} | /

Notes:
* **/basic/moveTo** API endpoint has a pre-set duration of the move 100 ms, the moves are quite slow.
* **/basic/move** endpoint has a pre-set duration of the move of 0.1 ms. **The moves are fast, do not make big changes!**
* When moving the robotic arm consider the limits of the arm end effector and of the operational area. 

## Examples:
* JetMax Robotic Arm state JSON object: 
```json
{
"x": 0, 
"y": -150, 
"z": 200, 
"servo1": 500, 
"servo2": 500, 
"servo3": 520, 
"joint2": 84.4424819946289, 
"joint3": 4.903716564178467, 
"joint1": 120, 
"pwm1": 90, 
"pwm2": 90, 
"sucker": false
}
```
* /basic/moveTo endpoint parameter msg:
```json
{
"x": 0, 
"y": -150, 
"z": 200
}
```
* /basic/move endpoint parameter msg:
```json
{
"x": 0, 
"y": 10, 
"z": 0
}
```

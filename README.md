# Roomba Simulink Library
The following Simulink library contains blocks that allow the iRobot Create 2 to autonomously navigate via 6 built-in IR sensors located on the front bumper. Depending on which sensors are active, the stateflow will determine the speed and direction of each motor to avoid obstacles. Contained in this block is a state that stops the Roomba if the temperature goes above a certain value. There is a wifi init block that creates a TCPIP object using the ad hoc IP address of the RooWifi chip. Lastly, a shutoff block is created utilizing the _PowerOffRoomba_ function that can be used with a switch.

**Must download and open library before running test case**

## Intro
Things needed before starting:

iRobot Create 2:
http://www.irobot.com/About-iRobot/STEM/Create-2.aspx

Matlab Toolbox(Add-ons): 
https://www.mathworks.com/matlabcentral/fileexchange/52644-matlab-toolbox-for-the-irobot-create-2  
**Be sure to edit the _RoombaInit_ function to contain the serial port object with your specific IP address**

RooWifi to wirelessly control the Roomba:
http://www.roowifi.com/products-page/

## Blocks
### **wifi init**
![wifi init](https://github.com/asoussan/markdown_images/blob/master/wifi%20init.jpg)  
The wifi init block has a TCPinit function defined inside that utilizes the coder extrinsic feature of Matlab in order to calls on _RoombaWifiInit_. The block also creates a persistent object that, if empty, will assign the serial port object to a given IP address and mode. It has only one output, which passes the object along to all other blocks.

### **ir sensors**
![ir sensors](https://github.com/asoussan/markdown_images/blob/master/ir%20sensors.jpg)  
This block contains a function that also utilizes coder extrinsic to call _RangeStateRoomba_. The values for all six IR sensors are initalized by setting the array to zero. We also create a persistent object that is set to the arugumnet of _RangeStateRoomba_, or y. Each of the six sensors are blocked if the ouput of that element is 1. This data is the input for the stateflow which will guide the Roomba depending on which sensor, or configuration of sensors, are blocked.

### **temperature**
![temperature](https://github.com/asoussan/markdown_images/blob/master/temperature.jpg)  
The temperpature block utilizes the add-on function _TemperatureRoomba_ to collect data on the temperature of the Roomba at any given time. Another persistent object is defined and set to the input of _TemperatureRoomba_, or temp. This data is also an input to the stateflow contained inside the wheels block.
### **wheels**
![wheels](https://github.com/asoussan/markdown_images/blob/master/wheels.jpg)  
This block contains two main components. The stateflow that performs all decision making for the navigation of the Roomba, and a function that also utilizes coder extrinsic to call _SetWheelVelRoomba_ are contained inside the block. A persistent object is set to the arugment of _SetWheelVelRoomba_ along with two wheel speeds, u1 and u2. The stateflow is set with pre-defined wheel speeds to avoid obstacles depending on which input is given from the ir sensors block. Upon entry, both motors are set to reverse for 1 second to let the Roomba have better perception of objects in front of it. If no sensors are obstructed, the stateflow remains at a slow speed foward. If the temperature is less than or equal to a desired value, the stateflow will continue to run. Otherwise, if the temperature goes above a given value the stateflow will turn off.
### **shutoff**
![shutoff](https://github.com/asoussan/markdown_images/blob/master/shutoff.jpg)  
Shut off block that utilizes add-on function _PowerOffRoomba_ to shut off Roomba at any given time. Must be used in conjuction with switch.

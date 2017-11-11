# Roomba Simulink Library
The following Simulink library contains blocks that allow the iRobot Create 2 to autonomously navigate via 6 built-in IR sensors located on the front bumper. Depending on which sensors are active, the stateflow will determine the speed and direction of each motor to avoid obstacles. Contained in this block is a state that stops the Roomba if the temperature goes above a certain value. There is a wifi init block that creates a TCPIP object using the ad hoc IP address of the RooWifi chip. Lastly, a shutoff block is created utilizing the PowerOffRoomba function that can be used with a switch.
## Intro
Things are needed before starting:

iRobot Create 2:
http://www.irobot.com/About-iRobot/STEM/Create-2.aspx

Matlab Toolbox: 
https://www.mathworks.com/matlabcentral/fileexchange/52644-matlab-toolbox-for-the-irobot-create-2

RooWifi to wirelessly control the Roomba:
http://www.roowifi.com/products-page/

## Blocks
### **wifi init**
![wifi init](https://github.com/asoussan/markdown_images/blob/master/wifi%20init.jpg)

### **ir sensors**
![ir sensors](https://github.com/asoussan/markdown_images/blob/master/ir%20sensors.jpg)

### **temperature**
![temperature](https://github.com/asoussan/markdown_images/blob/master/temperature.jpg)

### **wheels**
![wheels](https://github.com/asoussan/markdown_images/blob/master/wheels.jpg)

### **shutoff**
![shutoff](https://github.com/asoussan/markdown_images/blob/master/shutoff.jpg)

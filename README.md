# Edison IoT Tech Intro
This repo contains all the instructions and example code required for the Edison IoT Tech Intro

##Repo Contents
* Examples - Contains all the example code required
* README.md - This guide

##Order of the Day
* 11:30 Welcome & introductions
* 11:35 Introduction to Intel Edison - presentation
* 11:45 Practical Session
	* Getting started with your Edison
		* Configuring wifi and passwords
		* Blink example
		* Intel XDK and flashing code to the Edison
		* Hooking up sensors
* Break
	* Hooking up the Edison to Enable IoT
		* Adding required sensors to Edison
		* Adding Edison device to Enable IoT account
		* Defining sensor types
		* Registering sensors
	* Pushing data to Enable IoT
		* Javascript example
* 2pm Wrap up and close

##Getting started with your Edison
> **Note:** For all instructions, please read through the entire step before following; there might be some important details later on for how to perform that step!

1. Plug in both USB cables to the Edison and your laptop. Ensure that the small switch on the Edison is positioned towards the 2 micro USB ports.
2. Check the COM port for your Edison.  
**WINDOWS USERS:** Go to the Device Manager (usually under Control Panel or you can search for this) and check under 'Ports (COM and LPT)' for 'USB Serial Port (COMxx)', where xx is the name of the Edison COM port.  
**MAC USERS:** Open a terminal and type 'ls /dev/tty.\*' (note the space between ls and /dev/tty.\*). Check for an entry like '/dev/tty.usbserial-xxxxxxxx' and make note of the last part 'usbserial-xxxxxxxx' as this is your serial port name.
3. Serial into your Edison on the port from the previous step.  
**WINDOWS USERS:** Use putty or equivalent. (If you don't have putty you can quickly download it from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html). Select the Serial radio button, enter the COM port (COM17) and the baud rate 115200, then click 'Open'. A terminal window should appear.  
**MAC USERS:** In your terminal window type the screen command using the serial port name from previous step 'screen /dev/tty.\<yourSerialPortName\> \<baudRate\>' where \<baudRate\> is 115200.  
Example: 'screen /dev/tty.usbserial-AJ035E52 115200'
4. If you have a blank terminal window press 'Return' once. You should now have a login prompt.
5. Login: 'root'
6. To configure wifi, type the command 'configure_edison --wifi'
	1. Select number of the network to join
	2. Enter network password
7. To configure a password for your Edison, type the command 'configure_edison --password'
	1. Enter a new password for your Edison and confirm

##Blink example
1. Open your Grove kit. This has a number of basic input and output electronics, which can easily be hooked up to your Edison via the supplied ribbon cables (the black/red/white/yellow wires) and the Grove shield.
2. The shield is the circuit board with a grid of white connectors hiding under the LCD display. Take it out and carefully but firmly push it onto the black headers on your Edison breakout board. It will only fit one way round, so check you've got everything lined up before forcing it.
3. Find the LED socket board (name marked on bottom), an LED, and a ribbon cable from your Grove kit. Place the LED into the socket on the board (the longer leg of the LED goes into the hole marked +) and connect it with a ribbon cable to the socket marked D2 on the shield. The sockets marked with D are for digital inputs and outputs - things that are either on or off. Those labelled with A are for analog inputs and outputs - things that can vary over a range. We'll come to the analog inputs shortly.

##Intel XDK and flashing code to the Edison
1. To have the LED you just wired up do anything, you need to upload code to your Edison. To do this we will use Intel XDK. Open XDK. You might need to register if it is your first time using it.
2. On the home screen create a new project by clicking on 'Templates' under the 'Start a new project' heading. Then select the 'LED Blink' template and define a save location and name for your new project. The example code will open in the main window. The code uses the 'mraa' library to access the input and output pins where the LED is attached. It will turn the LED on and off for 1 second each but at the moment the code is set up to control the built-in LED on board the Edison breakout board - not the LED that you just hooked up. To change this look for the following line in the code: 
`var myOnboardLed = new mraa.Gpio(13);`  
Replace the 13 with 2 (the number of the D socket that we conneted the LED to).
3. To upload this code to the Edison we first need to connect the Edison to XDK. To do this, go to the dropdown menu towards the bottom of the screen where it says 'IoT Device'. Look through the list for your Edison with the correct IP addess and select it. In the popup window enter the password for your Edison (the one you configured above) and click 'connect'. Wait for the confirmation that your Edison is connected.  

	> To find the IP address of your Edison - go back to your putty/terminal window and type  
**WINDOWS USERS:** 'ipconfig'  
**MAC USERS:** 'ifconfig'  
You will see the IP address for your wifi port (wlan) listed among all the details.  

4. Beside the 'IoT Device' dropdown menu there is also a down arrow button. Press this button to flash the LED blink code to your Edison. You can see the success confirmation in the Intel IoT XDK console at the bottom of the screen. 
5. To run the code on your Edison, click the button with the green play arrow. The LED you wired up should now start to blink on and off. To stop it, you can press the button with the red stop icon in XDK (beside the play button).

##Hooking up sensors
1. Find the light sensor board (name marked on bottom) and a ribbon cable from your Grove kit and connect it with a ribbon cable to the socket marked A0 on the shield.  
2. Go to your XDK and click on 'Projects' at the top right of your screen. Then click 'Start a new project' and 'Templates'. Then select the 'Analog Read' template, select a save location and a name for the new project. The example code will open in the main window. The code uses the 'mraa' library to access the input and output pins where your light sensor is attached. It reads the current sensor value and prints it out.
3. Flash the code to your Edison using the downward arrow button and then start it running using the green play button. In the console you should see a number printed out - this is the current reading from the light sensor. To test it further cover the sensor with your finger and run the code again. You should see a much lower value printed out.

##Hooking up Edison to Enable IoT
1. Find the temperature and sound sensor boards (names marked on the bottom) and two more cable ribbon cables in the Grove kit.
2. Connect the temperature sensor to A1 and the sound sensor to A3 (Note - **not A2** as there are sometimes issues with this port). Make sure you have the sensors connected exactly as described or you might run into issues later on.
3. We will now configure the Edison to be ready to connect it to Enable IoT. Go back to your putty/terminal window and type 'iotkit-admin test'. You should see a success message. This tests the connection between your Edison and Enable IoT. The iotkit-admin is part of an iotkit package that is pre-installed in Edisons. The iotkit-admin simplifies the process of configuring and connecting Edisons with Enable IoT.
4. Next you need to set the ID of your Edison for Enable IoT. A default ID is already assigned and you can see this by typing 'iotkit-admin device-id'. If you want to change the ID of your device (perhaps to something more memorable), type the command 'iotkit-admin set-device-id \<your-new-device-id\>'.
5. Now you are ready to activate your Edison device on Enable IoT, but first you need to get an activation code. To do this, log into your Enable IoT account and navigate to Main menu -> Account -> Details. Click the refresh button beside 'Activation code' and then click the eye button to see what the new activation code is. Then, back in your putty/terminal window type 'iotkit-admin activate \<your-activation-code\>' using the activation code you just got from Enable IoT.
6. To check if your Edison device is now activated in Enable IoT, navigate to Main menu -> Devices, and you should see your Edison listed with the correct device ID.
7. Next, we need to tell Enable IoT what types of sensors we are planning to send data from. Enable IoT already knows about some types of sensor, you can see these by navigating to Main menu -> Accounts -> Catalog. There should be 3 listed by default - Humidity, Powerswitch and Temperature. We need to add two more types - Light and Sound. Create new ones for Light and Sound by clicking 'Add new catalog item' and filling in the details in the popup window. For Light - make sure the component name is 'light' (no capitals), for Sound - make sure the component name is 'sound' (no capitals), otherwise you could have issues later on.
8. Now we go back to the Edison putty/terminal window to register your Edison's 3 connected sensors with the corresonding catalog items listed in Enable IoT. To see the list of possible catalog items that your Enable IoT account has, type the command 'iotkit-admin catalog'. You should see a table with 5 items - the default 3 plus the 2 extra you created. Pay particular attention to the 'measure' and 'id' fields for each item as you will need these now. To register your light sensor, type the command 'iotkit-admin register \<measure\> \<catalog-id\>' using the measure and id fields for the light catalog item. Repeat this step with the other 2 sensors - temperature and sound. The 3 sensors should now be registered with your Edison device on Enable IoT. To check, go to Enable IoT and navigate to Main menu -> Charts. Select your Edison under 'Select device' and you should see the 3 attached sensors listed.
9. We can test the entire setup now by sending some fake data from the Edison. To do this, go to the putty/terminal window and type the follwing 3 commands:  
'iotkit-admin observation light 250'  
'iotkit-admin observation temperature 21'  
'iotkit-admin observation sound 345'  
Go back to Enable IoT and navigate to Main menu -> Charts. Select your Edison device and select all 3 sensors. Below that, click on List view and you should see your 3 fake data points listed.

##Pushing data to Enable IoT
The Edison comes with an iotkit-agent by default, which makes it really easy to push data to Enable IoT. If you were to do this manually (e.g. if you were using a device other than Edison) you would need to handle all the Enable IoT authentication yourself in your own device code. Instead, the iotkit-agent handles all this for us. It does this within a process in the Edison that listens on port 41234 for new Enable IoT data. When new data is received through this port the process checks it is the right format, handles the authentication and pushes it up to Enable IoT - Done!  
1. To start the iotkit-agent we need to run a standard linux system command for starting and stopping such processes:  
'systemctl start iotkit-agent'  
To check it is running sucessfully type:  
'systemctl status iotkit-agent'  
To stop the process type:  
'systemctl stop iotkit-agent'  
2. Go back to XDK and create a new project from a blank template. (Click on Project at the top left of the screen and then 'Start a new project' at the bottom left, then 'Templates' at the top left, and select the blank template option)  
3. Copy and paste the code from the push_data.js example (in the Examples directory of this repo) into the blank template in XDK. This code captures readings from all 3 sensors every 1 second and sends the data to port 41234 where the iotkit-agent takes over and pushes the data to Enable IoT. Flash the code to your Edison using the downward arrow button and then start it running using the green play button. Sensor data should now be streaming up to your Enable IoT account every 1 second.  
4. Go to you Enable IoT account to check if the data is coming through. Navigate to Main menu -> Charts, and select you device and sensors. Below that click on the graph view and you will see a line graph showing the sensor inputs.

##Resources
1. [Enable IoT website](https://dashboard.us.enableiot.com/ui/auth#/login)
2. [Enable IoT Github repo](https://github.com/enableiot/iotkit-agent) - includes much more details of the Enable IoT platform plus reference documents and example code for pushing data from your own device or requesting data from Enable IoT.
3. [The Grove Starter Kit website](http://www.seeedstudio.com/wiki/Grove_-_Starter_Kit_V2.0)
4. [Edison Arduino expansion board hardware guide](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005583.html) - includes details of the jumper settings, pin-out diagram, etc. for the expansion board.
5. [Intel XDK IoT Edition User Guide](https://software.intel.com/en-us/intel-xdk-iot-edition-guide)
6. [Intel IoT Developer Zone](https://software.intel.com/en-us/iot/home)
7. [Edison community forum](https://communities.intel.com/community/makers/edison)
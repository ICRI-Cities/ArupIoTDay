# Arup IoT Tech Intro
This repo contains all the instructions and example code required for Arup IoT Tech Intro

##Repo Contents
* Examples - Contains all the example code required
* README.md - This guide

##Order of the Day
* 11:30 Introductions
* 11:35 Introduction to Intel Edison - presentation
* 11:45 Practical Session
	* Getting started with your Edison
		* Installing tools
		* Configuring wifi and passwords
		* Hooking up sensors
		* Intel XDK and flashing code to the Edison
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
1. Plug in both USB cables to the Edison and your laptop. Ensure that the small switch on the Edison is positioned towards the 2 micro USB ports.
2. Check the COM port for your Edison

**WINDOWS USERS:** Go to the Device Manager (usually under Control Panel or you can search for this) and check under 'Ports (COM and LPT)' for 'USB Serial Port (COMxx)', where xx is the name of the Edison COM port.

**MAC USERS:** Open a terminal and type 'ls /dev/tty.\*' (note the space between ls and /dev/tty.\*). Check for an entry like '/dev/tty.usbserial-xxxxxxxx' and make note of the last part 'usbserial-xxxxxxxx' as this is your serial port name. 
3. Serial into your Edison on the port from the previous step.

**WINDOWS USERS:** Use putty or equivalent. (If you don't have putty you can quickly download it from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html). Select the Serial radio button, enter the COM port (COM17) and the baud rate 115200, then click 'Open'. A terminal window should appear.

**MAC USERS:** In your terminal window type the screen command using the serial port name from previous step 'screen /dev/tty.<yourSerialPortName> <baudRate>' where baudRate is 115200. Example: 'screen /dev/tty.usbserial-AJ035E52 115200'
4. If you have a blank terminal window press 'Enter' once. You should now have a login prompt.
5. Login: 'Root'
6. To configure wifi type 'configure_edison --wifi'
	1. Select number of the network to join
	2. Enter network password
7. To configure a password for your Edison type 'configure_edison --password'
	1. Enter a new password for your Edison and confirm

##Hooking up sensors
1. Open your Grove kit. This has a number of basic input and output electronics, which can easily be hooked up to your Edison via the supplied ribbon cables (the black/red/white/yellow wires) and the Grove shield.
2. The shield is the circuit board with a grid of white connectors hiding under the LCD display. Take it out and carefully but firmly push it onto the black headers on your Edison breakout board. It will only fit one way round, so check you've got everything lined up before forcing it.
3. Find the light sensor board (name marked on bottom) and a ribbon cable from your Grove kit and connect it with a ribbon cable to the socket marked A0 on the shield. The 'A' stands for analog meaning that the socket can handle analog inputs and outputs - things that can vary over a range such as the light sensor. The sockets marked 'D' are for digital inputs and outputs - things that are either on or off.

##Intel XDK and flashing code to the Edison
1. Open XDK. You might need to register if it is your first time using it.
2. On the home screen create a new project by clicking on 'Templates' under the 'Start a new project' heading. Then select the 'Analog Read' template. The example code will open in the main window. The code uses the 'mraa' library to access the input and output pins where your light sensor is attached. It reads the current sensor value and prints it out.
3. To upload this code to the Edison we first need to connect the Edison to XDK. To do this, go to the dropdown menu towards the bottom of the screen where it says 'IoT Device'. Look through the list for the Edison with the correct IP addess. To find the IP address of your Edison - go back to your putty/terminal window and type

**WINDOWS USERS:** 'ipconfig'

**MAC USERS:** 'ifconfig'

You will see the IP address for your wifi port (wlan) listed.
4. In the popup window enter the password for your Edison (the one you configured above) and click 'connect'. Wait for the confirmation that your Edison is connected.
5. Beside the dropdown menu there is also a down arrow. Press this button to flash the analog_read code to your Edison. You can see the success confirmation in the Intel IoT XDK console at the bottom of the screen. 
6. To run the code on your Edison, click the icon with the green play arrow. In the console you should see a number printed out - this is the current reading from the light sensor. To test it further cover the sensor with your finger and run the code again. You should see a much lower value printed out.

##Hooking up Edison to Enable IoT
1. Find the temperature and sound sensor boards (names marked on the bottom) and two more cable ribbon cables in the Grove kit.
2. Connect the temperature sensor to A1 and the sound sensor to A3 (note - NOT A2 as there are sometimes issues with this port). Make sure you have the sensors connected exactly as described or you might run into issues later on.
3. We will now configure the Edison to be ready to connect it to Enable IoT. Go back to your putty/terminal window and type 'iotkit-admin test'. You should see a success message. This tests the connection between your Edison and Enable IoT. The iotkit-admin is part of an iotkit agent that is pre-installed in Edisons. The agent simplifies the process of configuring and connecting Edisons with Enable IoT.
4. Next you need to set the ID of your Edison for Enable IoT. A default ID is already assigned and you can see this by typing 'iotkit-admin device-id'. If you want to change the ID of your device (perhaps to something more memorable), type the command 'iotkit-admin set-device-id <your-new-device-id\>'.
5. Now you are ready to activate your Edison device on Enable IoT, but first you need to get an activation code. To do this, log into your Enable IoT account and navigate to Main menu -> Account -> Details. Click the refresh button beside 'Activation code' and then click the eye button to see what the new activation code is. Then, back in your putty/terminal window type 'iotkit-admin activate <your-activation-code>' using the activation code you just got from Enable IoT.
6. To check if your Edison device is now activated in Enable IoT, navigate to Main menu -> Devices, and you should see your Edison listed with the correct device ID.
7. Next, we need to tell Enable IoT what types of sensors we are planning to send data from. Enable IoT already knows about some types of sensor, you can see these by navigating to Main menu -> Accounts -> Catalog. There should be 3 listed by default - Humidity, PowerSwitch and Temperature. We need to add two more types - light and sound. Create new ones for light and sound by clicking 'Add new catalog item' and filling in the details in the popup window. For light - make sure the component name is 'light', for sound - make sure the component name is 'sound'. Otherwise you could have issues later on.
8. Now we go back to the Edison putty/terminal window to register your Edison's 3 connected sensors with the corresonding catalog items listed in Enable IoT. To see the list of possible catalog items that your Enable IoT account has, type the command 'iotkit-admin catalog'. You should see a table with 5 items - the default 3 plus the 2 extra you created. Pay particular attention to the 'measure' and 'id' fields for each item as you will need these now. To register your light sensor, type the command 'iotkit-admin register <measure> <catalog-id>' using the measure and id fields for the light catalog item. Repeat this step with the other 2 sensors - temperature and sound. The 3 sensors should now be registered with your Edison device on Enable IoT. To check, go to Enable IoT and navigate to Main menu -> Charts. Select your Edison under 'Select device' and you should see the 3 attached sensors listed.
9. We can test the entire setup now by sending some fake data from the Edison. To do this, go to the putty/terminal window and type the follwing 3 commands: 

'iotkit-admin observation light 250'

'iotkit-admin observation temperature 21'

'iotkit-admin observation sound 345'

Go back to Enable IoT and navigate to Main menu -> Charts. Select your Edison device and select all 3 sensors. Below that, click on List view and you should see your 3 fake data points listed.


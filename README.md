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
2. 



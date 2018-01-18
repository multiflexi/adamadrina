# adamadrina
2017/2018 Advanced Digital Architectures project at UPM in Madrid

Tasks for the development of the BBB Project

Authors: Jaroslav Svoboda, Diallo Elhadj Sadou, Andrea Vallejo Puigvert


Session 1

Buildroot : 

	- Download of VMware Workstation version 14.1.1
	- Download of Ubuntu 14.04.5 and install it
	- Download of buildroot source code buildroot2016-05 from https://buildroot.org/
	- Executed in the terminal the following commands in order to open the configuration window: 

	$ cd buildroot-2016.05
	$ make xconfig

- In the Buildroot setup screen, were configured and saved, the items we wanted to install. (Following pages 10 to 11, of the lab guide). 

Notes:

	-This topic is very important since one minimum mistake will carry many problems in the future.  
	-The configuration will be stored in a file named ".config". Do a copy of this file just to be sure we have a backup file.
	- Compiled buildroot using: $ make 

Note: Compilation tooks hours. It was genereated a folder with different files with: root filesystem image, kernel image bootloader image, toolchain.


Session 2

	- Created a github site for collecting the whole information of the project: https://github.com/multiflexi/adamadrina

Booting the BBB from a SD card:

	- Format the SD card: Done according to https://elinux.org/BeagleBoardBeginners#Formatting_the_SD_card_via_fdisk_.22Expert_mode.22
	- First was copied the MLO file to the SD card.
	- After all the remaining files, except for rootfs.ext2, to the SD card in the FAT32 partition for booting the BBB. 
	- The rootfs.ext2  copied in the Linux partition:
	$ cd buildrrot-2016.05/output/images
	$ sudo dd if=rootfs.ext2 of=/dev/sd<n>2
	- Verified all the files were well copied by trying to boot BBB. 

Kernel Configuration:
In order to support the different physical devices and user space application, it is necessary to set up the kernel. However, we dont need to apply 
changes in the default kernel configuration for BBB.

Booting the BBB:

	- In order to have a console in the linux operating system, connect the USB RS-232 adapter to the BBB serial line header. 
	- Connect power supply to the jack identified as 5v or using USB cable. 
	- Open the PuTTy application in the linux host executing in linux terminal: 
	  $ sudo putty
	- Open a session to the serial line: use/dev/ttyUSB0.
	- Apply the power supply pressing S2 button and releasing it after a while. 
	
The BBB will boot from SD card.  If everything is correct, a login prompt will appear. In order to have Linux shell available, either login as
root user or user prdel.


Session 3

Analysis of the correct functioning of the embedded Linux System executing:

	$dmesg
	$uname r
	$ifconfig
	$ps ax

Configuration the network interface of the BBB:

	- In our case we set the network interface in a static way since we did not use DHCP server, in /etc/network/interfaces:
	iface eth0 inet static
		address: 192.168.1.2
		netmask: 255.255.255.0
	- By running the ping command we tested the connection from VM

Adding cross-compiling tools to PATH variable:

	- In the .profile file, it was added: PATH="/home/jaroslav/buildroot-2016-05/buildroot/output/host/usr/bin:$PATH"
	- Download of Eclipse Oxygen 
	- Set the Workspace location.
	- Creation a Eclipse C/C++ project called: gyroRGB
	- Set the toolchain: Cross GCC

In the tool chain editor:

	- Set the configuration as: Debug [Activate]
	- Set the current builder as: Gnu Make Builder

In the tool chain settings:

	- Prefix: arm-buildroot-linux-uclibcgnueabihf-
	- Path: /home/jaroslav/buildroot-2016.05/output/host/usr/bin

Configuration of the search paths for the compiler and linker:

	- Include path:  /home/jaroslav/buildroot-2016.05/output/host/usr/bin
	- Library search path data:  
		output/host/usr/lib 
		/output/host/usr/arm-buildroot-linux-uclibcgnueabihf-lib


Session 4

	- Soldering: The two sensors were soldered to the additional board that is connected to the BBB. In addition, the necessary connections 
were soldered from the sensor pins to the pins of the BBB, following the datasheet of each device.

	- Creation of the C/C++ application

Automatic debugging:

- In Debug configuration -> Main Tab:

		- Configuration of the path to the C/C++ application
		- Set project name
		- Connection with the target (using IP of BBB: 192.168.1.2)
		- Remote path where the executable file will be uploaded
		- User root
		- Make binary executable after upload
		- Mode for the debugging (Automatic)

In Debug Configuration -> Argument Tab:

	- Specify the path of the working directory.

In Debug Configuration -> Argument Tab:

	- Configuration of the path of the gdb application. 
	- Configuraton of the gdbserver path in the target.


Session 5

	- Device tree recognition for the i2C
	- Study how the rgb sensor should behave for our application in the BBB.
	- Search for codes compatible with our sensor, to have a broad idea of how it should be coded.
	- We read the datasheets of the sensors to compare the adress of the each register and to know the function of each register.
	- Implement our own solution  with the necessary requirements to achieve the correct functioning of our application.
	- Compilation of the rgb code.
	- Debugging the rgb code. 
	- Tested the code with the BBB. 


Session 6

	- Study of how the gyroscope sensor should behave for our application in the BBB.
	- Search for codes compatible with our sensor, to have a broad idea of how should be coded.
	- We read the datasheets of the sensors to compare the adress of the each register and to know the function of each register.
	- Implement our own solution with the necessary requirements to achieve the correct functioning of our application.
	- Compilation of the gyroscope code.
	- Debugging the gyroscope code. 
       	- Tested the code with the BBB. 

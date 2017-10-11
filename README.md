# install-vivado2015.2-at-ubuntu14.04
download installation file from xilinx offical website 
(for some reason, the xilinx web installation cannot get access to the internet during installation)
had to download the whole installation file: Xilinx_Vivado_SDK_Lin_2015.2_0626_1.tar.gz
unzip the file in somewhere(I did it under Downloads/Xilinx_Vivado_SDK_Lin_2015.2_0626_1)

open a new terminal, source to the directory(in my case its /home/yourusername/Downloads/Xilinx_Vivado_SDK_Lin_2015.2_0626_1 )

sudo ./xsetup
(you may need to enter your ubuntu password here)
(you may ignore the warning of "cannot connect to the internet" during install)

next...next you then get to the stage of License, select the license you want to add


cd ~
sudo chgrp -R <USERNAME> .Xilinx
sudo chown -R <USERNAME> .Xilinx

these commands are used for changing the permission of folder access, for me, i use it like this: 

cd ~
sudo chgrp -R xd .Xilinx
sudo chown -R xd .Xilinx

nearly there, use this manually setup the system environmental variables:
(actually I dont need SDK, so I didn't ticked this opetion during installation, however, <b>if you do need this function, make sure ticked SDK box during installation</b>, otherwise it would be diffcult to install it afterwards. Xilinx official website said users can add extra function by [help/aditional function in vivado]) however I did try, and the [next] button on the bottom of the window is just hang there. may need to uninstall it and reinstall it to make the SDK install properly.

/opt/Xilinx/Vivado/2015.2/settings64.sh
/opt/Xilinx/SDK/2015.2/settings64.sh(actually after enter this line, i got an error said cannot find beacuse I didn't install SDK in my system, I ignored it for now)


now its the last stage, copy two lines below to .bashrc file 
go to your home directory and use gedit to edit this file, then add following lines at the bottom:
(if your system hide some files, use ctrl+H to show all of them)

#Xilinx tools
source /opt/Xilinx/Vivado/2015.2/settings64.sh
source /opt/Xilinx/SDK/2015.2/settings64.sh


ok, now its time to launch your vivado

 vivado &


more info refer:
https://allmyzynquits.wordpress.com/2015/08/18/installing-vivado-sdk-2015-2-under-ubuntu-14-04/

===================================================================================================
Install cable drivers

when connect board hardware with Vivado hardware manager, the cable driver is needed:

install the prerequisite
On 32-bit
sudo apt-get install gitk git-gui libusb-dev build-essential libc6-dev fxload
On 64-bit
sudo apt-get install gitk git-gui libusb-dev build-essential libc6-dev-i386 fxload



Download the driver source and install:

/*
manully download install_drivers.tar.gz from the following Xilinx website:
secure.xilinx.com/webreg/clickthrough.do?cid=103670

Extract the driver script and its support files by typing:
tar xzvf install_drivers.tar.gz
cd install_drivers
./install_drivers

[actually I followed these steps above from xilinx, I got Error 2 feedback in terminal, so I used steps below]
*/
alternatively, follow steps below:

cd /opt/Xilinx
sudo git clone git://git.zerfleddert.de/usb-driver
cd usb-driver/

On 32-bit
sudo make
On 64-bit
sudo make lib32
[ref http://dreamrunner.org/blog/2012/09/12/install-xilinx-ise-on-the-ubuntu/]


go to directory
/opt/Xilinx/Vivado/2015.2/data/xicom/cable_drivers/lin64

copy the install_script folder to /tmp

sudo -s(change the permition into full sudo access, maynot need this step)
cd /tmp/install_script/install_drivers 
./install_drivers 

you will get 
Digilent Return code = 0
Xilinx Return code = 0
Return code = 0
Driver installation successful.


remember to restart the PC to makesure its working properly.

job done.




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

nearny there, use this manually setup the system environmental variables:

/opt/Xilinx/Vivado/2015.2/settings64.sh
/opt/Xilinx/SDK/2015.2/settings64.sh(actually after enter this line, i got an error said cannot find, I ignored it for now)


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

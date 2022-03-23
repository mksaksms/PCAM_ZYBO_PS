# PCAM_ZYBO_PS

Petalinux and Vivado version 19.1 



Modules : 
vdmadriver 
Application : 
uiotools (must needed - must be started before while booting
initcamera(must needed - must be started on the while booting)
videotest (testing software)


Added device tree : 
Device Tree 

HDF file (design_wrapper_1.hdf) vivado 2019.1 
bit file - final.bit vivado 2019.1 


sudo apt-get install -y gcc git make net-tools libncurses5-dev tftpd zlib1g-dev libssl-dev
flex bison libselinux1 gnupg wget diffstat chrpath socat xterm autoconf libtool tar unzip
texinfo zlib1g-dev gcc-multilib build-essential libsdl1.2-dev libglib2.0-dev zlib1g:i386
screen pax gzip
```
petalinux-config --get-hw-description /home/kawser/Peta19/camera 

petalinux-create -t apps -n uiotools
petalinux-create -t apps -n initcamera
petalinux-create -t apps -n videotest --template c --enable
petalinux-create -t modules -n vdmadriver
petalinux-config -c rootfs
petalinux-build -c uiotools 
petalinux-build -c videotest 
petalinux-build -c vdmadriver
petalinux-build -c initcamera
petalinux-build 
petalinux-package --boot --format BIN --fsbl ./images/linux/zynq_fsbl.elf --fpga ./images/linux/final.bit --u-boot --force
```

To clean any software 
petalinux-build -c uiotools -x cleanall 

To test the software in Petalinux OS : 
check /bin folder 

cd bin 
ls 



Issues : 
I found that if petalinux-create -t apps -n videotest --template c --enable template is not fixed then 
 
 
 To take the picture : 
 ./videotest /dev/video kawser
 
 It will create a kawser.ppm in the /home/root/kawser.ppm
 
 mount /dev/mmcblk0p1 /mnt/ 
 cp /home/root/kawser.ppm /mnt
 
 I have added a sh script in the file named takepicture.sh 
 
 

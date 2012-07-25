uClinux-with-Motorola-Coldfire-MCF5272
======================================

uClinux with Motorola Coldfire MCF5272

Step By Step
------------

### 1 - Download files in [http://www.uclinux.org/] (http://www.uclinux.org/)

    m68k-elf-tools-20030314.sh
    uClinux-dist-20041215.tar.bz2

### 2 - Preparing the uClinux
    $ mkdir /comum
    $ chmod 777 /comum
    $ mkdir /comum/uclinux
    
### 3 - Installation
    #./m68k-elf-tools-20030314.sh

### 4 - Uncompress
    $ /comum/uclinux
    $ tar -jxvf uClinux-dist-20041215.tar.bz2

### 5 - Compile uClinux
    $ cd /comum/uclinux/uClinux
    $ make menuconfig

Kernel Configuration
--------------------
There was an error of no Library

`kurumin@ltr03:/comum/uclinux/uClinux-dist$ apt-get install libncurses5-dev`

Solving the problem

    $ apt-get install libncurses5-dev

Continuing

    $ make dep
    $ make

### 6 - Install TFTPD
The TFTP server used for the server image file uClinux

    # apt-get install tftpd
    # mkdir /tftpboot
    # chmod 777 tftpboot

### 7 - Edit the file /etc/inetd.conf
To that TFTP is running as a service, every time the computer starts

    $ mcedit /etc/inetd.conf

`tftp    dgram   udp   wait   nobody   /usr/sbin/tcpd   /usr/sbin/in.tftpd /tftpboot`

### 8 - Restart network services

    $ /etc/init.d/inetd restart

### 9 - Verify that the TFTP service is already running

    $ netstat -tuanp

`udp        0      0 0.0.0.0:69              0.0.0.0:*                          4477/inetd`

### 10 - Install MINICOM

    # apt-get install minicom

The End :)
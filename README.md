uClinux-with-Motorola-Coldfire-MCF5272
======================================

uClinux with Motorola Coldfire MCF5272

Step By Step
------------
1. [Download files in http://www.uclinux.org/] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#1---download-files-in-httpwwwuclinuxorg)
2. [Preparing the uClinux] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#2---preparing-the-uclinux)
3. [Installation] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#3---installation)
4. [Uncompress] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#4---uncompress)
5. [Compile uClinux] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#5---compile-uclinux)
6. [Install TFTPD] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#6---install-tftpd)
7. [Edit the file /etc/inetd.conf] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#7---edit-the-file-etcinetdconf)
8. [Restart network services] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#8---restart-network-services)
9. [Verify that the TFTP service is already running] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#9---verify-that-the-tftp-service-is-already-running)
10. [Install MINICOM] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#10---install-minicom)
11. [Recognizing the plate MOD5272 the TFTP server] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/edit/master/README.md#11---recognizing-the-plate-mod5272-the-tftp-server)
12. [Running MINICOM] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/edit/master/README.md#12---running-minicom)

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
Used to perform serial communication with the board

    # apt-get install minicom

#### Configuring the Serial Port
    # minicom -s mod5272

Configuration

    Baudrate = 9600
    Serial port = /dev/ttyS0
    Hardware Flow Control = No
    Software Flow Control = No

#### Save Configuration as mod5272
`Exit from Minicom`

### 11 - Recognizing the plate MOD5272 the TFTP server
It is recommended crossover cable connection to speed up the detection process

    # arp -s 10.2.4.123 00:03:F4:01:1E:F0

### 12 - Running MINICOM
Reset development board if necessary

    $ minicom -o mod5272

Result

    Netburner MOD-5272 (5272) Monitor V1.00 Sep 26 2003 13:57:32
    HELP for help
    nb>

The End :)
uClinux with Motorola Coldfire MCF5272
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
13. [Finish And Run] (https://github.com/tulioseveriano/uClinux-with-Motorola-Coldfire-MCF5272/blob/master/README.md#13---finish-and-run)

### 1 - Download files in [http://www.uclinux.org/] (http://www.uclinux.org/)

    m68k-elf-tools-20030314.sh
    uClinux-dist-20041215.tar.bz2
[m68k-elf-tools-20030314.sh](http://www.uclinux.org/pub/uClinux/m68k-elf-tools/m68k-elf-tools-20030314.sh)

[uClinux-dist-20041215.tar.bz2](http://www.uclinux.org/pub/uClinux/dist/uClinux-dist-20041215.tar.bz2)

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

Solving the problem

    kurumin@ltr03:/comum/uclinux/uClinux-dist$ apt-get install libncurses5-dev

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

#### Set the development board
Use the setup command

    nb>setup
    
Configuration

    MAC address=00-03-F4-01-1E-F0
    1.)IP Address =10.2.4.123
    2.)IP Mask    =255.255.0.0
    3.)IP Gateway =10.2.0.1
    4.)TFTP Server=10.2.8.181
    5.)TFTP File  =
    6.)Baudrate  =9600
    7.)Wait      =1
    8.)Boot to Monitor
    9.)Exceptions CauseReboot
    1-9 to change, S to save, X to exit

### 13 - Finish And Run
copy image to the /tftpboot

    cp images/image.s19 /tftpboot/IMAGE.S19
    minicom -o mod5272

Reboot the board with RESET button

Loads the image into RAM

    ndl image.s19
    
Address boot file found in

    $ mcedit linux-2.4.x/arch/m68knommu/platform/5272/MOD5272/ram.ld

Initializes the image that has already been preloaded

    go 2020400

#### Results of some commands

ps

    /> ps
      PID PORT STAT SIZE SHARED %CPU COMMAND
        1      S    141K     0K  0.8 /bin/init
        2      S      0K     0K  0.0 keventd
        3      R      0K     0K  0.0 ksoftirqd_CPU0
        4      S      0K     0K  0.0 kswapd
        5      S      0K     0K  0.0 bdflush
        6      S      0K     0K  0.0 kupdated
       18      S     41K     0K  0.0 portmap
       19   S0 S     27K     0K  0.1 /bin/sh
       20   S0 S     26K     0K  0.2 /bin/agetty 9600 ttyS1
       31   S0 R     20K     0K  0.0 ps

cat /proc/meminfo

    />cat /proc/meminfo
           total:    used:    free:  shared: buffers:  cached:
    Mem:   6275072  1220608  5054464        0   151552   131072
    Swap:        0        0        0
    MemTotal:         6128 kB
    MemFree:          4936 kB
    MemShared:           0 kB
    Buffers:           148 kB
    Active:            180 kB
    Inactive:           96 kB
    HighTotal:           0 kB
    HighFree:            0 kB
    LowTotal:         6128 kB
    LowFree:          4936 kB
    SwapTotal:           0 kB
    SwapFree:            0 kB

cat /proc cpuinfo

    /> cat /proc cpuinfo
    CPU:            COLDFIRE(m5272)
    MMU:            none
    FPU:            none
    Clocking:       59.2MHz
    BogoMips:       39.52
    Calibration:    19763200 loops

The End :)
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


The End :)
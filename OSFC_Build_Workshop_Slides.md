
# Slide 1
## Building Open Source Unified Extensible Firmware Interface (UEFI) Firmware with EFI Development Kit II (EDK II)
- Laurie Jarlstrom laurie.Jarlstrom@intel.com,
- Stephano Cetola Stephano.Cetola@intel.com, 
- Brian Richardson Brian.Richardson@intel.com 
- Intel Corporation
- OSFC - 2018

# Slide 2
## Workshop Objective
- Open Virtual Machine Firmware (OVMF) Platform Overview 
- Build a EDK II Platform using OVMF package and use QEMU  to boot to UEFI Shell
- Run UEFI Shell Commands  and Scripts


# Slide 3
## What is OVMF?
- Open Virtual Machine Firmware for UEFI

# Slide 4
##  Where? Tianocore.org 

# Slide 5
## Projects 	GitHub Tianocore.org
- edk2 – Platforms on edk2- “CORE”
	- BeagleBoardPkg
	- Coreboot…Pkg
	- DuetPkg
	- Nt32Pkg
	- OvmfPkg
	- QuarkPlatformPkg

- See Readme.md files

# Slide 6
## Open Virtual Machine Firmware (OVMF) 
- Uses EDK II to support firmware in the OvmfPkg platform package
- Supports UEFI:  Helps develop/debug drivers & applications
- QEMU VM; emulates IA32 (x86)/X64 (x86-64) based system  
- Exit condition  UEFI Shell
- Tool Chain/OS Support
- Information  Ovmf wiki, Tianocore.org

# Slide 7
## OVMF BIOS w/ QEMU Boots to UEFI Shell
- Boots to UEFI Shell

# Slide 8
## OVMF with QEMU Boot Options
- Possibilities to test  OS installers,  UEFI boot loaders and unique, dependent guest OS features.

# Slide 9
## OVMF with QEMU Test RAM Disk
- Create a  RAM disk, either raw or from a file

# Slide 10
## OVMF with QEMU Test Secure Boot
- Development and testing of Secure Boot-related features in guest operating systems
- Enable the Build switch SECURE_BOOT_ENABLE
- Uses OpenSsl Libraries


# Slide 11
## OVMF with QEMU boot to UEFI Shell
- OVMF will Boot to the Internal UEFI Shell Application by default

- The UEFI Shell is an extensive & Standardized  Pre-OS UEFI Application



# Slide 12
## UEFI – PI & EDK II Boot Flow

# Slide 13
## UEFI Shell Elements
- The UEFI Shell is an extensive & Standardized  Pre-OS UEFI Application

# Slide 14
## UEFI Shell Usage
- Execute pre-boot programs
- Move files between devices 
- Load and test a pre-boot UEFI driver



# Workshop Start
# Slide 15
## BUILD OVMFPKG 
- Setup OvmfPkg to build and run w/ QEMU* and Ubuntu*

# Slide 16
## Extract Container
- Copy “docker“ directory from usb thumb drive to local hard driver


- Load the edk2-Ubuntu.dockerimage
```
 bash$ docker load –i edk2-Ubuntu.dockerimage
```

- For OpenSuse – also set up share
```
 bash$ xhost local:root
```
- Create a work directory 
```
 bash$ mkdir workspace
 bash$ cd workspace
```

- Docker run command  from the docker directory
```
 bash$ . ~/docker/edk2-ubuntu.sh
```

# Slide 17
## Extract Container

- From this point on the terminal window for Ubuntu 16.04 will be available and $HOME/workspace will be the shared directory between the host and the Docker container
- window will look like: 
```
[edk2-ubuntu] workspace #
```
- Open Multiple terminal windows run the script OpenEdk2Window.sh
```
 bash$ docker exec –it edk2 bash
```

# Slide 18
## Pre-requisites Ubuntu 16.04 
- Instructions from: tianocore wiki Ubuntu_1610 

- Example Ubuntu 16.04

- The following need to be accessible for building Edk2, From the terminal prompt (Cnt-Alt-T):
```
 bash$ sudo apt-get install build-essential uuid-dev iasl git gcc-5 nasm  
 bash$ sudo apt-get install python  (NOT 3)
```
- build-essential - Informational list of build-essential packages
- uuid-dev - Universally Unique ID library (headers and static libraries)
- iasl - Intel ASL compiler/decompiler (also provided by acpica-tools)
- git - support for git revision control system
- gcc-5 - GNU C compiler (v5.4.0 as of Ubuntu 16.04 LTS)
- nasm - General-purpose x86 assembler 

```
 bash$ sudo apt-get install qemu
```

- Qemu – Emulation with Intel architecture with UEFI Shell 





# Slide 19
## Create QEMU Run Script
- Create a run-ovmf directory under the home directory
```
 bash$ cd ~/workspace
 bash$ mkdir run-ovmf
 bash$ cd run-ovmf
```

- Create a directory to use as a hard disk image
``` 
 bash$ mkdir hda-contents
```

- Create a Linux shell script to run the QEMU from the run-ovmf directory
```
  bash$ gedit RunQemu.sh


  qemu-system-x86_64 -pflash bios.bin -hda fat:rw:hda-contents -net none     -debugcon file:debug.log -global isa-debugcon.iobase=0x402 
```
- Save and Exit


# Slide 20
## Setup Workshop Material 

# Slide 21
## Workshop Material 

1. Copy the Workshop_Material from  the thumb drive  to $HOME/workspace
- Directory Workshop_Material/FW will be created
   ~/workspace/Workshop_Material/ 
    - Documentation 
    - edk2      
    - SampleCode
	- Presentations


# Slide 22
## BUILD EDK II OVMF  -Getting the Source 
2. From the Docker terminal prompt, Copy the edk2 directory to the docker ~/workspace
```
    bash$ cp -R Workshop_Material/edk2 .
```
- 	From the FW folder, copy and paste folder “~/../edk2” to ~/workspace



# Slide 23
## BUILD EDK II OVMF  -Getting BaseTools
3. From the folder ~/workspace/edk2, Extract the BaseTools.tar.xz to edk2 directory.
```
 bash$ tar -xf BaseTools.tar.xz
```

# Slide 24
## BUILD EDK II OVMF 
- Building the Base Tools

- Run Make from the Docker Terminal prompt
```
 bash$ cd ~/workspace/edk2
 bash$ make –C BaseTools
```
- Run edksetup (note This will need to be done for every new Docker Terminal prompt)
``` 
 bash$ . edksetup.sh
```

# Slide 25
## Build Ovmf Platform

# Slide 26
## BUILD EDK II OVMF 
-Update Target.txt and Build
- Open Virtual Machine Firmware (OVMF)- Build


- Edit the file Conf/target.txt
``` 
 bash$ gedit Conf/target.txt
   #

   ACTIVE_PLATFORM       = OvmfPkg/OvmfPkgX64.dsc
   #. . .
   TARGET_ARCH           = X64
   #. . .
   TOOL_CHAIN_TAG        = GCC5

``` 
- Save and Exit


- Build  from the edk2 directory

``` 
 bash$ build
``` 

# Slide 27
## BUILD EDK II OVMF 
-Inside Terminal

- Finished build 



# Slide 28
## Build EDK II OVMF -Verify Build Succeeded 
- OVMF.fd should be in the Build directory
- For GCC5 with X64, it should be located at
```  
   ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd
```
   
   
# Slide 29
## Invoke QEMU
- Change to run-ovmf directory under the home directory
```
 bash$ cd ~/workspace/run-ovmf
```
- Copy the OVMF.fd BIOS image created from the build to the run-ovmf directory naming it bios.bin
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd bios.bin
```

- Run the RunQemu.sh Linux shell script
```
 bash$ . RunQemu.sh
```


# Slide 30
## UEFI Shell  with QEMU 

# Slide 31
## QEMU boot to UEFI Shell

# Slide 32
## Common Shell Commands for Debugging
- help 
- mm
- mem
- memmap
- drivers
- devices
- devtree
- dh
- Load
- Dmpstore
- stall

- “-b” is the command line parameter for breaking after each page.



# Slide 33

## Shell Help
```
Shell> help –b
```

# Slide 34

## Shell “mm”
```
Shell> mm -? -b
```

Help for “mm” command shows options for different types of memory and I/O that can be modified
	

# Slide 35
## Shell “mm”
```
 Shell> mm  0x06bbb000 


 Shell> mm 0
```

- MM in can display / modify  any location 

- "q” to exit



# Slide 36
## Shell “mem”
```
Shell> mem
```

- Displays the contents of the system or device memory
- without arguments, displays the system memory configuration.


# Slide 37
## Shell “memmap”
```
Shell> memmap
```
- Displays the memory map maintained by the UEFI environment


# Slide 38
## Shell “Drivers”
```
Shell> drivers -b
```

# Slide 39
## Shell “Devices”
```
Shell> devices –b
```
- Displays a list of devices that UEFI drivers manage.


# Slide 40
## Shell “Devtree”
```
Shell> devtree –b
```
- Displays s tree of devices currently managed by UEFI drivers

# Slide 41
## Shell Handle Database - “Dh”
```
Shell> dh –b
```
- Displays the device handles associated with UEFI drivers

# Slide 42
## Shell “Load”
```
Shell> load -?
```

# Slide 43
## Shell “dmpstore”
```
Shell> dmpstore -all –b
```
- Display the contents of the NVRAM variables

# Slide 44
## Shell “Stall”
```
Shell> stall 10000000

```
- Stalls the operation for a specified number of microseconds


# Slide 45
## UEFI SHELL SCRIPTS

- The UEFI Shell can execute commands from a file, which is  called a batch script file (`.nsh` files).

- Benefits: These files allow users to simplify routine or repetitive tasks.

- Perform basic flow control.
- Allow branching and looping in a script.
- Allow users to control input and output and call other batch programs (known as script nesting).

# Slide 46
## WRITING UEFI SHELL SCRIPTS
- At the shell prompt
```
Shell> fs0:
FS0:\> edit HelloScript.nsh 
```

- Type : echo "Hello World"

- Press “F2”
- Enter
- Press “F3” to exit



# Slide 47
## Hello World Script
- In the shell, type HelloScript for the following result:



- Close the QEMU

# Slide 48
## UEFI SHELL NESTED SCRIPTS
- Copy the Scripts from the ~../SampleCode/ShellScripts to the run-ovmf directory  ~/workspace/run-ovmf/hda-contents
```
 bash$ cp ~/workspace/Workshop_Material/SampleCode/ShellScripts ~/workspace/run-ovmf/hda-contents/.
```


# Slide 49
## UEFI Shell Script Example
### Script1.nsh
```
//  # Simple UEFI Shell script file
 echo -off
 script2.nsh
 if exist %cwd%Mytime.log then
      type Mytime.log
 endif
 echo "%HThank you.” “%VByeBye:) %N“
```


### Script2.nsh
```
// # Show nested scripts
 time > Mytime.log
 for %a run (3 1 -1)
    echo %a counting down
 endfor
```


# Slide 50
## Run UEFI Shell Scripts
- Run the RunQemu.sh from the terminal 
```
       	 bash$ cd run-ovmf
    	 bash$ . RunQemu.sh
```
- At the Shell prompt Type  

```
 Shell> fs0:
 FS0:\> Script1

 FS0:\> Edit Script1.nsh
```

# Slide 51
## Run UEFI Shell Scripts
- Remove the “#” on the first line


- Press “F2”
- Enter
- Press “F3” to exit
- Type 

```
 FS0:\> Script1
```

# Slide 52
## Summary
- OVMF Platform Overview 
- Build a EDK II Platform using OVMF package and use QEMU  to boot to UEFI Shell
- Run UEFI Shell Commands  and Scripts



# Slide 53
## Legal Notice

```
No license (express or implied, by estoppel or otherwise) to any intellectual property rights is granted by this document. 
Intel disclaims all express and implied warranties, including without limitation, the implied warranties of merchantability, fitness for a particular purpose, and non-infringement, as well as any warranty arising from course of performance, course of dealing, or usage in trade. 
This document contains information on products, services and/or processes in development.  All information provided here is subject to change without notice.  
The products and services described may contain defects or errors known as errata which may cause deviations from published specifications. Current characterized errata are available on request. 

Intel, the Intel logo are trademarks of Intel Corporation or its subsidiaries in the U.S. and/or other countries.  

*Other names and brands may be claimed as the property of others
 
© Intel Corporation.
```

# Slide 54
- Logo 

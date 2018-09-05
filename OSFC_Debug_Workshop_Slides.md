
# Slide 1
## Debugging Unified Extensible Firmware Interface (UEFI) Firmware under Linux*
- Laurie Jarlstrom laurie.Jarlstrom@intel.com,
- Stephano Cetola Stephano.Cetola@intel.com, 
- Brian Richardson Brian.Richardson@intel.com 
- Intel Corporation
- OSFC - 2018

# Slide 2
## Workshop Objective
- List the ways to debug
- Define EDK II (EFI Development Kit) DebugLib and its attributes
- Introduce the Intel® UEFI Development Kit Debugger  (Intel® UDK Debugger)
- Debugging PI’s phases
- Debug EDK II using Intel® UDK w/ GDB - LAB


# Slide 3
## Debugging UEFI
- Debugging UEFI Firmware on EDK II


# Slide 4
## Debug Methods 
- DEBUG and ASSERT macros in EDK II code 
- DEBUG instead of Print functions 
- Software/hardware debuggers
- Shell commands to test capabilities for simple debugging

# Slide 5
## EDK II DebugLib Library


# Slide 6
## Using PCDs to Configure DebugLib
- MdePkg Debug Library Class

# Slide 7
## The DebugLib Class    	
- ASSERT (Expression)
- DEBUG (Expression)
- ASSERT_EFI_ERROR (StatusParameter)
- ASSERT_PROTOCOL_ALREADY_INSTALLED(…)





- DEBUG_CODE (Expression)
- DEBUG_CODE_BEGIN() & DEBUG_CODE_END()
- DEBUG_CLEAR_MEMORY(…)


# Slide 8
## DebugLib Instances

# Slide 9
## Changing Library Instances

# Slide 10
## UEFI Debugger Overview
- Intel® UEFI Development Kit Debugger Tool


# Slide 11
## Intel® UEFI Development Kit Debugger Tool


# Slide 12
## Host & Target Debug Setup
- Null Modem Cable or
- USB 2.0 Debug Cable or USB 3.0


# Slide 13
## Distribution

# Slide 14
## Host Configuration Requirements


# Slide 15
## Host Configuration Requirements


# Slide 16
## Host Configuration Requirements-GDB


# Slide 17
## Changes to Target Firmware


# Slide 18
## Configure (Target)
- Add Symbolic Debug to platform DSC (Build Switch)
	- -D SOURCE_DEBUG_ENABLE
- Change Debug Agent Library appropriately (SEC | DXE | SMM)
- Configure target to use COM port via PCD
- Ensure COM port not used by other project modules/features
- Simple “ASCII Print” though COM port is allowed


# Slide 19
## Debugging UEFI
- Debugging UEFI Firmware using Intel® UDK w/ GDB

# Slide 20
## Source Level Debug Features

# Slide 21
## Launching UDK Debugger- Linux

# Slide 22
## Launching UDK Debugger- Linux

# Slide 23
## Launching UDK Debugger- Linux

# Slide 24
## Launching UDK Debugger- Linux 

# Slide 25
## UDK Debugger – Setting break points  

# Slide 26
## UDK Debugger UEFI Scripts 
- Info modules 
	- Lists information about the loaded modules or the specified module
- py mmio
	- Access the memory mapped IO space
- py pci
	- Display PCI devic list
- py mtrr
	- Dump the MTRR Setting of the current processor
- py DumpHobs
	- dump contents of the HOB list
- resettarget 


# Slide 27
## Debugging Boot flow
- Debug through the UEFI Firmware Boot Flow

# Slide 28
## Debugging the Boot Phases 

# Slide 29
## Debugging the Boot Phases - SEC

# Slide 30
## Debugging the Boot Phases - PEI 

# Slide 31
## PEI Phase: Trace Each PEIM

# Slide 32
## Check for transition from PEI to DXE

# Slide 33
## Check for transition from DxeIpl to DXE

# Slide 34
## Debugging the Boot Phases - DXE

# Slide 35
## DXE: Trace Each Driver Load

# Slide 36
## Debugging the Boot Phases - BDS
- Detect console devices (input and output)
- Check enumeration of all devices’ preset
- Detect boot policy
- Ensure BIOS “front page” is loaded


# Slide 37
## BDS Phase – Entry Point

# Slide 38
## Debugging the Boot Phases - Pre-Boot

# Slide 39
## Debug in Pre-Boot – UEFI Shell Application

# Slide 40
## Debug in Pre-Boot – UEFI Shell Application

# WORKSHOP Slides 
# Slide 41 
## Debug Workshop
- Steps to setup the GDB & UDK with QEMU to debug UEFI Firmware

# Slide 42 section slide
## Setup OVMFPKG 
- Setup OvmfPkg to build and run with QEMU and Ubuntu


# Slide 43
## Extract Container
- Copy “docker“ directory from usb thumb drive to local hard driver
- Load the edk2-Ubuntu.dockerimage
```
 bash$ docker load –i edk2-Ubuntu.dockerimage
```

- For Open Suse – also set up share
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

# Slide 44
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


# Slide 45
## Workshop Material 
- Copy the Workshop_Material from  the thumb drive  to $HOME/workspace

# Slide 46
## Create QEMU Run Script
1. Create  Directories  for invoking Qemu under the home directory
```
 bash$ cd ~/workspace
 bash$ mkdir run-ovmf
 bash$ cd run-ovmf
 bash$ mkdir hda-contents
```

2. Create a FIFO Pipe used by Qemu and the UDK debugger
```   
    bash$ mkfifo /tmp/serial.in
    bash$ mkfifo /tmp/serial.in
```

3. Create a Linux shell script to run the QEMU from the run-ovmf directory

```
 bash$ gedit RunQemu.sh

  qemu-system-i386 -s  -pflash bios.bin -hda fat:rw:hda-contents -net none\
  -debugcon file:debug.log\
  -global isa-debugcon.iobase=0x402\
  -serial pipe:/tmp/serial 
```

4. Save and Exit

# Slide 47
## BUILD EDK II OVMF  -Getting the Source 
- From the Docker terminal window, Copy the edk2 directory to the docker ~/workspace
```
    bash$ cp -R Workshop_Material/edk2 .
```
- 	From the FW folder, copy and paste folder “~/../edk2” to ~/workspace




# Slide 48
## BUILD EDK II OVMF  -Getting BaseTools
- From the folder ~/workspace/edk2, Extract the BaseTools.tar.xz to edk2 directory.
```
 bash$ tar -xf BaseTools.tar.xz
```

# Slide 49
## BUILD EDK II OVMF 
- Building the Base Tools

- Run Make from the Docker Terminal window
```
 bash$ cd ~/workspace/edk2
 bash$ make –C BaseTools
```

- Run edksetup (note This will need to be done for every new Docker Terminal window)
```
 bash$ . edksetup.sh
```


# Slide 50
## BUILD EDK II OVMF 
-Update Target.txt and Build

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
 bash$ build -D SOURCE_DEBUG_ENABLE
```


# Slide 51
## BUILD EDK II OVMF 
-Inside Terminal

- Finished build 



# Slide 52
## Build EDK II OVMF -Verify Build Succeeded 


# Slide 53
## Invoke QEMU
Change to run-ovmf directory under the home directory
```
 bash$ cd ~/workspace/run-ovmf
```
- Copy the OVMF.fd BIOS image created from the build to the run-ovmf directory naming it bios.bin
```
bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd   bios.bin
```

- Run the RunQemu.sh Linux shell script
```
bash$ . RunQemu.sh
```
- Exit Qemu


# Slide 54
## UDK Debugger
- Update the Configuration for the Intel® UDK Debugger Tool

# Slide 55
## Intel® UDK Debugger Tool
- Configure Debug Port Menu

- Edit Configuration file:  /etc/udkdebugger.conf
```
 bash$ gedit /etc/udkdebugger.conf
```

- Change Channel = Pipe and  Port = /tmp/serial
```
 [Debug Port]
 Channel = Pipe
 Port = /tmp/serial
 FlowControl = 1
 BaudRate = 115200
 Server = 

 [Target System]
```

- Save the file


- Copy the file for successive sessions
```
 bash$ cp /etc/udkdebugger.conf ~/workspace
```

# Slide 56 section slide
## Debug a Driver 
- Build a UEFI Driver and use the Debugger tools to Debug


# Slide 57
## Simple UEFI Driver - MyUefiDriver
- MyUEFIDriver – UEFI Driver Produces:
- Driver Binding Protocol
- Component Name Protocol
- HII forms / Fonts w/ supporting Protocols
- My Dummy Protocol – 
  - Updates NVRAM Variable – Unicode string
  - Updates a Memory buffer – Unicode char

  
- MyApp – UEFI application interfaces with My Dummy Protocol



# Slide 58
## Debugging MyUefiDriver from the UEFI Shell
- MyUefiDriver produces
- Protocol (4) – My dummy protocol	
	- String write to NVRAM
 	- String clear NVRAM
	- Char write memory buffer
	- Char clear memory buffer

- MyApp consumes Protocol (4)

- Use the UEFI Shell for debugging MyUefiDriver

	

# Slide 59
## Copy Simple Driver to Your Workspace
- Open Directory Workshop-Material/SampleCode/UEFI-Driver
```
 bash$ cd ~/workshop/Workshop-Material/SampleCode/UEFI-Driver
```

- Copy the sample driver to the edk2 directories
```
 bash$ cp –R MyUefiDriver  ~/workspace/edk2/
 bash$ cp –R Protocol  ~/workspace/OvmfPkg/Include/
 bash$ cp OvmfPkg.dec  ~/workspace/edk2/OvmfPkg/
 bash$ cp OvmfPkgX64.dsc  ~/workspace/edk2/OvmfPkg/
 bash$ cp –R bin ~/workspace/run-ovmf/hda-contents
```




# Slide 60
## Build UEFI Driver & Test
- Build with Source Debugger
```
 bash$ cd ~/workspace/edk2
 bash$ build -D SOURCE_DEBUG_ENABLE
```
- Change to run-ovmf directory under the home directory
```
 bash$ cd ~/workspace/run-ovmf
```

- Copy the OVMF.fd BIOS image created from the build to the run-ovmf directory naming it bios.bin
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd bios.bin
```
- Copy MyUefiDriver and MyApp to the Qemu file system hda-contents
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyApp.efi hda-contents/
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyUefiDriver.efi hda-contents/
```



# Slide 61
## Test UEFI Driver in Qemu
Run QEMU
```
 bash$ . RunQemu.sh
```
2. Load the UEFI Driver at the shell prompt
```
 Shell> fs0:
 FS0:> Load MyUefiDriver.efi
```

3. Test with Drivers command
```
 FS0:> Drivers
```

-   See “My Uefi Sample Driver” in the list

4. Run the MyApp that calls the protocols
```
 FS0:> MyApp.efi
```




# Slide 62
## Test UEFI Driver in Qemu
```
 FS0:> MyApp.efi H “hello world”
 FS0:> Dmpstore –all –b
```
- Then use Mem on the address found in debug.log
```
 FS0:> Mem 0x07278618
```

# Slide 63
## Debugging with DEBUGLIB
- Check debug.log
```
 bash$ cat debug.log
```
- Notice all the Debug statements from the Supported function and only one from the Start function.
- Notice the Memory buffer location that is created in the start.
- Notice the install of MyDummyProtocol in the Start



# Slide 64
## Debugging with DEBUGLIB
- Check debug.log for PeiMain and DxeMain

  - Notice PeiMain is invoked 3 times
    - Beginning with Temp Memory
    - After memory Initiation
    - Address in System memory

  - Notice DxeCore and entry point for DxeMain 
  - Most of the Initialization is done in DxeCore

  - Make note of addresses to be later used for breakpoints in gdb /udk

- EXIT QEMU

# Slide 65 section slide
## Invoke Debugger
- Invoking Intel® UDK, GDB and QEMU

# Slide 66
## Open 4 Terminal Console Windows
- Open successive terminal windows with:
```
 bash$ docker exec –it edk2 
```
1. Run Intel® UDK Debugger 
2. Run Gdb
3. Run Qemu
4. Check debug.log with cat


# Slide 67
## 1st Terminal window, UDK Debugger
- 1st Terminal window

- Invoke Intel® UDK Debugger

- Open a terminal window in opt/intel/udkdebugger
```
 bash$ cd /opt/intel/udkdebugger
 bash$ ./bin/udk-gdb-server
``` 

# Slide 68
## 2nd Terminal window, GDB
- 2nd Terminal window


- Invoke GDB  (note `gdb --tui` to get layout src) 

```
 bash$ cd /opt/intel/udkdebugger
 bash$ gdb
```


# Slide 69
## 3rd  Terminal window (QEMU)       
- 3rd window

- Invoke Qemu
```
 bash$ . RunQemu.sh 
```

- Notice that the 2nd Terminal window (UDK) will see the Qemu and will print out the command you need to enter in the 3rd Terminal window (gdb)
- Terminal(2) will show "Connection from localhost" message
- Attach to the UDK debugger
- Connect with ‘`target remote <HOST>:1234`’



# Slide 70
## 4th Terminal window
- 4th window
```
 bash$ cd ~/workspace/run-ovmf 
```
- Periodically use `cat debug.log` to check debug output
``` 
 bash$ cat debug.log
```

- OR  Edit source and rebuild in `~/workspace/edk2`


# Slide 71
## 2nd  Terminal window - gdb
- In gdb window, type the following to attach to the UDK debugger
```
 (gdb) target remote <HOST>:1234
```
- This should be the same as in the 2nd Terminal window (UDK) shows.  Note: “<HOST>” should be your Host or VM and 1234 will be the serial pipe port # 

- NOTE: For OpenSUSE use 
```
 (gdb) target remote 127.0.0.1:1234
```

# Slide 72
## 2nd  Terminal window  - gdb
- Now the gdb  Terminal window will be in control of QEMU 
- Open the udk scripts in GDB – Terminal(2)
```
 (gdb) source ./script/udk_gdb_script
```

- Symbols will show for PeiCore, also 
- notice the prompt changes from  "(gdb)" to "(udb)" 

# Slide 73
## 2nd Terminal window -gdb
- At this point the Qemu is waiting because the udk has halted.
- In gdb :

- Set breakpoints (i.e. Address of DxeMain from debug.log)
```
 (udk) b *0x07e9a240
```
- Continue 	
```
 (udk) c
```

- Warning unless a breakpoint is hit there is no way to Halt gdb once “continue” is invoked 

- DO NOT Cntl-Z out of the gdb while Qemu is running or you may have to reload the docker




# Slide 74
## Example: Break at DXE Core
- If a breakpoint was set for DxeMain, Debug could continue to debug DXE / UEFI drivers
 
- Layout  C Source code
```
 (udk) layout src
```
- Step Next Instruction
```
 (udk) next
```
- Show the Modules initialized
```
 (udk) info modules
```

- See gdb cheat sheet pdfs for more Documentation\gdb_UDK_Debugger

- EXIT QEMU if gdb at prompt (udb)


 





# Slide 75
## Exit QEMU gdb “Continuing.”
- Do not Exit Qemu if the gdb is in “Continuing.”
- In invoke the app: 
```
 FS0:> bin\myCpubreak
```

- This will force gdb to break at the and stop running Qemu
- Then Exit Qemu by closing window for QEMU
- DO NOT EXIT gdb


# Slide 76 section slide
## Add CPU Breakpoint 
- Debug the UEFI Driver by adding function call “CpuBreakpoint()” in the code


# Slide 77
## Add CpuBreakpoint() Entry and Start 
- Use 4th Terminal window to edit edk2/MyUefiDriver/MyUefiDriver.c and add CpuBreakpoint(); to the driver’s :
       - Entry point and Start functions

- Entry point - Line 246:
```c

MyUefiDriverDriverEntryPoint (
  // . . .
)
{
  EFI_STATUS                  Status;
  EFI_HII_PACKAGE_LIST_HEADER *PackageListHeader;
  EFI_HII_DATABASE_PROTOCOL   *HiiDatabase;
  EFI_HII_HANDLE              HiiHandle;
  CpuBreakpoint();
  Status = EFI_SUCCESS;

```



- Start function - Line 456:

```c
MyUefiDriverDriverBindingStart (
// . . .)
{
MY_DUMMY_DEVICE_PATH     MyDummyDP;
EFI_DEVICE_PATH_PROTOCOL EndDP;
EFI_DEVICE_PATH_PROTOCOL *Dp1;
EFI_STATUS               Status;
CpuBreakpoint();
```

# Slide 78
## Add CpuBreakpoint() in the UEFI Application 
- Edit edk2/MyUefiDriver/MyApp.c and add CpuBreakpoint(); to the beginning just after the debug print statement.
- Approx.- Line 75:

```c
EFI_STATUS
EFIAPI
MyAppUefiMain (
// . . .
  )
{
//. . .
 DEBUG((EFI_D_INFO, "\n\n>>>>>>[MyApp]Start of MyApp with Entry point at:  0x%08x \n", \
      MyAppUefiMain));
 CpuBreakpoint();
 
 //Initialize local protocol pointer
  EfiShellParametersProtocol = NULL;
``` 

# Slide 79
## Build UEFI Driver & Test
- Build with Source Debugger
```
 bash$ cd ~/workspace/edk2
 bash$ build -D SOURCE_DEBUG_ENABLE
```

- Change to run-ovmf directory under the home directory

```
 bash$ cd ~/workspace/run-ovmf
```

- Copy the OVMF.fd BIOS image created from the build to the run-ovmf directory naming it bios.bin
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd bios.bin
```
 
- Copy MyUefiDriver and MyApp to the Qemu file system had-contents
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyApp.efi hda-contents/.
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyUefiDriver.efi hda-contents/.
```





# Slide 80 
## 4 Terminal Console Windows
- the following windows should already be opened running the debug applications and qemu
```
  #1
 bash$ bin/udk-gdb-server
  #2
 bash$ Gdb
  #3
 bash$ . RunQemu.sh
  #4
 bash$ cat debug.log
``` 


# Slide 81
## 2nd  Terminal - gdb
- In gdb window, type the following to attach to the UDK debugger
```
(gdb) target remote <HOST>:1234
```
- This should be the same as in the 2nd Terminal window (UDK) shows.  Note: “<HOST>” should be your Host or VM and 1234 will be the serial pipe port # 

- NOTE: For OpenSUSE use 
```
(gdb) target remote 127.0.0.1:1234

```


# Slide 82
## 2nd  Terminal window - gdb
- Now the gdb  Terminal window will be in control of QEMU 
- Open the udk scripts in GDB – 
- Terminal(2)
```
 (gdb) source ./script/udk_gdb_script
```

- Notice the prompt changes from "(gdb)" to "(udb)" 

# Slide 83
## Debugging with GDB and UDK
- Continue “c” will boot up to UEFI Shell


# Slide 84
## Debugging with GDB and UDK
- At the UEFI Shell
```
 Shell > fs0:
 FS0: > Load MyUefiDriver.efi
```
 
- Notice that the CpuBreakpoint will stop the QEMU

- Now move to GDB window (2)
- At the (udb) window
```
 (udb) Layout src
 (udb) next
```

# Slide 85
## Debugging with GDB and UDK
- At the (udb) window set a break point at line 580 in the MyUefiDriver.c
```
 (udb) b MyUefiDriver.c:580
```
- Swap between gdb source and gdb command window
```
(udb) tui disable
(udb) layout src
```




# Slide 86
## Debugging with GDB and UDK
- Notice the “b+” added to the source code
- This will set a breakpoint in the MyDummyProtocol for Storing a string 

- Continue to load the driver
```
 (udb) c
```



# Slide 87
## Debugging with GDB and UDK
- The next CpuBreakpoint in the Start function

- Step through the Start function with “next”
```
(udb) next
```
- Note: use cntl-O to repeat the “next” command in (udb)






# Slide 88
## Debugging with GDB and UDK
- Debug in Window 2 (gdb)
- Other commands in the Debugger when a breakpoint is hit:
```
 (udb) info locals
 (udb) info args
 (udb) info modules
 (udb) backtrace 
 (udb) b MyApp.c:147
```
- Check the PDF  docs on gdb and UDK Debugger for other debug commands 









# Slide 89
## Exit QEMU
- Do not Exit Qemu if the gdb is in “Continuing.”
- In invoke the app: 
```
 FS0:> bin\myCpubreak
```
-  This will force gdb to break at the and stop Qemu
- Then Exit Qemu by closing window for QEMU
- DO NOT EXIT gdb



# Slide 90 section slide
## Debug a Real Bug 
- Debug a UEFI Driver with a Real Bug and use the Debugger tools to find the bug


# Slide 91
## Copy Simple Driver to Your Workspace
- Open Directory Workshop-Material/SampleCode/UEFI-Driver
```
 bash$ cd ~/workshop/Workshop-Material/SampleCode/UEFI-Driver02
```

- Copy the sample driver to the edk2 directories
```
 bash$ cp –R MyUefiDriver  ~/workspace/edk2/
```

- Be sure that the Driver gets re-built by deleting the intermediate object files
```
 bash$ rm -R ~/workshop/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyUefiDriver
```



# Slide 92
## Build UEFI Driver & Test
- Build with Source Debugger
```
 bash$ cd ~/workspace/edk2
 bash$ build -D SOURCE_DEBUG_ENABLE
```

- Change to run-ovmf directory under the home directory
```
 bash$ cd ~/workspace/run-ovmf
```
- Copy the OVMF.fd BIOS image created from the build to the run-ovmf directory naming it bios.bin
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd bios.bin
```
- Copy MyUefiDriver and MyApp to the Qemu file system had-contents
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyApp.efi hda-contents/.
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyUefiDriver.efi hda-contents/.
```



# Slide 93
## Build UEFI Driver & Test
- Run QEMU
```
 bash$ . RunQemu.sh
```
- Load the UEFI Driver at the shell prompt

```
 Shell> fs0:
 FS0:> Load MyUefiDriver.efi
```
- Continue “c” in (gdb) when “CpuBreakpoint()” is hit

- Test with the MyApp
```
 FS0:> MyApp H “hello world”
```








# Slide 94
## Add Heap Guard 
- Turn on Heap Guard


# Slide 95
## Check PCD for Heap Guard Enabling
- Open edk2/OvmfPkg/OvmfPkgX64.dsc and scroll to the bottom

```bash

!if $(LAB_HEAPGUARD)  == TRUE
 MyUefiDriver/MyUefiDriver.inf{
 <PcdsFixedAtBuild>
  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPageType|0x01e
  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPoolType|0x01e
  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask|0x03
  gEfiMdeModulePkgTokenSpaceGuid.PcdCpuStackGuard|TRUE
}


 MyUefiDriver/MyApp.inf{
 <PcdsFixedAtBuild>
  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPageType|0x01e
  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPoolType|0x01e
  gEfiMdeModulePkgTokenSpaceGuid.PcdHeapGuardPropertyMask|0x03
  gEfiMdeModulePkgTokenSpaceGuid.PcdCpuStackGuard|TRUE
}

```

# Slide 96
## Build UEFI Driver & Test
- Build with Source Debugger
```
 bash$ cd ~/workspace/edk2
 bash$ build -D SOURCE_DEBUG_ENABLE –D LAB_HEAPGUARD
```

- Change to run-ovmf directory under the home directory
```
 bash$ cd ~/workspace/run-ovmf
```
- Copy the OVMF.fd BIOS image created from the build to the run-ovmf directory naming it bios.bin
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd bios.bin
```
- Copy MyUefiDriver and MyApp to the Qemu file system had-contents
```
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyApp.efi hda-contents/.
 bash$ cp ~/workspace/edk2/Build/OvmfX64/DEBUG_GCC5/X64/MyUefiDriver.efi hda-contents/.
```



# Slide 97
## Build UEFI Driver & Test
- Run QEMU
```
 bash$ . RunQemu.sh
```
- Load the UEFI Driver at the shell prompt

```
 Shell> fs0:
 FS0:> Load MyUefiDriver.efi
```
- Continue “c” in (gdb) when “CpuBreakpoint()” is hit

- Test with the MyApp
```
 FS0:> MyApp H “hello world”
```








# Slide 98
## Summary
- List the ways to debug
- Define EDK II DebugLib and its attributes
- Introduce the Intel® UEFI Development Kit Debugger  (Intel® UDK Debugger)
- Debugging PI’s phases
- Debug EDK II using Intel® UDK w/ GDB - LAB


# Slide 99
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

# Slide 100
  Logo

# Slide 101
## Backup

# Slide 102
## Restarting Docker
Close all docker sessions and open native console/terminal session 

$> docker ps –a
$> docker rm –f edk2
$> xhost local:root

Re-load Docker image

$> docker load –i edk2-ubuntu.dockerimage
$> cd ~/workspace
$> . ~/docker/edk-2-ubuntu.sh

Re-do Pipe and UDK Debugger config

 bash$ mkfifo /tmp/serial.in
 bash$ mkfifo /tmp/serial.out
 bash$ cp udkdebugger.conf /etc/

             Return to Open 4 docker terminal console windows

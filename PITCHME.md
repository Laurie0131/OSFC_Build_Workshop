---?image=/assets/images/slides/Slide1.JPG
@title[Platform Build Lab]
<br><br><br><br><br>
<p style="line-height:80%"> <span class="white"   >Building Open Source Unified Extensible Firmware Interface (UEFI) 
Firmware with EFI Development Kit II (EDK II)</span></p>
<p style="line-height:60%"><span style="font-size:0.6em" ><font color="yellow">
Laurie Jarlstrom laurie.Jarlstrom@intel.com,<br>
Stephano Cetola Stephano.Cetola@intel.com, <br>
Brian Richardson Brian.Richardson@intel.com <br>
Intel Corporation<br></font></span></p>
<br>
<span style="font-size:0.9em" >OSFC - 2018</span><br>
<span style="font-size:0.5em" >Intel® Corporation –© 2018</span>

Note:
  PITCHME.md for OFSF BUILD WORKSHOP

  Copyright (c) 2018, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.




---?image=assets/images/sectionslide.jpg
@title[Workshop Objective]
<BR>
### <p align="center"<span class="gold"   >Workshop Objective </span></p><br>

<!---  Add bullets using https://fontawesome.com/cheatsheet certificate
-->

 @fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Open Virtual Machine Firmware (OVMF) Platform Overview </span><br><br>
 @fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Build a EDK II Platform using OVMF package and use QEMU  to boot to UEFI Shell</span><br><br>
 @fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Run UEFI Shell Commands  and Scripts</span> <br>
 
---?image=assets/images/sectionslide.jpg
@title[What is OVMF Section]
<br><br><br><br><br>
## <span class="white"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;What is OVMF</span>
<span style="font-size:0.9em" > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="yellow">Open Virtual Machine Firmware for UEFI</font></span>


---?image=/assets/images/slides/Slide4.JPG
@title[Web Tianocore.org]
<p align="right"><span style="font-size:1.0em" > &nbsp;&nbsp;&nbsp;Where? <a href='http://www.tianocore.org'>Tianocore.org</a></span></p>

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p style="line-height:50%"><span style="font-size:0.5em" >Platforms on tianocore.org :
<a href='https://github.com/tianocore/tianocore.github.io/wiki/Nt32Pkg'>Nt32</a>, 
<a href='https://github.com/tianocore/tianocore.github.io/wiki/OvmfPkg'>OVMF</a>, 
<a href='https://github.com/tianocore/edk2/tree/master/ArmVirtPkg'>ArmVirt</a>, 
<a href='https://github.com/tianocore/tianocore.github.io/wiki/MdePkg'>MdePkg</a>, 
<a href='https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Platforms'>HW Platforms</a>, 
<a href='https://github.com/tianocore/tianocore.github.io/wiki/MinnowBoardMax'>Max/Turbot</a>, 
<a href='https://github.com/tianocore/tianocore.github.io/wiki/MinnowBoard-3'>MinnowBoard 3</a> and
<a href='https://github.com/tianocore/tianocore.github.io/wiki/Galileo'>Intel® Galileo</a>
</span>	</p>


Note:

---?image=/assets/images/slides/Slide5.JPG
<!-- .slide: data-transition="none" -->		  
@title[Projects github tianocore]
<br>
<p style="line-height:80%"><span style="font-size:1.1em" >Projects<br>
@fa[github gp-bullet-gold]&nbsp;</span><span style="font-size:.80em" ><b>GitHub</b>&nbsp;&nbsp;
<a href='https://github.com/tianocore'>tianocore.org</a></span></p>

<div class="left1">
<p style="line-height:80%"><span style="font-size:.80em" ><a href='https://github.com/tianocore/edk2'>edk2</a> -
Platforme on edk2- <br>"<b>CORE</b>"</span></p>
<p style="line-height:50%"><span style="font-size:.50em" > 
    BeagleBoardPkg <br>
	Coreboot…Pkg<br>
	DuetPkg<br>
	Nt32Pkg<br>
	OvmfPkg<br>
	QuarkPlatformPkg<br><br>
See Readme.md files
</span></p>

</div>
<div class="right1">
<span style="font-size:0.5em" ></span>
</div>
Note:

---?image=/assets/images/slides/Slide6.JPG
@title[Open Virtual Machine Firmware  ]
<p align="right"><span class="white" >&nbsp;&nbsp;&nbsp;Open Virtual Machine Firmware (OVMF) </span></p>
<br>
<div class="left1">
- <span style="font-size:.70em" >Uses EDK II to support firmware in the OvmfPkg Platform Package</span>
- <span style="font-size:.70em" >Supports UEFI:  Helps develop/<br>debug drivers & applications </span>
- <span style="font-size:.70em" >QEMU VM; emulates IA32 (x86)/<br>X64 (x86-64) based system  </span>
- <span style="font-size:.70em" >Exit condition &rarr; UEFI Shell </span>
- <span style="font-size:.70em" >Tool Chain/OS Support </span>
- <span style="font-size:.70em" >Information <a href='https://github.com/tianocore/tianocore.github.io/wiki/OvmfPkg'>OVMF wiki </a>,<br>  Tianocore.org </span>
</div>
<div class="right1">
<span style="font-size:0.5em" ></span>
</div>

Note:
- Support firmware for VM using EDK II
- EDK II Package Directory – OvmfPkg
- Enable support for UEFI within VM to help develop/debug UEFI drivers & applications
- QEMU1 VM supported to emulate IA32 (x86) or X64 (x86-64) based system  
- OVMF is a sample platform for how VM firmware can be built with EDK II to boot EFI/UEFI Shell & OS in the VM

- 1 QEMU - Open source processor emulator virtual machine using dynamic translation to achieve good emulation speed 


- Tool chain support
- Microsoft Visual Studio*, WINDDK*, Intel ‘C’ Compiler (ICC), GCC Linux and GCC Windows (under CYGWIN*)
- OVMF also requires an ASL compiler to be installed on the system. Intel ASL is available from http://www.acpica.org. 
- More Information available at TianoCore.org

---?image=/assets/images/slides/Slide7.JPG
@title[OVMF BIOS w/ QEMU ]
<br>
<p align="right" style="line-height:70%"><span class="white" >OVMF BIOS w/ QEMU</span><br><span style="font-size:0.7em" >Boots to UEFI Shell</span></p>

Note:

---?image=/assets/images/slides/Slide8.JPG
@title[OVMF w/ QEMU Boot Options]
<p align="right"><span class="white" >OVMF with QEMU Boot Options</span></p>
<br>
<p style="line-height:70%"><span style="font-size:0.7em" > Possibilities to test  OS installers,  UEFI boot loaders and unique, dependent guest OS features.</span></p>

Note:


---?image=/assets/images/slides/Slide9.JPG
@title[OVMF w/ QEMU Test RAM Disk]
<p align="right"><span class="white" >OVMF with QEMU Test RAM Disk</span></p>
<br>
<p style="line-height:70%"><span style="font-size:0.7em" > Create a  RAM disk, <br>either raw or from a file</span></p>

Note:


---?image=/assets/images/slides/Slide10.JPG
@title[OVMF w/ QEMU Test Secure Boot]
<p align="right"><span class="white" >OVMF with QEMU Test Secure Boot</span></p>
<br>
<div class="left1">
<p style="line-height:70%"><span style="font-size:0.7em" > Development and testing of Secure Boot-related features in guest operating systems</span></p>
<p style="line-height:70%"><span style="font-size:0.7em" > Enable the Build switch SECURE_BOOT_ENABLE</span></p>
<p style="line-height:70%"><span style="font-size:0.7em" > Uses OpenSsl Libraries</span></p>
</div>
<div class="right1">
</div>
Note:


---?image=/assets/images/slides/Slide11.JPG
@title[OVMF w/ QEMU boot to UEFI Shell]
<p align="right"><span class="white" >OVMF with QEMU boot to UEFI Shell</span></p>
<br>
<div class="left1">
<p style="line-height:70%"><span style="font-size:0.8em" > OVMF will Boot to the Internal UEFI Shell Application by default</span></p>
<p style="line-height:70%"><span style="font-size:0.5em" > The UEFI Shell is an extensive & Standardized  Pre-OS UEFI Application</span></p>
</div>
<div class="right1">
</div>
Note:

---?image=/assets/images/slides/Slide12.JPG
@title[UEFI – PI & EDK II Boot Flow]
<p align="right"><span class="white" >UEFI – PI & EDK II Boot Flow</span></p>


Note:


---?image=/assets/images/slides/Slide13.JPG
@title[UEFI Shell Elements]
<p align="right"><span class="white" >UEFI Shell Elements</span></p>
<p style="line-height:80%"><span style="font-size:0.7em" >The UEFI Shell is an extensive & Standardized  Pre-OS UEFI Application </span></p>


Note:

---?image=/assets/images/slides/Slide14.JPG
@title[UEFI Shell Usage]
<p align="right"><span class="white" >UEFI Shell Usage</span></p>

Notes:


 
---?image=assets/images/sectionslide.jpg
@title[Build OvmfPkg Section]
<br><br><br><br><br>
## <span class="white"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Build OvmfPkg</span>
<span style="font-size:0.9em" > &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="yellow">Setup OvmfPkg to build and run w/ QEMU* and Ubuntu*</font></span>


---?image=/assets/images/slides/Slide16.JPG
@title[Extract Container]
<br>
### <p align="right"><span class="white" >Extract Container</span></p>
<p style="line-height:80%"><span style="font-size:0.7em" >Copy “docker“ directory from usb thumb drive to local hard driver</span></p>


<p style="line-height:80%"><span style="font-size:0.7em" >Load the edk2-Ubuntu.dockerimage</span></p>
```
bash$ docker load –i edk2-Ubuntu.dockerimage
```

<p style="line-height:80%"><span style="font-size:0.7em" >For OpenSuse – also set up share</span></p>
```
bash$ xhost local:root
```

<p style="line-height:80%"><span style="font-size:0.7em" >Create a work directory </span></p>
```
bash$ mkdir workspace
bash$ cd workspace
```

<p style="line-height:80%"><span style="font-size:0.7em" >Docker run command  from the docker directory</span></p>
```
bash$ . ~/docker/edk2-ubuntu.sh
```

Note:

---
@title[Extract Container 02]
### <p align="right"><span class="white" >Extract Container</span></p>
<p style="line-height:80%"><span style="font-size:0.7em" >From this point on the terminal window for Ubuntu 16.04 will be available and $HOME/workspace will be the shared directory between the host and the Docker container <BR>
window will look like: </span></p>
```
[edk2-ubuntu] workspace #
```


<span style="font-size:0.7em" >Open Multiple terminal windows run the script OpenEdk2Window.sh </span>

```
bash$ docker exec –it edk2 bash
```


Note:

---?image=/assets/images/slides/Slide18.JPG
@title[Pre-requisites Ubuntu 16.04 ]
### <p align="right"><span class="gold" >Pre-requisites Ubuntu 16.04 </span></p>

Note:


---
@title[Create QEMU Run Script]
<p align="right"><span class="white" >Create QEMU Run Script</span></p>
<p style="line-height:80%"><span style="font-size:0.7em" >1. Create a run-ovmf directory under the home directory</span></p>

```
 bash$ cd ~/workspace
 bash$ mkdir run-ovmf
 bash$ cd run-ovmf

```

<p style="line-height:80%"><span style="font-size:0.7em" >2. Create a directory to use as a hard disk image </span></p>

```
 bash$ mkdir hda-contents

```

<p style="line-height:80%"><span style="font-size:0.7em" >3. Create a Linux shell script to run the QEMU from the run-ovmf directory</span></p>

```
 bash$ gedit RunQemu.sh

 qemu-system-x86_64 -pflash bios.bin -hda fat:rw:hda-contents -net none     -debugcon file:debug.log -global isa-debugcon.iobase=0x402 

```



<p style="line-height:80%"><span style="font-size:0.7em" >4. Save and Exit </span></p><br>

<p style="line-height:50%"><span style="font-size:0.5em" >example scripts  See: ~/workshop-material/SampleCode/Qemu/RunQemuX64.sh </span></p>

Note:



---  
@title[Summary]
<BR>
### <p align="center"><span class="white"   >Summary </span></p><br>


 @fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Open Virtual Machine Firmware (OVMF) Platform Overview </span><br><br>
 @fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Build a EDK II Platform using OVMF package and use QEMU  to boot to UEFI Shell</span><br><br>
 @fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Run UEFI Shell Commands  and Scripts</span> <br>
 

 

---?image=assets/images/gitpitch-audience.jpg
@title[Questions]
<br>
![Questions](/assets/images/questions.JPG =10x) 



---
@title[Acknowledgements]
#### <p align="center"><span class="white"   >Legal Notice</span></p>

```c++
/**
No license (express or implied, by estoppel or otherwise) to any intellectual property rights is 
granted by this document. 
Intel disclaims all express and implied warranties, including without limitation, the implied warranties of 
merchantability, fitness for a particular purpose, and non-infringement, as well as any warranty arising from course of 
performance, course of dealing, or usage in trade. 

This document contains information on products, services and/or processes in development.  All information provided 
here is subject to change without notice.  
The products and services described may contain defects or errors known as errata which may cause deviations from 
published specifications. Current characterized errata are available on request. 

Intel, the Intel logo are trademarks of Intel Corporation or its subsidiaries in the U.S. and/or other countries.  

*Other names and brands may be claimed as the property of others
 
© Intel Corporation.

Copyright (c) 2018, Intel Corporation. All rights reserved.
**/

```

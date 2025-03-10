## Slide 1  EDK II Debugging]
<br><br><br>

## UEFI & EDK II Training

#### EDK II Debugging w/ Windows Lab

<br>

<a href='http://www.tianocore.org'>tianocore.org</a>

<!---
Note:

  LabGuid.md for UEFI / EDK II Training  EDK II Debugging Pres-lab

  Copyright (c) 2021, Intel Corporation. All rights reserved.<BR>

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

<!---  
-->

---

## Slide 2  Lesson Objective
<BR>

### Lesson Objective <br>



- Using PCDs to Configure DebugLib - LAB
- Change the DebugLib instance to modify the debug
        output - LAB
- Debug EDK II using VS Debugger - LAB


---
## Slide 3 Lab 1: Adding Debug Statements

In this lab, you’ll add debug statements to the previous lab's SampleApp UEFI Shell application


Note:
In this lab, you'll learn how to add debug statements.  
This lab uses code from a previous exercise as a starting point (refer to  Writing Simple UEFI Applications).  Before proceeding, verify that the SampleApp code is present in your workspace and that the code references the OvmfPkgX64.dsc file.

---
## Slide 4 Lab 1: Catch Up SampleApp

### <b>Lab 1: Catch up from previous lab</b>

Skip to next slide if Lab Writing UEFI App Lab</a> completed - <a href="https://github.com/tianocore-training/Presentation_FW/blob/main/FW/Presentations/Lab_Guides/_C_03_Writing_UEFI_App_WIN_LabGuide.md"> Labguide </a> <BR>

- Perform Lab Setup from previous Labs  <a href="https://github.com/tianocore-training/Presentation_FW/blob/main/FW/Presentations/Lab_Guides/_C_01_Platform_Build_Win_Emulator_Lab_guide.md">LabGuide</a>  
- Create a Directory under the workspace `C:/FW/edk2-ws/edk2 : "SampleApp"`
- Copy contents of `C:/../FW/LabSampleCode/SampleAppDebug to C:/FW/edk2-ws/edk2/SampleApp`
- Open `C:/FW/edk2-ws/edk2/EmulatorPkg/EmulatorPkg.dsc`
- Add the following to the `[Components]` section: 

```
 # Add new modules here
SampleApp/SampleApp.inf
```
<br>
- Save and close the file `C:/FW/edk2-ws/edk2/EmulatorPkg/EmulatorPkg.dsc`



---
## Slide 5 Lab 1: Add debug statements SampleApp

Open a VS  Command Prompt and type: cd C:/FW/edk2-ws then
```
    C:/FW/edk2-ws > setenv.bat
    C:/FW/edk2-ws > cd edk2 
    C:/FW/edk2-ws/edk2 > edksetup
```
Open C:/FW/edk2-ws/edk2/SampleApp/SampleApp.c

Add the following to the include statements at the top of the file after below the last "include" statement:
```
	#include <Library/DebugLib.h>
```



---
## Slide 6 Lab 1: Add debug statements SampleApp 02]
### <b>Lab 1: Add debug statements to SampleApp</b>
- Locate the `UefiMain` function. Then copy and paste the following 
code after the &nbsp;"`EFI_INPUT_KEY  KEY;`" statement: and before the first &nbsp;`Print()` statement 


```c
DEBUG ((0xffffffff, "\n\nUEFI Base Training DEBUG DEMO\n") );
DEBUG ((0xffffffff, "0xffffffff USING DEBUG ALL Mask Bits Set\n") );

DEBUG ((DEBUG_INIT,     " 0x%08x USING DEBUG DEBUG_INIT\n" , (UINTN)(DEBUG_INIT))  );
DEBUG ((DEBUG_WARN,     " 0x%08x USING DEBUG DEBUG_WARN\n", (UINTN)(DEBUG_WARN))  );
DEBUG ((DEBUG_LOAD,     " 0x%08x USING DEBUG DEBUG_LOAD\n", (UINTN)(DEBUG_LOAD))  );
DEBUG ((DEBUG_FS,       " 0x%08x USING DEBUG DEBUG_FS\n", (UINTN)(DEBUG_FS))  );
DEBUG ((DEBUG_POOL,     " 0x%08x USING DEBUG DEBUG_POOL\n", (UINTN)(DEBUG_POOL))  );
DEBUG ((DEBUG_PAGE,     " 0x%08x USING DEBUG DEBUG_PAGE\n", (UINTN)(DEBUG_PAGE))  );
DEBUG ((DEBUG_INFO,     " 0x%08x USING DEBUG DEBUG_INFO\n", (UINTN)(DEBUG_INFO))  );
DEBUG ((DEBUG_DISPATCH, " 0x%08x USING DEBUG DEBUG_DISPATCH\n",(UINTN)(DEBUG_DISPATCH)));
DEBUG ((DEBUG_VARIABLE, " 0x%08x USING DEBUG DEBUG_VARIABLE\n",(UINTN)(DEBUG_VARIABLE)));
DEBUG ((DEBUG_BM,       " 0x%08x USING DEBUG DEBUG_BM\n", (UINTN)(DEBUG_BM))  );
DEBUG ((DEBUG_BLKIO,    " 0x%08x USING DEBUG DEBUG_BLKIO\n", (UINTN)(DEBUG_BLKIO))  );
DEBUG ((DEBUG_NET,      " 0x%08x USING DEBUG DEBUG_NET\n", (UINTN)(DEBUG_NET))  );
DEBUG ((DEBUG_UNDI,     " 0x%08x USING DEBUG DEBUG_UNDI\n", (UINTN)(DEBUG_UNDI))  );
DEBUG ((DEBUG_LOADFILE, " 0x%08x USING DEBUG DEBUG_LOADFILE\n",(UINTN)(DEBUG_LOADFILE)));
DEBUG ((DEBUG_EVENT,    " 0x%08x USING DEBUG DEBUG_EVENT\n", (UINTN)(DEBUG_EVENT))  );
DEBUG ((DEBUG_GCD,      " 0x%08x USING DEBUG DEBUG_GCD\n", (UINTN)(DEBUG_EVENT))  );
DEBUG ((DEBUG_CACHE,    " 0x%08x USING DEBUG DEBUG_CACHE\n", (UINTN)(DEBUG_EVENT))  );
DEBUG ((DEBUG_VERBOSE,  " 0x%08x USING DEBUG DEBUG_VERBOSE\n", (UINTN)(DEBUG_EVENT))  );
DEBUG ((DEBUG_ERROR,    " 0x%08x USING DEBUG DEBUG_ERROR\n", (UINTN)(DEBUG_ERROR))  );

```



---
## Slide 7 Lab 1: Build,Run and Test Result 
### <b>Lab 1: Build, Run and Test Result</b>

At the VS Command Prompt
```
   C:/FW/edk2-ws/edk2> Build
   C:/FW/edk2-ws/edk2> RunEmulator
```
Run the application from the shell
```
   Shell>  SampleApp 
```
Check the VS Debug output
Exit

```
   Shell>  Reset 
```

Note:

Notice the changes in DEBUG output for SampleApp in the Visual Studio Command Prompt.  Since the new PCD definitions were only applied to SampleApp, the DEBUG output properties are not changed for other parts of the Emulator project.
At the VS Command Prompt

---
## Slide 8 Lab 2: Changing PCD Value
<br>

In this lab, you’ll learn how to use PCD values to change debugging capabilities

<br>
Note:

In this lab, you'll learn how to use PCD values to change debugging capabilities.  The previous lab,  Adding Debug Statements, did not display all the DEBUG messages added to SampleApp.c.  This lab shows how to change this behavior.




---
## Slide 9  Lab 2: Change PCDs for SampleApp
### <b>Lab 2: Change PCDs for SampleApp</b>

Open  `C:/FW/edk2-ws/edk2/EmulatorPkg/EmulatorPkg.dsc`

Replace `SampleApp/SampleApp.inf` with the following:
```
SampleApp/SampleApp.inf {
   <PcdsFixedAtBuild>
    gEfiMdePkgTokenSpaceGuid.PcdDebugPropertyMask|0xff
    gEfiMdePkgTokenSpaceGuid.PcdDebugPrintErrorLevel|0xffffffff
 }
```
Save and close `EmulatorPkg.dsc`


Note:

---
## Slide 10 Lab 2: Build,Run and Test Result 
### <b>Lab 2: Build, Run and Test Result</b>

Notice the changes in DEBUG output for SampleApp in the Visual Studio Command Prompt.  Since the new PCD definitions were only applied to SampleApp, the DEBUG output properties are not changed for other parts of the  Emulator project.

At the VS Command Prompt
```
   C:/FW/edk2-ws/edk2> Build
   C:/FW/edk2-ws/edk2> RunEmulator
```
Run the application from the shell
```
   Shell>  SampleApp 
```
Check the VS Debug output

Exit

```
   Shell>  Reset 
```



---
## Slide 11 Lab 3: Library Instances for Debugging


In this lab, you’ll learn how to add specific debug library instances

Note:

---
## Slide 12 Lab 3: Using Library Instances for Debugging
### <b>Lab 3: Using Library Instances for Debugging</b>

- Open C:/FW/edk2-ws/edk2/EmulatorPkg/EmulatorPkg.dsc
- Replace SampleApp/SampleApp.inf { . . .} with the following:

```
SampleApp/SampleApp.inf {
   <LibraryClasses>
    DebugLib|MdePkg/Library/UefiDebugLibConOut/UefiDebugLibConOut.inf
 }
```
- Save and close EmulatorPkgPkg.dsc



---
## Slide 13 Lab 3: Build, Run and Test Result]
### <b>Lab 3: Build, Run and Test Result</b>

-At the VS Command Prompt
```
   C:/FW/edk2-ws/edk2> Build
   C:/FW/edk2-ws/edk2> RunEmulator 
```
- Run the application from the shell
```
Shell> SampleApp
```
- See that the output from the Debug 
statements now goes to the console 
- Exit 
```
Shell> Reset
```
Note:

Notice the Debug messages output to the console 



---

## Slide 14 Lab 4: Serial port Instance of DebugLib

### <b>Lab 4: Null Instance of `DebugLib`</b>
<br>
In this lab,  you'll change the `DebugLib` to the Null instance. 

Note:

The DEBUG output for SampleApp is no debug output


---
## Slide 15 Lab 4: Using Null Library Instances
### <b>Lab 4: Using Null Library Instances</b>
<br>


- C:/FW/edk2-ws/edk2/EmulatorPkg/EmulatorPkg.dsc
- Replace `SampleApp/SampleApp.inf { . . .}`with the following: <br>

```c
  SampleApp/SampleApp.inf {
   <LibraryClasses>      
      DebugLib|MdePkg/Library/BaseDebugLibNull/BaseDebugLibNull.inf
 }
```
-Save and close `C:/FW/edk2-ws/edk2/EmulatorPkg/EmulatorPkg.dsc` 

---
## Slide 16 Lab 4: Build, Run and Test Result]
### <b>Lab 4: Build, Run and Test Result</b>



-At the VS Command Prompt
```
   C:/FW/edk2-ws/edk2> Build
   C:/FW/edk2-ws/edk2> RunEmulator 
```
- Run the application from the shell
```
Shell> SampleApp
```
- Check – now NO Debug output

Exit 
```
  Shell> Reset
```


Note:
Notice NO Debug messages output to the console or cmd Prompt



---

## Slide 17 Lab 5: Debugging EDK II with VS Debugger]
<br>

### <b>Lab 5: Debugging EDK II with VS Debugger</b>
<br>

In this lab,  you'll learn how setup the VS to debug the EDK II  emulation

First make sure you have "Just-in-Time" Debugging enabled in the Visual Studio Application <a href="https://docs.microsoft.com/en-us/visualstudio/debugger/debug-using-the-just-in-time-debugger?view=vs-2019#BKMK_Enabling">
 Link</a>
 

---
## Slide 18 Lab 5: Emulator Debug with VS]
### <b>Lab 5:  Debug with VS</b> 
<br>
- Edit the `SampleApp.c`and add the "`ASSERT_EFI_ERROR`" Statement : <br>

```c
    EFI_STATUS      Status;
 	 Status = EFI_NO_RESPONSE;  // or any other EFI Error 
```

Then copy and paste the assert statement just after the first 2 DEBUG statements
    
```
    ASSERT_EFI_ERROR(Status);

```
<br>

- Save `SampleApp.c` <br>

---

## Slide 19 Lab 5: Emulator Debug with VS - ASSERT ]
### <b>Lab 5: Debug with VS - ASSERT  </b>

1. First make sure you have "Just-in-Time" Debugging enabled in the Visual Studio Application <a href="https://docs.microsoft.com/en-us/visualstudio/debugger/debug-using-the-just-in-time-debugger?view=vs-2019#BKMK_Enabling">Link</a> (note: need to open as Admin)
  -  Select Managed, Native and Script
2. Use the Regedt32 to add the "Auto" key: See Slide 32
3. Next Open the Visual Studio Application


---

## Slide 20 Lab 5: Emulator Debug with VS - ASSERT ]
### <b>Lab 5: Debug with VS - ASSERT  </b>

-At the VS Command Prompt
```
   C:/FW/edk2-ws/edk2> Build
   C:/FW/edk2-ws/edk2> RunEmulator 
```

- Inside the Visual Studio app, Enable the Winhost.exe for Debugging
  - Select "Debug" > "Attach to "Process" > find "Winhost.exe"
  - Click "Attach"
---

## Slide 21 Lab 5: Emulator Debug with VS - ASSERT ]
### <b>Lab 5: Debug with VS - ASSERT  </b>


- Run the application from the shell
```
Shell> SampleApp
```
- Assert in VS Command Prompt


Note:

Notice the Assert will have the line number and error code where the assert occured.

---

## Slide 22 Lab 5: Debug with VS ASSERT 02
### <b>Lab 5: Debug with VS - ASSERT  </b>

- Windows* VS Debugger

1. Select "Break"
2.  press "F10" about 2-3 times
3. SampleApp.c can be debugged at this point 

- continue
- "F5" to continue
- "Shift F5" to Stop debugging

Note:
- Notice the debugger will break inside a function called "`CpuBreakpoint()`", press "F10" a few times to step over
- The Visual Studio Debugger will then step into your SampleApp File.
- At this point you can continue debugging or select F5 to go or Shift F5 to exit.
- Upon exiting you can choose to save the solution file or not save it.


---


## Slide 23 Lab 5: Debug with VS- CPU bp
### <b>Lab 5: Debug with VS - `CpuBreakpoint`</b>

<br>
- Edit the `SampleApp.c` and add the `CpuBreakpoint();` Statement and comment out the "`ASSERT` statement": 

```c
    CpuBreakpoint();
```
<br>

- Save `SampleApp.c`


---

## Slide 24 Lab 5:  Debug with VS - CPU bp 02
### <b>Lab 5: Debug with VS - `CpuBreakpoint`</b>


-At the VS Command Prompt
```
   C:/FW/edk2-ws/edk2> Build
   C:/FW/edk2-ws/edk2> RunEmulator 
```

- Inside the Visual Studio App, Enable the Winhost.exe for Debugging.
  - "Cnt-Alt-p" then select "Winhost.exe" 



- Run the application from the shell
```
Shell> SampleApp
```
- VS Debugger pops up, select "Break"
-  press "F10" about 2-3 times until SampleApp.c shows

- SampleApp.c can be debugged at this point 


Note:


---

## Slide 25 Invoke Windows Visual Studio Debugger 02]
### <b>Invoke Windows Visual Studio Debugger</b>

Note:
Now the visual studio debugger is debugging the sampleapp function and common debug tasks can be done:
- stepping 
- checking local variables
- checking the call stack.
- etc.



---

## Slide 26 Lab 6: Debugging EDK II add Debug to Boot Flow
<br>

### <b>Lab 6: Debugging EDK II add Debug to Boot Flow</b>
<br>

In this lab, you’ll learn how add Debug statements to the EDK II Boot flow and check the debug log output



---

## Slide 27 Lab 6: Debug Boot Flow

### Lab 6: Debug Boot Flow

Edit the MdeModulePkg/Core/Pei/PeiMain/PeiMain.c and add a “DEBUG”  print ~line 489 before the call to the PeiDispatcher:
```
	DEBUG((DEBUG_INFO, "***********Before call to Pei Dispatcher ********\n"));
```


Save PeiMain.c


---

## Slide 28 Lab 6: Build, Run and Test Result 


At the VS Command Prompt
```
$> Build
$> RunEmulator.bat
```

Check the VS Debug output
```
Loading PEIM at 0x227A1DC0000 EntryPoint=0x227A1DC1078 PeiCore.efi
Reinstall PPI: 8C8CE578-8A3D-4F1C-9935-896185C32DD3
Reinstall PPI: 5473C07A-3DCB-4DCA-BD6F-1E9689E7349A
Reinstall PPI: B9E0ABFE-5979-4914-977F-6DEE78C278A6
Install PPI: F894643D-C449-42D1-8EA8-85BDD8C65BDE
***********Before call to Pei Dispatcher ********
Loading PEIM 9B3ADA4F-AE56-4C24-8DEA-F03B7558AE50
```

Exit
``` 
Shell> Reset
```

---  
## Slide  29 Summary

### Summary 

- Using PCDs to Configure DebugLib - LAB
- Change the DebugLib instance to modify the debug
        output - LAB
- Debug EDK II using VS Debugger - LAB


---
## Slide 30 Questions
<br>

---
## Slide 31 return to main
### <b>Return to Main Training Page</b>
<br>
<br>
Return to Training Table of contents for next presentation <a href="https://github.com/tianocore-training/Tianocore_Training_Contents/wiki#schedule--outline">link</a>

---
## Slide 32 Logo Slide]



---
## Slide 33 Acknowledgements
#### Acknowledgements

```c++
/**
Redistribution and use in source (original document form) and 'compiled' forms (converted
to PDF, epub, HTML and other formats) with or without modification, are permitted provided
that the following conditions are met:

Redistributions of source code (original document form) must retain the above copyright 
notice, this list of conditions and the following disclaimer as the first lines of this 
file unmodified.

Redistributions in compiled form (transformed to other DTDs, converted to PDF, epub, HTML
and other formats) must reproduce the above copyright notice, this list of conditions and 
the following disclaimer in the documentation and/or other materials provided with the 
distribution.

THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR IMPLIED 
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND 
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL TIANOCORE PROJECT BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES 
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, 
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF ADVISED OF THE POSSIBILITY 
OF SUCH DAMAGE.

Copyright (c) 2021, Intel Corporation. All rights reserved.
**/

```


---
## Slide 34 Backup Section


---
## Slide 35 Issue: Debugging in Emulation with Windows 7 and VS
### Issue:<br>

Debugging in  Emulator with Windows 7/10 64Bit <br>and Visual Studio does not work?


- Symptom:  With Windows 7/10 a CpuBreakpoint() or ASSERT  just exits . 


- Link to fix this issue: 
https://github.com/tianocore/tianocore.github.io/wiki/NT32#Debugging_in_Nt32_Emulation_with_Windows_7_and_Visual_Studio_does_not_work

1. Run the RegEdt32
2. Navigate to the HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug
3. Add a string value entry called "Auto" with a value of "1"



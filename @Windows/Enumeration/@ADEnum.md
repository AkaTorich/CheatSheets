### Domain Enumeration

###### PowerView module 
`. .\PowerView.ps1`
##### ActiveDirectory module 
`Import-Module .\Microsoft.ActiveDirectory.Management.dll`
`Import-Module .\Microsoft.ActiveDirectory.Management.psd1`

###### Get current domain (PowerView)
`Get-NetDomain`
`Get-NetDomain -Domain powershell.local`
###### Get the current domain SID
`Get-DomainSID`
##### Using ActiveDirectory module
`Get-ADDomain`
`Get-ADDomain -Identity powershell.local`
`(Get-ADDomain).DomainSID.Value`
###### Get domain  controller for domain
`Get-NetDomainController`
`Get-NetDomainController -Domain powershell.local`
##### Using ActiveDirectory module
`Get-ADDomainController`
`Get-ADDomainController -Discover -DomainName powershell.local`
###### Get user of domain 
`Get-NetUser`
`Get-NetUser -Domain powershell.local`
`Get-NetUser -UserName labuser`
##### Using ActiveDirectory module
`Get-ADUser -Filter * -Properties *`
`Get-ADUser -Server ps-dc.powershell.local`
`Get-ADUser -Identify labuser`
###### Get groups of domain 
`Get-NetGroup`
`Get-NetGroup *admin*`
##### Using ActiveDirectory module
`Get-ADGroup -Filter * | select Name`
`Get-ADGroup -Filter {Name -like "*admin*"} | select Name`
###### Get all members of the Domain Admins group 
`Get-NetGroupMember -GroupName "Domain Admins"`
##### Using ActiveDirectory module
`Get-ADGroupMember -Identity "Domain Admins" -Recursive`
###### Get groups membership of user 
`Get-NetGroup -UserName "labuser"`
##### Using ActiveDirectory module
`Get-ADGroup -Filter * | select Name`
`Get-ADPrincipalGroupMembership -Identity labuser`
###### Get all computers of the domain 
`Get-NetComputer`
`Get-NetComputer -FullData`
##### Using ActiveDirectory module
`Get-ADComputer -Filter * | select Name`
`Get-ADComputer -Filter * -Properties *`
###### Find all machines of the current domain where the currrent user has local admin access
`Find-LocalAdminAccess -Verbose`
##### Find local admins on all machines of the domain
`Invoke-EnumerateLocalAdmin -Verbose`
###### List Sessions on a particular computer
`Get-NetSession -ComputerName ops-dc`
##### Find computers where a domain admin is logged in and current user has access
`Invoke-UserHunter -CheckAccess`
### Get the ACL associated with the specified object
`Get-ObjectAcl -SamAccountName labuser -ResolveGUIDs`
#### Get the ACLs associated with the specified prefix to be used for search
`Get-ObjectAcl -ADSprefix 'CN=Administrator,CN=Users' -Verbose`
### Enum ACLs using ActiveDirectory module but without resolbing GUIDs
`(Get-Acl 'AD:\CN=labuser,CN=Users,DC=offensiveps,DC=powershell,DC=local').Access`
##### To look for interesting ACEs
`Invoke-ACLScanner -ResolveGUIDs`
###### Get a list of all domain trusts for the current domain
`Get-NetDomainTrust`
`Get-NetDomainTrust -Domain redpc.offensiveps.powershell.local`
##### Using ActiveDirectory module
`Get-ADTrust -Filter **`
`Get-ADTrust -Identity redps.offensiveps.powershell.local`
###### Get details about the current forest
`Get-NetForest`
`Get-NetForest -Forest defensiveps.local`
##### Using ActiveDirectory module
`Get-ADForest`
`Get-ADForest -Identify defensiveps.local`
###### Get all domains in thee current forest
`Get-NetForestDomain`
`Get-NetForestDomain -Forest defensiveps.local`
##### Using ActiveDirectory module
`(Get-ADForest).Domains`
###### Get trusts in the forest
`Get-NetForestTrust`
`Get-NetForestTrust -Forest defensiveps.local`
##### Using ActiveDirectory module
`Get-ADTrust -Filter 'msDS-TrustForestTrustInfo -ne "$null"'`

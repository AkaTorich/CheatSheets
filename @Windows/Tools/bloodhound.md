```bash
~# log4j console
	after login try and login "log4j:password"
~# bloodhound
```

```powershell
	on windows
PS C:\Users\administrator\Desktop> Import-Module .\SharpHound.ps1
PS C:\Users\administrator\Desktop> Invoke-BloodHound -CollectionMethod All -Domain TEST.local -ZipFileName file.zip
2022-10-18T07:52:24.5059518-07:00|INFORMATION|This version of SharpHound is compatible with the 4.2 Release of BloodHound
2022-10-18T07:52:24.6311009-07:00|INFORMATION|Resolved Collection Methods: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote
2022-10-18T07:52:24.6467345-07:00|INFORMATION|Initializing SharpHound at 7:52 AM on 10/18/2022
2022-10-18T07:52:24.8967530-07:00|INFORMATION|Flags: Group, LocalAdmin, GPOLocalGroup, Session, LoggedOn, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote
2022-10-18T07:52:25.0843221-07:00|INFORMATION|Beginning LDAP search for TEST.local
2022-10-18T07:52:25.1155754-07:00|INFORMATION|Producer has finished, closing LDAP channel
2022-10-18T07:52:25.1155754-07:00|INFORMATION|LDAP channel closed, waiting for consumers
2022-10-18T07:53:10.3657554-07:00|INFORMATION|Status: 0 objects finished (+0 0)/s -- Using 101 MB RAM
2022-10-18T07:53:10.6778368-07:00|INFORMATION|Consumers finished, closing output channel
2022-10-18T07:53:10.7246971-07:00|INFORMATION|Output channel closed, waiting for output task to complete
Closing writers
2022-10-18T07:53:10.7872900-07:00|INFORMATION|Status: 103 objects finished (+103 2.288889)/s -- Using 105 MB RAM
2022-10-18T07:53:10.7872900-07:00|INFORMATION|Enumeration finished in 00:00:45.7007767
2022-10-18T07:53:10.8344895-07:00|INFORMATION|Saving cache with stats: 61 ID to type mappings.
 64 name to SID mappings.
 2 machine sid mappings.
 2 sid to domain mappings.
 0 global catalog mappings.
2022-10-18T07:53:10.8498260-07:00|INFORMATION|SharpHound Enumeration Completed at 7:53 AM on 10/18/2022! Happy Graphing!
PS C:\Users\administrator\Desktop>

and copy file to attacker
```
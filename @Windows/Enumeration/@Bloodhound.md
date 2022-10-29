https://github.com/BloodHoundAD/BloodHound
```bash
~# log4j console
	http://localhost:7474
	after login try and login "log4j:password"
	
~# bloodhound
```

```powershell
	on windows
PS C:\Users\administrator\Desktop> Import-Module .\SharpHound.ps1
PS C:\Users\administrator\Desktop> Invoke-BloodHound -CollectionMethod All -Domain TEST.local -ZipFileName file.zip
PS C:\Users\administrator\Desktop> Invoke-BloodHound -CollectionMethod All -ExcludeDC

and copy file to attacker
```
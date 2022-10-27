###### Use accesschk.exe to check for write permissions:
`> .\accesschk.exe /accepteula -uwdq C:\` #writeable 
`> .\accesschk.exe /accepteula -uwdq "C:\Program Files\"` #writeable 
`> .\accesschk.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service\"` #writeable
`> .\accesschk.exe /accepteula -uvwqk HKLM\System\CurrentControlSet\Services\regsvc`
`.\accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"` #writeable
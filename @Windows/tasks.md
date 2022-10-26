###### List all scheduled tasks your user can see:
`> schtasks /query /fo LIST /v`
###### In PowerShell:
`PS> Get-ScheduledTask | where {$_.TaskPath -notlike "\Microsoft*"} | ft TaskName,TaskPath,State`
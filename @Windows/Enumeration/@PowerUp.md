https://github.com/PowerShellMafia/PowerSploit.git
# PowerUp.ps1
`powershell -ep bypass`
`. .\PowerUp.ps1`
`Invoke-AllChecks`

`Get-ServiceUnquoted -Verbose` #unquoted with unquoted path and spaces in their name
`Get-ModifialeServiceFile -Verbose` #modifiable Get service where current user can write to this binary path
`Get-ModifiableService` #modifiable Get services which current user can modify

`help Invoke-ServiceAbuse -Examples`
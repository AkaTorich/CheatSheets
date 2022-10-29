`sc query windefend` #windefender if exists
`sc queryex type= service` #enum all services

netsh advfirewall firewall dump 
netsh advfirewall show state
netsh advfirewall show config
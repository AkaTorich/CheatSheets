nc -nv TARGET PORT   
VRFY root  
VRFY password  
  
###ENUM USERS##############################################################  
import socket  
import sys  
  
if len(sys.argv) != 2:  
    print ("Usage: vrfy.py <username>")  
    sys.exit(0)  
  
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)  
connect = s.connect(('TARGET', 25))  
banner = s.recv(1024)  
print(banner)  
  
s.send('VRFY' + sys.argv[i] + '\r\n')  
result = s.recv(1024)  
print(result)  
  
s.close()  
############################################################################
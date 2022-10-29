https://github.com/PowerShellMafia/PowerSploit.git

```powershell
C:\Users\asuka\Downloads>powershell -ep bypass
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\Users\asuka\Downloads> . ..\Desktop\powerview.ps1
PS C:\Users\asuka\Downloads> get-netdomain


Forest                  : TEST.local
DomainControllers       : {PENTEST-DC.TEST.local}
Children                : {}
DomainMode              : Unknown
DomainModeLevel         : 7
Parent                  :
PdcRoleOwner            : PENTEST-DC.TEST.local
RidRoleOwner            : PENTEST-DC.TEST.local
InfrastructureRoleOwner : PENTEST-DC.TEST.local
Name                    : TEST.local



PS C:\Users\asuka\Downloads> get-netdomaincontroller


Forest                     : TEST.local
CurrentTime                : 10/18/2022 4:20:38 AM
HighestCommittedUsn        : 24644
OSVersion                  : Windows Server 2019 Standard
Roles                      : {SchemaRole, NamingRole, PdcRole, RidRole...}
Domain                     : TEST.local
IPAddress                  : 2a00:a040:181:ad58:1:5b89:fc0a:f28a
SiteName                   : Default-First-Site-Name
SyncFromAllServersCallback :
InboundConnections         : {}
OutboundConnections        : {}
Name                       : PENTEST-DC.TEST.local
Partitions                 : {DC=TEST,DC=local, CN=Configuration,DC=TEST,DC=local,
                             CN=Schema,CN=Configuration,DC=TEST,DC=local, DC=DomainDnsZones,DC=TEST,DC=local...}



PS C:\Users\asuka\Downloads> get-domainpolicy


RegistryValues : @{MACHINE\System\CurrentControlSet\Control\Lsa\NoLMHash=System.String[]}
SystemAccess   : @{MinimumPasswordAge=1; MaximumPasswordAge=42; LockoutBadCount=0; PasswordComplexity=1;
                 RequireLogonToChangePassword=0; LSAAnonymousNameLookup=0; ForceLogoffWhenHourExpire=0;
                 PasswordHistorySize=24; ClearTextPassword=0; MinimumPasswordLength=7}
Version        : @{Revision=1; signature="$CHICAGO$"}
KerberosPolicy : @{MaxTicketAge=10; MaxServiceAge=600; MaxClockSkew=5; MaxRenewAge=7; TicketValidateClient=1}
Unicode        : @{Unicode=yes}



PS C:\Users\asuka\Downloads> (get-domainpolicy)."system access"
PS C:\Users\asuka\Downloads> (Get-DomainPolicy)."system access"
PS C:\Users\asuka\Downloads> (Get-DomainPolicy)."System Access"
PS C:\Users\asuka\Downloads> (Get-DomainPolicy)."unicode"

Unicode
-------
yes


PS C:\Users\asuka\Downloads> (Get-DomainPolicy).""
PS C:\Users\asuka\Downloads> get-netuser


logoncount             : 23
badpasswordtime        : 12/31/1600 4:00:00 PM
description            : Built-in account for administering the computer/domain
distinguishedname      : CN=Administrator,CN=Users,DC=TEST,DC=local
objectclass            : {top, person, organizationalPerson, user}
lastlogontimestamp     : 10/17/2022 5:51:54 AM
name                   : Administrator
objectsid              : S-1-5-21-2792811091-2429234815-3980700349-500
samaccountname         : Administrator
admincount             : 1
codepage               : 0
samaccounttype         : 805306368
whenchanged            : 10/17/2022 12:51:54 PM
accountexpires         : 9223372036854775807
countrycode            : 0
adspath                : LDAP://CN=Administrator,CN=Users,DC=TEST,DC=local
instancetype           : 4
objectguid             : 606e542e-3845-4ca4-b576-3f8ac10d0579
lastlogon              : 10/17/2022 9:00:49 PM
lastlogoff             : 12/31/1600 4:00:00 PM
objectcategory         : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata  : {10/17/2022 12:49:08 PM, 10/17/2022 12:49:08 PM, 10/17/2022 12:33:58 PM, 1/1/1601 6:12:16 PM}
memberof               : {CN=Group Policy Creator Owners,OU=Groups,DC=TEST,DC=local, CN=Domain
                         Admins,OU=Groups,DC=TEST,DC=local, CN=Enterprise Admins,OU=Groups,DC=TEST,DC=local, CN=Schema
                         Admins,OU=Groups,DC=TEST,DC=local...}
whencreated            : 10/17/2022 12:30:21 PM
iscriticalsystemobject : True
badpwdcount            : 0
cn                     : Administrator
useraccountcontrol     : 66048
usncreated             : 8196
primarygroupid         : 513
pwdlastset             : 10/17/2022 3:20:34 PM
usnchanged             : 12780

pwdlastset             : 12/31/1600 4:00:00 PM
logoncount             : 0
badpasswordtime        : 12/31/1600 4:00:00 PM
description            : Built-in account for guest access to the computer/domain
distinguishedname      : CN=Guest,CN=Users,DC=TEST,DC=local
objectclass            : {top, person, organizationalPerson, user}
name                   : Guest
objectsid              : S-1-5-21-2792811091-2429234815-3980700349-501
samaccountname         : Guest
codepage               : 0
samaccounttype         : 805306368
whenchanged            : 10/17/2022 12:30:21 PM
accountexpires         : 9223372036854775807
countrycode            : 0
adspath                : LDAP://CN=Guest,CN=Users,DC=TEST,DC=local
instancetype           : 4
objectguid             : 0e2bcf9b-05a3-4fb2-96a9-c0d3084fca54
lastlogon              : 12/31/1600 4:00:00 PM
lastlogoff             : 12/31/1600 4:00:00 PM
objectcategory         : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata  : {10/17/2022 12:33:58 PM, 1/1/1601 12:00:01 AM}
memberof               : CN=Guests,CN=Builtin,DC=TEST,DC=local
whencreated            : 10/17/2022 12:30:21 PM
badpwdcount            : 0
cn                     : Guest
useraccountcontrol     : 66082
usncreated             : 8197
primarygroupid         : 514
iscriticalsystemobject : True
usnchanged             : 8197

logoncount                    : 0
badpasswordtime               : 12/31/1600 4:00:00 PM
description                   : Key Distribution Center Service Account
distinguishedname             : CN=krbtgt,CN=Users,DC=TEST,DC=local
objectclass                   : {top, person, organizationalPerson, user}
name                          : krbtgt
primarygroupid                : 513
objectsid                     : S-1-5-21-2792811091-2429234815-3980700349-502
whenchanged                   : 10/17/2022 12:49:08 PM
admincount                    : 1
codepage                      : 0
samaccounttype                : 805306368
showinadvancedviewonly        : True
accountexpires                : 9223372036854775807
cn                            : krbtgt
adspath                       : LDAP://CN=krbtgt,CN=Users,DC=TEST,DC=local
instancetype                  : 4
objectguid                    : 8137e7f6-f1c1-4288-86ed-f92b23060c35
lastlogon                     : 12/31/1600 4:00:00 PM
lastlogoff                    : 12/31/1600 4:00:00 PM
samaccountname                : krbtgt
objectcategory                : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata         : {10/17/2022 12:49:08 PM, 10/17/2022 12:33:58 PM, 1/1/1601 12:04:16 AM}
serviceprincipalname          : kadmin/changepw
memberof                      : CN=Denied RODC Password Replication Group,OU=Groups,DC=TEST,DC=local
whencreated                   : 10/17/2022 12:33:58 PM
iscriticalsystemobject        : True
badpwdcount                   : 0
useraccountcontrol            : 514
usncreated                    : 12324
countrycode                   : 0
pwdlastset                    : 10/17/2022 5:33:58 AM
msds-supportedencryptiontypes : 0
usnchanged                    : 12777

logoncount            : 11
badpasswordtime       : 12/31/1600 4:00:00 PM
description           : Passw0rd
distinguishedname     : CN=Franc Casl,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Franc Casl
lastlogontimestamp    : 10/17/2022 6:26:05 AM
userprincipalname     : fcasl@TEST.local
name                  : Franc Casl
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1104
samaccountname        : fcasl
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:26:05 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Franc Casl,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : 42367c0f-245c-4567-83ea-9b13347f7d6c
lastlogon             : 10/17/2022 8:50:11 PM
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : 1/1/1601 12:00:00 AM
givenname             : Franc Casl
whencreated           : 10/17/2022 1:05:50 PM
sn                    : Casl
badpwdcount           : 0
cn                    : Franc Casl
useraccountcontrol    : 66048
usncreated            : 12820
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:05:50 AM
usnchanged            : 12912

logoncount            : 0
badpasswordtime       : 12/31/1600 4:00:00 PM
description           : Password2022
distinguishedname     : CN=Tony Stark,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Tony Stark
userprincipalname     : tstark@TEST.local
name                  : Tony Stark
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1105
samaccountname        : tstark
admincount            : 1
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:57:53 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Tony Stark,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : dff51b93-dc9d-442d-bdff-b1cb168b724e
lastlogon             : 12/31/1600 4:00:00 PM
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : {10/17/2022 1:57:53 PM, 1/1/1601 12:00:00 AM}
givenname             : Tony
memberof              : {CN=Group Policy Creator Owners,OU=Groups,DC=TEST,DC=local, CN=Domain
                        Admins,OU=Groups,DC=TEST,DC=local, CN=Enterprise Admins,OU=Groups,DC=TEST,DC=local, CN=Schema
                        Admins,OU=Groups,DC=TEST,DC=local...}
whencreated           : 10/17/2022 1:06:45 PM
sn                    : Stark
badpwdcount           : 0
cn                    : Tony Stark
useraccountcontrol    : 66048
usncreated            : 12827
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:06:45 AM
usnchanged            : 16402

logoncount            : 0
badpasswordtime       : 10/17/2022 6:35:37 AM
description           : Passw0rd
distinguishedname     : CN=Peter Parker,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Peter Parker
userprincipalname     : pparker@TEST.local
name                  : Peter Parker
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1106
samaccountname        : pparker
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:34:40 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Peter Parker,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : 6bb42e0a-3c20-4b42-9459-4fef08da37c3
lastlogon             : 12/31/1600 4:00:00 PM
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : 1/1/1601 12:00:00 AM
givenname             : Peter
whencreated           : 10/17/2022 1:07:34 PM
sn                    : Parker
badpwdcount           : 8
cn                    : Peter Parker
useraccountcontrol    : 66048
usncreated            : 12849
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:34:40 AM
usnchanged            : 12955

logoncount            : 0
badpasswordtime       : 12/31/1600 4:00:00 PM
description           : Passw0rd
distinguishedname     : CN=SQL Service,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : SQL Service
userprincipalname     : SQLService@TEST.local
name                  : SQL Service
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1107
samaccountname        : SQLService
lastlogon             : 12/31/1600 4:00:00 PM
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:57:53 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=SQL Service,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : aeb8da25-be38-4e39-86c3-7d1416e45f43
sn                    : Service
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : {10/17/2022 1:57:53 PM, 1/1/1601 12:00:00 AM}
serviceprincipalname  : PENTEST-DC/SQLService.TEST.local:60111
givenname             : SQL
admincount            : 1
memberof              : {CN=Group Policy Creator Owners,OU=Groups,DC=TEST,DC=local, CN=Domain
                        Admins,OU=Groups,DC=TEST,DC=local, CN=Enterprise Admins,OU=Groups,DC=TEST,DC=local, CN=Schema
                        Admins,OU=Groups,DC=TEST,DC=local...}
whencreated           : 10/17/2022 1:09:26 PM
badpwdcount           : 0
cn                    : SQL Service
useraccountcontrol    : 66048
usncreated            : 12856
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:09:26 AM
usnchanged            : 16401

logoncount            : 10
badpasswordtime       : 12/31/1600 4:00:00 PM
distinguishedname     : CN=Alisa Suka,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Alisa Suka
lastlogontimestamp    : 10/17/2022 6:36:58 AM
userprincipalname     : asuka@TEST.local
name                  : Alisa Suka
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1110
samaccountname        : asuka
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:36:58 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Alisa Suka,CN=Users,DC=TEST,DC=local
instancetype          : 4
usncreated            : 12961
objectguid            : a479778c-1139-49c8-8e8d-0d389c04824a
sn                    : Suka
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : 1/1/1601 12:00:00 AM
givenname             : Alisa
lastlogon             : 10/17/2022 8:46:03 PM
badpwdcount           : 0
cn                    : Alisa Suka
useraccountcontrol    : 66048
whencreated           : 10/17/2022 1:36:26 PM
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:36:26 AM
usnchanged            : 12967



PS C:\Users\asuka\Downloads> get-netuser | select cn

cn
--
Administrator
Guest
krbtgt
Franc Casl
Tony Stark
Peter Parker
SQL Service
Alisa Suka


PS C:\Users\asuka\Downloads> get-netuser | select accountname

accountname
-----------










PS C:\Users\asuka\Downloads> get-netuser | select account name
Select-Object : A positional parameter cannot be found that accepts argument 'name'.
At line:1 char:15
+ get-netuser | select account name
+               ~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Select-Object], ParameterBindingException
    + FullyQualifiedErrorId : PositionalParameterNotFound,Microsoft.PowerShell.Commands.SelectObjectCommand

PS C:\Users\asuka\Downloads> get-netuser | select account-name

account-name
------------










PS C:\Users\asuka\Downloads> get-netuser | select


logoncount             : 23
badpasswordtime        : 12/31/1600 4:00:00 PM
description            : Built-in account for administering the computer/domain
distinguishedname      : CN=Administrator,CN=Users,DC=TEST,DC=local
objectclass            : {top, person, organizationalPerson, user}
lastlogontimestamp     : 10/17/2022 5:51:54 AM
name                   : Administrator
objectsid              : S-1-5-21-2792811091-2429234815-3980700349-500
samaccountname         : Administrator
admincount             : 1
codepage               : 0
samaccounttype         : 805306368
whenchanged            : 10/17/2022 12:51:54 PM
accountexpires         : 9223372036854775807
countrycode            : 0
adspath                : LDAP://CN=Administrator,CN=Users,DC=TEST,DC=local
instancetype           : 4
objectguid             : 606e542e-3845-4ca4-b576-3f8ac10d0579
lastlogon              : 10/17/2022 9:00:49 PM
lastlogoff             : 12/31/1600 4:00:00 PM
objectcategory         : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata  : {10/17/2022 12:49:08 PM, 10/17/2022 12:49:08 PM, 10/17/2022 12:33:58 PM, 1/1/1601 6:12:16 PM}
memberof               : {CN=Group Policy Creator Owners,OU=Groups,DC=TEST,DC=local, CN=Domain
                         Admins,OU=Groups,DC=TEST,DC=local, CN=Enterprise Admins,OU=Groups,DC=TEST,DC=local, CN=Schema
                         Admins,OU=Groups,DC=TEST,DC=local...}
whencreated            : 10/17/2022 12:30:21 PM
iscriticalsystemobject : True
badpwdcount            : 0
cn                     : Administrator
useraccountcontrol     : 66048
usncreated             : 8196
primarygroupid         : 513
pwdlastset             : 10/17/2022 3:20:34 PM
usnchanged             : 12780

pwdlastset             : 12/31/1600 4:00:00 PM
logoncount             : 0
badpasswordtime        : 12/31/1600 4:00:00 PM
description            : Built-in account for guest access to the computer/domain
distinguishedname      : CN=Guest,CN=Users,DC=TEST,DC=local
objectclass            : {top, person, organizationalPerson, user}
name                   : Guest
objectsid              : S-1-5-21-2792811091-2429234815-3980700349-501
samaccountname         : Guest
codepage               : 0
samaccounttype         : 805306368
whenchanged            : 10/17/2022 12:30:21 PM
accountexpires         : 9223372036854775807
countrycode            : 0
adspath                : LDAP://CN=Guest,CN=Users,DC=TEST,DC=local
instancetype           : 4
objectguid             : 0e2bcf9b-05a3-4fb2-96a9-c0d3084fca54
lastlogon              : 12/31/1600 4:00:00 PM
lastlogoff             : 12/31/1600 4:00:00 PM
objectcategory         : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata  : {10/17/2022 12:33:58 PM, 1/1/1601 12:00:01 AM}
memberof               : CN=Guests,CN=Builtin,DC=TEST,DC=local
whencreated            : 10/17/2022 12:30:21 PM
badpwdcount            : 0
cn                     : Guest
useraccountcontrol     : 66082
usncreated             : 8197
primarygroupid         : 514
iscriticalsystemobject : True
usnchanged             : 8197

logoncount                    : 0
badpasswordtime               : 12/31/1600 4:00:00 PM
description                   : Key Distribution Center Service Account
distinguishedname             : CN=krbtgt,CN=Users,DC=TEST,DC=local
objectclass                   : {top, person, organizationalPerson, user}
name                          : krbtgt
primarygroupid                : 513
objectsid                     : S-1-5-21-2792811091-2429234815-3980700349-502
whenchanged                   : 10/17/2022 12:49:08 PM
admincount                    : 1
codepage                      : 0
samaccounttype                : 805306368
showinadvancedviewonly        : True
accountexpires                : 9223372036854775807
cn                            : krbtgt
adspath                       : LDAP://CN=krbtgt,CN=Users,DC=TEST,DC=local
instancetype                  : 4
objectguid                    : 8137e7f6-f1c1-4288-86ed-f92b23060c35
lastlogon                     : 12/31/1600 4:00:00 PM
lastlogoff                    : 12/31/1600 4:00:00 PM
samaccountname                : krbtgt
objectcategory                : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata         : {10/17/2022 12:49:08 PM, 10/17/2022 12:33:58 PM, 1/1/1601 12:04:16 AM}
serviceprincipalname          : kadmin/changepw
memberof                      : CN=Denied RODC Password Replication Group,OU=Groups,DC=TEST,DC=local
whencreated                   : 10/17/2022 12:33:58 PM
iscriticalsystemobject        : True
badpwdcount                   : 0
useraccountcontrol            : 514
usncreated                    : 12324
countrycode                   : 0
pwdlastset                    : 10/17/2022 5:33:58 AM
msds-supportedencryptiontypes : 0
usnchanged                    : 12777

logoncount            : 11
badpasswordtime       : 12/31/1600 4:00:00 PM
description           : Passw0rd
distinguishedname     : CN=Franc Casl,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Franc Casl
lastlogontimestamp    : 10/17/2022 6:26:05 AM
userprincipalname     : fcasl@TEST.local
name                  : Franc Casl
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1104
samaccountname        : fcasl
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:26:05 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Franc Casl,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : 42367c0f-245c-4567-83ea-9b13347f7d6c
lastlogon             : 10/17/2022 8:50:11 PM
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : 1/1/1601 12:00:00 AM
givenname             : Franc Casl
whencreated           : 10/17/2022 1:05:50 PM
sn                    : Casl
badpwdcount           : 0
cn                    : Franc Casl
useraccountcontrol    : 66048
usncreated            : 12820
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:05:50 AM
usnchanged            : 12912

logoncount            : 0
badpasswordtime       : 12/31/1600 4:00:00 PM
description           : Password2022
distinguishedname     : CN=Tony Stark,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Tony Stark
userprincipalname     : tstark@TEST.local
name                  : Tony Stark
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1105
samaccountname        : tstark
admincount            : 1
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:57:53 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Tony Stark,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : dff51b93-dc9d-442d-bdff-b1cb168b724e
lastlogon             : 12/31/1600 4:00:00 PM
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : {10/17/2022 1:57:53 PM, 1/1/1601 12:00:00 AM}
givenname             : Tony
memberof              : {CN=Group Policy Creator Owners,OU=Groups,DC=TEST,DC=local, CN=Domain
                        Admins,OU=Groups,DC=TEST,DC=local, CN=Enterprise Admins,OU=Groups,DC=TEST,DC=local, CN=Schema
                        Admins,OU=Groups,DC=TEST,DC=local...}
whencreated           : 10/17/2022 1:06:45 PM
sn                    : Stark
badpwdcount           : 0
cn                    : Tony Stark
useraccountcontrol    : 66048
usncreated            : 12827
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:06:45 AM
usnchanged            : 16402

logoncount            : 0
badpasswordtime       : 10/17/2022 6:35:37 AM
description           : Passw0rd
distinguishedname     : CN=Peter Parker,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Peter Parker
userprincipalname     : pparker@TEST.local
name                  : Peter Parker
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1106
samaccountname        : pparker
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:34:40 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Peter Parker,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : 6bb42e0a-3c20-4b42-9459-4fef08da37c3
lastlogon             : 12/31/1600 4:00:00 PM
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : 1/1/1601 12:00:00 AM
givenname             : Peter
whencreated           : 10/17/2022 1:07:34 PM
sn                    : Parker
badpwdcount           : 8
cn                    : Peter Parker
useraccountcontrol    : 66048
usncreated            : 12849
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:34:40 AM
usnchanged            : 12955

logoncount            : 0
badpasswordtime       : 12/31/1600 4:00:00 PM
description           : Passw0rd
distinguishedname     : CN=SQL Service,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : SQL Service
userprincipalname     : SQLService@TEST.local
name                  : SQL Service
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1107
samaccountname        : SQLService
lastlogon             : 12/31/1600 4:00:00 PM
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:57:53 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=SQL Service,CN=Users,DC=TEST,DC=local
instancetype          : 4
objectguid            : aeb8da25-be38-4e39-86c3-7d1416e45f43
sn                    : Service
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : {10/17/2022 1:57:53 PM, 1/1/1601 12:00:00 AM}
serviceprincipalname  : PENTEST-DC/SQLService.TEST.local:60111
givenname             : SQL
admincount            : 1
memberof              : {CN=Group Policy Creator Owners,OU=Groups,DC=TEST,DC=local, CN=Domain
                        Admins,OU=Groups,DC=TEST,DC=local, CN=Enterprise Admins,OU=Groups,DC=TEST,DC=local, CN=Schema
                        Admins,OU=Groups,DC=TEST,DC=local...}
whencreated           : 10/17/2022 1:09:26 PM
badpwdcount           : 0
cn                    : SQL Service
useraccountcontrol    : 66048
usncreated            : 12856
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:09:26 AM
usnchanged            : 16401

logoncount            : 10
badpasswordtime       : 12/31/1600 4:00:00 PM
distinguishedname     : CN=Alisa Suka,CN=Users,DC=TEST,DC=local
objectclass           : {top, person, organizationalPerson, user}
displayname           : Alisa Suka
lastlogontimestamp    : 10/17/2022 6:36:58 AM
userprincipalname     : asuka@TEST.local
name                  : Alisa Suka
objectsid             : S-1-5-21-2792811091-2429234815-3980700349-1110
samaccountname        : asuka
codepage              : 0
samaccounttype        : 805306368
whenchanged           : 10/17/2022 1:36:58 PM
accountexpires        : 9223372036854775807
countrycode           : 0
adspath               : LDAP://CN=Alisa Suka,CN=Users,DC=TEST,DC=local
instancetype          : 4
usncreated            : 12961
objectguid            : a479778c-1139-49c8-8e8d-0d389c04824a
sn                    : Suka
lastlogoff            : 12/31/1600 4:00:00 PM
objectcategory        : CN=Person,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata : 1/1/1601 12:00:00 AM
givenname             : Alisa
lastlogon             : 10/17/2022 8:46:03 PM
badpwdcount           : 0
cn                    : Alisa Suka
useraccountcontrol    : 66048
whencreated           : 10/17/2022 1:36:26 PM
primarygroupid        : 513
pwdlastset            : 10/17/2022 6:36:26 AM
usnchanged            : 12967



PS C:\Users\asuka\Downloads> get-userproperty

Name
----
accountexpires
admincount
adspath
badpasswordtime
badpwdcount
cn
codepage
countrycode
description
distinguishedname
dscorepropagationdata
instancetype
iscriticalsystemobject
lastlogoff
lastlogon
lastlogontimestamp
logoncount
memberof
name
objectcategory
objectclass
objectguid
objectsid
primarygroupid
pwdlastset
samaccountname
samaccounttype
useraccountcontrol
usnchanged
usncreated
whenchanged
whencreated


PS C:\Users\asuka\Downloads> get-userproperty -properties pwdlastset

name          pwdlastset
----          ----------
Administrator 10/17/2022 3:20:34 PM
Guest         12/31/1600 4:00:00 PM
krbtgt        10/17/2022 5:33:58 AM
Franc Casl    10/17/2022 6:05:50 AM
Tony Stark    10/17/2022 6:06:45 AM
Peter Parker  10/17/2022 6:34:40 AM
SQL Service   10/17/2022 6:09:26 AM
Alisa Suka    10/17/2022 6:36:26 AM


PS C:\Users\asuka\Downloads> get-userproperty -properties logoncount

name          logoncount
----          ----------
Administrator         23
Guest                  0
krbtgt                 0
Franc Casl            11
Tony Stark             0
Peter Parker           0
SQL Service            0
Alisa Suka            10


PS C:\Users\asuka\Downloads> get-netcomputer
PENTEST-DC.TEST.local
ENT1.TEST.local
ENT2.TEST.local
PS C:\Users\asuka\Downloads> get-netcomputer --fulldata
PS C:\Users\asuka\Downloads> get-netcomputer -fulldata


pwdlastset                    : 10/17/2022 5:34:14 AM
logoncount                    : 54
msds-generationid             : {82, 74, 28, 73...}
serverreferencebl             : CN=PENTEST-DC,CN=Servers,CN=Default-First-Site-Name,CN=Sites,CN=Configuration,DC=TEST,D
                                C=local
badpasswordtime               : 12/31/1600 4:00:00 PM
distinguishedname             : CN=PENTEST-DC,OU=Domain Controllers,DC=TEST,DC=local
objectclass                   : {top, person, organizationalPerson, user...}
lastlogontimestamp            : 10/17/2022 5:34:38 AM
name                          : PENTEST-DC
primarygroupid                : 516
objectsid                     : S-1-5-21-2792811091-2429234815-3980700349-1000
samaccountname                : PENTEST-DC$
localpolicyflags              : 0
codepage                      : 0
samaccounttype                : 805306369
whenchanged                   : 10/18/2022 3:39:29 AM
accountexpires                : 9223372036854775807
cn                            : PENTEST-DC
adspath                       : LDAP://CN=PENTEST-DC,OU=Domain Controllers,DC=TEST,DC=local
instancetype                  : 4
msdfsr-computerreferencebl    : CN=PENTEST-DC,CN=Topology,CN=Domain System
                                Volume,CN=DFSR-GlobalSettings,CN=System,DC=TEST,DC=local
objectguid                    : 5438b31c-50b5-4d51-8825-9433f7560ce4
operatingsystem               : Windows Server 2019 Standard
operatingsystemversion        : 10.0 (17763)
lastlogoff                    : 12/31/1600 4:00:00 PM
objectcategory                : CN=Computer,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata         : {10/17/2022 12:33:58 PM, 1/1/1601 12:00:01 AM}
serviceprincipalname          : {Dfsr-12F9A27C-BF97-4787-9364-D31B6C55EB04/PENTEST-DC.TEST.local,
                                ldap/PENTEST-DC.TEST.local/ForestDnsZones.TEST.local,
                                ldap/PENTEST-DC.TEST.local/DomainDnsZones.TEST.local, DNS/PENTEST-DC.TEST.local...}
usncreated                    : 12293
usercertificate               : {48, 130, 5, 245...}
memberof                      : {CN=Pre-Windows 2000 Compatible Access,CN=Builtin,DC=TEST,DC=local, CN=Cert
                                Publishers,OU=Groups,DC=TEST,DC=local}
lastlogon                     : 10/17/2022 9:08:26 PM
badpwdcount                   : 0
useraccountcontrol            : 532480
whencreated                   : 10/17/2022 12:33:58 PM
countrycode                   : 0
iscriticalsystemobject        : True
msds-supportedencryptiontypes : 28
usnchanged                    : 24604
ridsetreferences              : CN=RID Set,CN=PENTEST-DC,OU=Domain Controllers,DC=TEST,DC=local
dnshostname                   : PENTEST-DC.TEST.local

logoncount                    : 20
badpasswordtime               : 12/31/1600 4:00:00 PM
distinguishedname             : CN=ENT1,CN=Computers,DC=TEST,DC=local
objectclass                   : {top, person, organizationalPerson, user...}
badpwdcount                   : 0
lastlogontimestamp            : 10/17/2022 6:25:09 AM
objectsid                     : S-1-5-21-2792811091-2429234815-3980700349-1108
samaccountname                : ENT1$
localpolicyflags              : 0
codepage                      : 0
samaccounttype                : 805306369
whenchanged                   : 10/17/2022 1:25:37 PM
countrycode                   : 0
cn                            : ENT1
accountexpires                : 9223372036854775807
adspath                       : LDAP://CN=ENT1,CN=Computers,DC=TEST,DC=local
instancetype                  : 4
usncreated                    : 12897
objectguid                    : 35e2b28e-ba97-4fcc-bd10-686d0970e5e6
operatingsystem               : Windows 10 Enterprise LTSC
operatingsystemversion        : 10.0 (17763)
lastlogoff                    : 12/31/1600 4:00:00 PM
objectcategory                : CN=Computer,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata         : 1/1/1601 12:00:00 AM
serviceprincipalname          : {RestrictedKrbHost/ENT1, HOST/ENT1, RestrictedKrbHost/ENT1.TEST.local,
                                HOST/ENT1.TEST.local}
lastlogon                     : 10/17/2022 8:53:59 PM
iscriticalsystemobject        : False
usnchanged                    : 12909
useraccountcontrol            : 4096
whencreated                   : 10/17/2022 1:25:09 PM
primarygroupid                : 515
pwdlastset                    : 10/17/2022 6:25:09 AM
msds-supportedencryptiontypes : 28
name                          : ENT1
dnshostname                   : ENT1.TEST.local

logoncount                    : 19
badpasswordtime               : 12/31/1600 4:00:00 PM
distinguishedname             : CN=ENT2,CN=Computers,DC=TEST,DC=local
objectclass                   : {top, person, organizationalPerson, user...}
badpwdcount                   : 0
lastlogontimestamp            : 10/17/2022 6:30:13 AM
objectsid                     : S-1-5-21-2792811091-2429234815-3980700349-1109
samaccountname                : ENT2$
localpolicyflags              : 0
codepage                      : 0
samaccounttype                : 805306369
whenchanged                   : 10/17/2022 1:30:40 PM
countrycode                   : 0
cn                            : ENT2
accountexpires                : 9223372036854775807
adspath                       : LDAP://CN=ENT2,CN=Computers,DC=TEST,DC=local
instancetype                  : 4
usncreated                    : 12929
objectguid                    : 29e97556-bcfd-463d-b7f3-11618e42eec2
operatingsystem               : Windows 10 Enterprise LTSC
operatingsystemversion        : 10.0 (17763)
lastlogoff                    : 12/31/1600 4:00:00 PM
objectcategory                : CN=Computer,CN=Schema,CN=Configuration,DC=TEST,DC=local
dscorepropagationdata         : 1/1/1601 12:00:00 AM
serviceprincipalname          : {RestrictedKrbHost/ENT2, HOST/ENT2, RestrictedKrbHost/ENT2.TEST.local,
                                HOST/ENT2.TEST.local}
lastlogon                     : 10/17/2022 8:46:07 PM
iscriticalsystemobject        : False
usnchanged                    : 12939
useraccountcontrol            : 4096
whencreated                   : 10/17/2022 1:30:13 PM
primarygroupid                : 515
pwdlastset                    : 10/17/2022 6:30:13 AM
msds-supportedencryptiontypes : 28
name                          : ENT2
dnshostname                   : ENT2.TEST.local



PS C:\Users\asuka\Downloads> get-netcomputer -fulldata | select operatingsystem

operatingsystem
---------------
Windows Server 2019 Standard
Windows 10 Enterprise LTSC
Windows 10 Enterprise LTSC


PS C:\Users\asuka\Downloads> get-netgroups
get-netgroups : The term 'get-netgroups' is not recognized as the name of a cmdlet, function, script file, or operable
program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ get-netgroups
+ ~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (get-netgroups:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\Users\asuka\Downloads> get-netgroup
Administrators
Users
Guests
Print Operators
Backup Operators
Replicator
Remote Desktop Users
Network Configuration Operators
Performance Monitor Users
Performance Log Users
Distributed COM Users
IIS_IUSRS
Cryptographic Operators
Event Log Readers
Certificate Service DCOM Access
RDS Remote Access Servers
RDS Endpoint Servers
RDS Management Servers
Hyper-V Administrators
Access Control Assistance Operators
Remote Management Users
Storage Replica Administrators
Domain Computers
Domain Controllers
Schema Admins
Enterprise Admins
Cert Publishers
Domain Admins
Domain Users
Domain Guests
Group Policy Creator Owners
RAS and IAS Servers
Server Operators
Account Operators
Pre-Windows 2000 Compatible Access
Incoming Forest Trust Builders
Windows Authorization Access Group
Terminal Server License Servers
Allowed RODC Password Replication Group
Denied RODC Password Replication Group
Read-only Domain Controllers
Enterprise Read-only Domain Controllers
Cloneable Domain Controllers
Protected Users
Key Admins
Enterprise Key Admins
DnsAdmins
DnsUpdateProxy
PS C:\Users\asuka\Downloads> get-netgroup -groupname "domain admins"
Domain Admins
PS C:\Users\asuka\Downloads> get-netgroup -groupname *admins*
Schema Admins
Enterprise Admins
Domain Admins
Key Admins
Enterprise Key Admins
DnsAdmins
PS C:\Users\asuka\Downloads> get-netgroupmember -groupname "domain admins"


GroupDomain  : TEST.local
GroupName    : Domain Admins
MemberDomain : TEST.local
MemberName   : SQLService
MemberSid    : S-1-5-21-2792811091-2429234815-3980700349-1107
IsGroup      : False
MemberDN     : CN=SQL Service,CN=Users,DC=TEST,DC=local

GroupDomain  : TEST.local
GroupName    : Domain Admins
MemberDomain : TEST.local
MemberName   : tstark
MemberSid    : S-1-5-21-2792811091-2429234815-3980700349-1105
IsGroup      : False
MemberDN     : CN=Tony Stark,CN=Users,DC=TEST,DC=local

GroupDomain  : TEST.local
GroupName    : Domain Admins
MemberDomain : TEST.local
MemberName   : Administrator
MemberSid    : S-1-5-21-2792811091-2429234815-3980700349-500
IsGroup      : False
MemberDN     : CN=Administrator,CN=Users,DC=TEST,DC=local



PS C:\Users\asuka\Downloads> invoke-sharefinder
\\ENT2.TEST.local\ADMIN$        - Remote Admin
\\ENT2.TEST.local\C$    - Default share
\\ENT2.TEST.local\IPC$  - Remote IPC
\\ENT2.TEST.local\Share         -
\\PENTEST-DC.TEST.local\ADMIN$  - Remote Admin
\\PENTEST-DC.TEST.local\C$      - Default share
\\PENTEST-DC.TEST.local\hackme  -
\\PENTEST-DC.TEST.local\IPC$    - Remote IPC
\\PENTEST-DC.TEST.local\NETLOGON        - Logon server share
\\PENTEST-DC.TEST.local\SYSVOL  - Logon server share
PS C:\Users\asuka\Downloads> get-netgpo


usncreated               : 5672
systemflags              : -1946157056
displayname              : Default Domain Policy
gpcmachineextensionnames : [{35378EAC-683F-11D2-A89A-00C04FBBCFA2}{53D6AB1B-2488-11D1-A28C-00C04FB94F17}][{827D319E-6EA
                           C-11D2-A4EA-00C04F79F83A}{803E14A0-B4FB-11D0-A0D0-00A0C90F574B}][{B1BE8D72-6EAC-11D2-A4EA-00
                           C04F79F83A}{53D6AB1B-2488-11D1-A28C-00C04FB94F17}]
whenchanged              : 10/17/2022 12:51:55 PM
objectclass              : {top, container, groupPolicyContainer}
gpcfunctionalityversion  : 2
showinadvancedviewonly   : True
usnchanged               : 12782
dscorepropagationdata    : {10/17/2022 12:33:58 PM, 1/1/1601 12:00:00 AM}
name                     : {31B2F340-016D-11D2-945F-00C04FB984F9}
adspath                  : LDAP://CN={31B2F340-016D-11D2-945F-00C04FB984F9},CN=Policies,CN=System,DC=TEST,DC=local
flags                    : 0
cn                       : {31B2F340-016D-11D2-945F-00C04FB984F9}
iscriticalsystemobject   : True
gpcfilesyspath           : \\TEST.local\sysvol\TEST.local\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}
distinguishedname        : CN={31B2F340-016D-11D2-945F-00C04FB984F9},CN=Policies,CN=System,DC=TEST,DC=local
whencreated              : 10/17/2022 12:30:21 PM
versionnumber            : 3
instancetype             : 4
objectguid               : e8842b1b-3397-441d-ab22-511ea8d5fa6d
objectcategory           : CN=Group-Policy-Container,CN=Schema,CN=Configuration,DC=TEST,DC=local

usncreated               : 5675
systemflags              : -1946157056
displayname              : Default Domain Controllers Policy
gpcmachineextensionnames : [{827D319E-6EAC-11D2-A4EA-00C04F79F83A}{803E14A0-B4FB-11D0-A0D0-00A0C90F574B}]
whenchanged              : 10/18/2022 3:13:25 AM
objectclass              : {top, container, groupPolicyContainer}
gpcfunctionalityversion  : 2
showinadvancedviewonly   : True
usnchanged               : 16549
dscorepropagationdata    : {10/17/2022 12:33:58 PM, 1/1/1601 12:00:00 AM}
name                     : {6AC1786C-016F-11D2-945F-00C04fB984F9}
adspath                  : LDAP://CN={6AC1786C-016F-11D2-945F-00C04fB984F9},CN=Policies,CN=System,DC=TEST,DC=local
flags                    : 0
cn                       : {6AC1786C-016F-11D2-945F-00C04fB984F9}
iscriticalsystemobject   : True
gpcfilesyspath           : \\TEST.local\sysvol\TEST.local\Policies\{6AC1786C-016F-11D2-945F-00C04fB984F9}
distinguishedname        : CN={6AC1786C-016F-11D2-945F-00C04fB984F9},CN=Policies,CN=System,DC=TEST,DC=local
whencreated              : 10/17/2022 12:30:21 PM
versionnumber            : 5
instancetype             : 4
objectguid               : 0dddde9e-f0f8-4f4d-be33-c0ab47687e42
objectcategory           : CN=Group-Policy-Container,CN=Schema,CN=Configuration,DC=TEST,DC=local

usncreated               : 12883
displayname              : Disable Windows Defender
gpcmachineextensionnames : [{35378EAC-683F-11D2-A89A-00C04FBBCFA2}{D02B1F72-3407-48AE-BA88-E8213C6761F1}]
whenchanged              : 10/17/2022 1:19:21 PM
objectclass              : {top, container, groupPolicyContainer}
gpcfunctionalityversion  : 2
showinadvancedviewonly   : True
usnchanged               : 12891
dscorepropagationdata    : 1/1/1601 12:00:00 AM
name                     : {0EBAD86D-3E3F-49F5-A964-07C03A1F0EA4}
adspath                  : LDAP://CN={0EBAD86D-3E3F-49F5-A964-07C03A1F0EA4},CN=Policies,CN=System,DC=TEST,DC=local
flags                    : 0
cn                       : {0EBAD86D-3E3F-49F5-A964-07C03A1F0EA4}
gpcfilesyspath           : \\TEST.local\SysVol\TEST.local\Policies\{0EBAD86D-3E3F-49F5-A964-07C03A1F0EA4}
distinguishedname        : CN={0EBAD86D-3E3F-49F5-A964-07C03A1F0EA4},CN=Policies,CN=System,DC=TEST,DC=local
whencreated              : 10/17/2022 1:16:10 PM
versionnumber            : 1
instancetype             : 4
objectguid               : c7f75b13-8db8-4ebb-b760-52fc2b207d0f
objectcategory           : CN=Group-Policy-Container,CN=Schema,CN=Configuration,DC=TEST,DC=local



PS C:\Users\asuka\Downloads> get-netgpo | select displayname, whenchange

displayname                       whenchange
-----------                       ----------
Default Domain Policy
Default Domain Controllers Policy
Disable Windows Defender


PS C:\Users\asuka\Downloads> get-netgpo | select displayname, whenchanged

displayname                       whenchanged
-----------                       -----------
Default Domain Policy             10/17/2022 12:51:55 PM
Default Domain Controllers Policy 10/18/2022 3:13:25 AM
Disable Windows Defender          10/17/2022 1:19:21 PM


P
```
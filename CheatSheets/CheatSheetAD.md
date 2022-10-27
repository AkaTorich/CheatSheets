# Шпаргалка IAD

---

## Необходимые основные команды

`xfreerdp /v:<IP> /u:<User> /p:<Password>`  
`ping <IP>`

---

## Общие команды

`Get-Module`  
Возвращает список загруженных модулей PowerShell.

`Get-Command -Module ActiveDirectory`  
Список команд для указанного модуля.

`Get-Help <cmd-let>`  
Показывает синтаксис справки для указанного cmd-let.

`Import-Module ActiveDirectory` Импортирует модуль Active Directory

---

## Команды Active Directory PowerShell

---

### Команды пользователя AD

`New-ADUser -Name "first last" -Accountpassword (Read-Host -AsSecureString "Super$ecurePassword!") -Enabled $true -OtherAttributes @{'title'="Analyst";'mail'="f.last@domain.com"}`  
Добавьте пользователя в AD и задайте атрибуты.

`Remove-ADUser -Identity <name>`  
Удаляет пользователя из AD с идентификатором "имя".

`Unlock-ADAccount -Identity <name>`  
Разблокирует учетную запись пользователя с идентификатором "имя".

`Set-ADAccountPassword -Identity <'name'> -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "NewP@ssw0rdReset!" -Force)`  
Установите для пароля пользователя AD указанный пароль.

`Set-ADUser -Identity amasters -ChangePasswordAtLogon $true`  
Заставьте пользователя изменить свой пароль при следующей попытке входа в систему.

---

### Команды группы объявлений

`New-ADOrganizationalUnit -Name "name" -Path "OU=folder,DC=domain,DC=local"`  
Создайте новый контейнер AD OU с именем "name" по указанному пути.

`New-ADGroup -Name "name" -SamAccountName analysts -GroupCategory Security -GroupScope Global -DisplayName "Security Analysts" -Path "CN=Users,DC=domain,DC=local" -Description "Members of this group are Security Analysts under the IT OU"`  
Создайте новую группу безопасности с именем "имя" и соответствующими атрибутами.

`Add-ADGroupMember -Identity 'group name' -Members 'ACepheus,OStarchaser,ACallisto'`  
Добавьте пользователя AD в указанную группу.

---

### Команды объекта групповой политики

`Copy-GPO -SourceName "GPO to copy" -TargetName "Name"`  
Скопируйте объект групповой политики для использования в качестве нового объекта групповой политики с целевым именем "name".

`Set-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes`  
Свяжите объект групповой политики для использования с определенным подразделением или группой безопасности.

---

### Компьютерные команды

`Add-Computer -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\HTB-student_adm' -Restart`  
Добавьте новый компьютер в домен, используя указанные учетные данные.

`Add-Computer -ComputerName 'name' -LocalCredential '.\localuser' -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\htb-student_adm' -Restart`  
Удаленное добавление компьютера в домен.

`Get-ADComputer -Identity "name" -Properties * | select CN,CanonicalName,IPv4Address`  
Проверьте наличие компьютера с именем "name" и просмотрите его свойства.
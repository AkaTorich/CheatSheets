Как поднять свой выходной узел TORa  
Еще больше ништяков у нас на канале t.me/sxemopub  
Зачем вообще нужна выходная нода?  
Есть сеть интернет, а есть сеть Тор. Простым языком если обьяснить, то http и .onion  
Ну так вот если с браузера тор, серфить по .onion ресурсам. То все пучком, трафик находится в зашифрованной сети и мы находимся в безопасности.  
А если мы хотим зайти в http то есть в сеть интернет, с браузера тор, то наш трафик автоматически расшифровывается через выходной узел, потому что сеть интернет не может читать трафик тора и для этого созданы выходные узлы, которые “конвертируют” трафик тора в трафик интернет.  
И тем самым мы просматриваем уже http сайты с тора, но тут есть опасность. Стать владельцем Выходного узла может каждый, в том числе и спец службы.  
А что грозит собой, быть владельцем тор узла?  
Если вы владелец маршутизатора, вы можете в легкую перехватывать Http трафик. И этого никто не заметит. С https ситуация сложней, но тоже вполне реализуема.  
А архитектура тора устроена так, что мы подключаемся к рандомным тор узлам.  
Вывод из этого какой? Владелец выходного узла, может быть мошенником или сотрудником каких либо организаций. Так могут перехватить ваши идентификационные данные, все странички куда ты серфите, файлы которые качали, да в общем то все.  
Но, выход есть. Мы можем сами стать владельцем выходного узла, плюсы имеются в том, что наш трафик будет только наш и никто его прослушать не сможет. А мы сможем прослушивать других и пылесосить логи, идентификационные данные и в принципе весь трафик который поступает через наш узел. Заманчиво?  
Давайте разберем, как нам поднять выходной узел?  
Нам необходимо купить сервер, впс. Версия Debian 8 x64 конфигурации можно самые простые выбрать, в целом такой впс стоит порядка 10$ примерно. Второй момент, если будете регать тор ноду на свои данные, то мы все знаем как людей арестовывали за содержание тор ноды, когда с этой ноды полилась грязь грязная, владельца арестовывали и трясли. Так что позаботьтесь о своей безопасности.  
Соотвественно, после того как мы купили впс, логируемся на него и прозводим следующие команды.  
# Обновляем пакеты.  
apt-get update  
# Устанавливаем непосредственно сам тор.  
apt-get install tor  
# Устанавливаем редактор, если он не установлен  
apt-get install nano  
# Далее переходим к настройке конфига  
nano /etc/tor/torrc  
# Скидываю пример конфига и рассказываю про него более подробно и соотвественно что редактировать и что менять.  
SocksPort 9050  
ORPort 9001  
Nickname torname  
RelayBandwidthRate 80 KB  
RelayBandwidthBurst 100 KB  
ExitPolicy accept *:20–23 # FTP, SSH, telnet  
ExitPolicy accept *:43 # WHOISsk  
ExitPolicy accept *:53 # DNS  
ExitPolicy accept *:79–81 # finger, HTTP  
ExitPolicy accept *:88 # kerberos  
ExitPolicy accept *:143 # IMAP  
ExitPolicy accept *:194 # IRC  
ExitPolicy accept *:220 # IMAP3  
ExitPolicy accept *:389 # LDAP  
ExitPolicy accept *:443 # HTTPS  
ExitPolicy accept *:464 # kpasswd  
ExitPolicy accept *:531 # IRC/AIM  
ExitPolicy accept *:543–544 # Kerberos  
ExitPolicy accept *:554 # RTSP  
ExitPolicy accept *:563 # NNTP over SSL  
ExitPolicy accept *:636 # LDAP over SSL  
ExitPolicy accept *:706 # SILC  
ExitPolicy accept *:749 # kerberos  
ExitPolicy accept *:873 # rsync  
ExitPolicy accept *:902–904 # VMware  
ExitPolicy accept *:981 # Remote HTTPS management for firewall  
ExitPolicy accept *:989–995 # FTP over SSL, Netnews Administration System, telnets, IMAP over SSL, ircs, POP3 over SSL  
ExitPolicy accept *:1194 # OpenVPN  
ExitPolicy accept *:1220 # QT Server Admin  
ExitPolicy accept *:1293 # PKT-KRB-IPSec  
ExitPolicy accept *:1500 # VLSI License Manager  
ExitPolicy accept *:1533 # Sametime  
ExitPolicy accept *:1677 # GroupWise  
ExitPolicy accept *:1723 # PPTP  
ExitPolicy accept *:1755 # RTSP  
ExitPolicy accept *:1863 # MSNP  
ExitPolicy accept *:2082 # Infowave Mobility Server  
ExitPolicy accept *:2083 # Secure Radius Service (radsec)  
ExitPolicy accept *:2086–2087 # GNUnet, ELI  
ExitPolicy accept *:2095–2096 # NBX  
ExitPolicy accept *:2102–2104 # Zephyr  
ExitPolicy accept *:3128 # SQUID  
ExitPolicy accept *:3389 # MS WBT  
ExitPolicy accept *:3690 # SVN  
ExitPolicy accept *:4321 # RWHOIS  
ExitPolicy accept *:4643 # Virtuozzo  
ExitPolicy accept *:5050 # MMCC  
ExitPolicy accept *:5190 # ICQ  
ExitPolicy accept *:5222–5223 # XMPP, XMPP over SSL  
ExitPolicy accept *:5228 # Android Market  
ExitPolicy accept *:5900 # VNC  
ExitPolicy accept *:6660–6669 # IRC  
ExitPolicy accept *:6679 # IRC SSL  
ExitPolicy accept *:6697 # IRC SSL  
ExitPolicy accept *:8000 # iRDMI  
ExitPolicy accept *:8008 # HTTP alternate  
ExitPolicy accept *:8074 # Gadu-Gadu  
ExitPolicy accept *:8080 # HTTP Proxies  
ExitPolicy accept *:8082 # HTTPS Electrum Bitcoin port  
ExitPolicy accept *:8087–8088 # Simplify Media SPP Protocol, Radan HTTP  
ExitPolicy accept *:8332–8333 # Bitcoin  
ExitPolicy accept *:8443 # PCsync HTTPS  
ExitPolicy accept *:8888 # HTTP Proxies, NewsEDGE  
ExitPolicy accept *:9418 # git  
ExitPolicy accept *:9999 # distinct  
ExitPolicy accept *:10000 # Network Data Management Protocol  
ExitPolicy accept *:11371 # OpenPGP hkp (http keyserver protocol)  
ExitPolicy accept *:12350 # Skype — XXX: Remove? Skype bans tor now..  
ExitPolicy accept *:19294 # Google Voice TCP  
ExitPolicy accept *:19638 # Ensim control panel  
ExitPolicy accept *:23456 # Skype — XXX: Remove? Skype bans tor now..  
ExitPolicy accept *:33033 # Skype — XXX: Remove? Skype bans tor now..  
ExitPolicy accept *:50002 # Electrum Bitcoin SSL  
ExitPolicy accept *:64738 # Mumble  
ExitPolicy reject *:*  
Данный конфиг, либо этот, либо ваш — надо вставить в конфиг. (см предыдущая команда)  
Сделать это надо копипастом. в линуксе чтоб скопировать в терминал надо Ctrl+shift+v  
Переписывать вручную не стоит, по причине если допустите хотябы 1 ошибку. ничего работать не будет.  
В самом начале параметр SocksPort это порт по которому будет работать ТОР сеть, тоесть там необходимо указывать два порт по которым будет работать тор — один порт для передачи данных, а второй для обмена информацией о ноде9050 — для передачи 9001 — для обмена инфой .  
Далее Nickname Это обязательный параметр — тор-нода должна как то называться, тут необходимо поменять TORNAME на свое — придумайте что нибудь. Любое имя.  
Последующие 2 параметра отвечают за скорость RelayBandwidthRate 80 KB — 80 КилоБайт в секунду  
это значит 80*8=… кбит\с и это неплохая скорость  
Если мы хотим увеличить — то можем увеличить скорость пропускания — зависит от задачи — если не будем использовать потоковое вещание или что то в этом роде (где надо онлайн передавать и получать инфу) то тогда лучше оставить так как есть .  
Далее, тор-ноду будут использовать все кто хочет, поэтому тут оч важно не переборщить — забьют канал и сожрут весь трафик который нам дан на ДО. Там есть лимиты .  
При покупке сервера там в конфигурации указывается, по умолчанию вроде минимум 1 тб стоит.  
Второй параметр это так называемый Burst. Это технология когда например приложение использующее сеть пытается запросить у маршрутизатора больший канал связи чем он ему дает посылает такой burst query “дай мне больше канала” , а маршрутизатор дает ему 100КБ. В данном случае маршрутизатор — торно затем со временем зарубает все равно до 80. Это сделано для того что бы так сказать пропихивать пакеты быстрее, например качаем 100гигов с интернета, качать неделю, вот в определенный период времени скорость взяла и понизилась  
Далее куча параметров ExitPolicy accept  
Эти параметры разрешают прохождение трафика по конкретным портам . Тут перечислены популярные порты , можем удалить не нужное, а можем и оставить или добавить спец. порты.  
Тут дело в том что для анонимности иногда хорошо иметь большой трафик. Как бы потеряться в 5 миллионном городе проще чем в деревне в 100человек.  
Поэтому решать вам, если наша цель минимизировать трафик и тогда стабильность будет выше канала — то разрешить только 1 порт который нужен, а если хотим такую большую мусорку трафика смотреть то тогда ничего не менять в конфиге .  
В самом низу  
reject  
это значит что все что не разрешено — запрещено, то есть открыли порты (перечислили accept…) и остальное блокируем.  
Далее сохраняем и перезапускаем тор .  
/etc/init.d/tor restart  
и посмотреть вывод ps -aux | grep tor  
эта команда покажет работающие процессы и отфильтрует их по слову tor  
если красных ошибок нет, значит после перезагрузки тора он запустился успешно  
Atlas  
когда зайдем на страничку в правом верхнем углу будет окно поиска — вбиваем там айпишник сервера на котором подняли тор ноду.  
Сразу атлас ничего о ней не знает. Обычно тор сервера спрашивают всех участников тора примерно каждые 2 часа и через 2 часа тор-нода должна включиться в работу.  
Можете проверять в атласе и когда она там появится — тор нода заработает.
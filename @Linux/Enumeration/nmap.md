сканировать диапазон последнего октета  
`sudo nmap -sP 192.168.1.0/24`
  
_скрипт для скана принимающий один аргумент — адрес сканируемого хоста:_
```bash
#!/bin/bash  
ports=$(nmap -p- --min-rate=500 $1 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)  
nmap -p$ports -A $1  
```

`nmap -T4 -A -v TARGET`

### common usage
#nmap: get active hosts (good for LAN)  
`nmap -sP --min-rate 1000 -T4 ipRange | grep -Eo '([0-9]*\.){3}[0-9]*'`

#nmap: get active hosts over internet on a big range  
`nmap -sS -F -n --min-rate 500 -T4 ipRange -oA nmap-100-ping-scan | grep -Eo '([0-9]*\.){3}[0-9]*' | sort -u`
  
#nmap: slow scan for UDP and TCP on all ports  
`nmap -p- --min-rate 500 --max-retries 1 -T4 -sUS -oA fileName targetIp`
  
#nmap: advanced scan fordetecting most of the services/os and versions  
`nmap --min-rate 500 -sS -sV -O -sC -iL active-hosts.txt -oA nmap-1000-ports`
  
#nmap: grep all hosts that has the port 445 open  
`cat file.gnmap | grep "445/open/tcp" | cut -f2 -d " "``
  
#nmap: path to scripts  
`/usr/share/nmap/scripts`
  
#nmap: Stealth-SYN-Scan (does not contact Service), -O = operating system.  
`nmap -e yourInterface -sS -O targetIp`
  
#nmap: find MySql server, UDP scan  
`nmap -iL targetIp-list.txt -sU -p 1434 --script=ms-sql-info`
  
#nmap: exploit checker  
`nmap -v -p 445 --script smb-vuln-ms08-067 targetIp`
`nmap -v -p 3389 --script rdp-vuln-ms12-020 targetIp`
  
#nmap: MSSQL scripts  
`nmap -n -sU --script=ms-sql-info -p 1434 targetIp`
`nmap -p 1434 --script ms-sql-brute --script-args userdb=user.txt,passdb=pws.txt targetIp`
`nmap -sS --script ms-sql-xp-cmdshell --script-args mssql.username=sa,mssql.password=sa,ms-sql-xp-cmdshell.cmd="whoami",mssql.instance-port=1434 targetIp`
  
#nmap: script category  
`nmap --script "http-*" targetIp`
`nmap --script "not intrusive" -p 80,443,445,8080`

#script snmp-brute
`nmap -sU -n -p 161 --script snmp-brute IP --script-args snmp-brute.communitiesdb=wordlist`

#nmap: write grepable, XML and nmap format  
`nmap -oA fileName targetIp`
  
#nmap: resume stopped scan (need normal (-oN) or grepable (-oG) format)  
`nmap --resume fileName`

#SSL Security check
`nmap --script=ssl-enum-ciphers -p 433 tesla.com`

#### Сводка опций
```bash
https://nmap.org/man/ru/man-briefoptions.html  
Эта сводка опций выводится на экран, когда Nmap запускается без каких-либо опций; последняя версия всегда доступна здесь https://nmap.org/data/nmap.usage.txt. Эта сводка помогает людям запомнить наиболее употребляемые опции, но она не может быть заменой документации, предоставленной в данном руководстве. Некоторые опции не включены в этот список.  
  
Nmap 4.76 ( https://nmap.org )  
Использование: nmap [Тип(ы) Сканирования] [Опции] {цель сканирования}  
ОПРЕДЕЛЕНИЕ ЦЕЛИ СКАНИРОВАНИЯ:  
  Можно использовать сетевые имена, IP адреса, сети и т.д.  
  Пример: scanme.nmap.org, microsoft.com/24, 192.168.0.1; 10.0.0-255.1-254  
  -iL <имя_входного_файла>: Использовать список хостов/сетей из файла  
  -iR <количество_хостов>: Выбрать произвольные цели  
  --exclude <хост1[,хост2][,хост3],...>: Исключить хосты/сети  
  --excludefile <имя_файла>: Исключить из сканирования список хостов/сетей, находящийся в файле  
ОБНАРУЖЕНИЕ ХОСТОВ:  
  -sL: Сканирование с целью составления списка - просто составить список целей для сканирования  
  -sP: Пинг сканирование - просто определить, работает ли хост  
  -PN: Расценивать все хосты как работающие - пропустить обнаружение хостов  
  -PS/PA/PU [список_портов]: TCP SYN/ACK или UDP пингование заданных хостов  
  -PE/PP/PM: Пингование с использованием ICMP-эхо запросов, запросов временной метки и сетевой маски   
  -PO [список_протоколов]: Пингование с использованием IP протокола  
  -PR ARP сканирование: самый быстрый способ обнаружения хостов
  -n/-R: Никогда не производить DNS разрешение/Всегда производить разрешение [по умолчанию: иногда]  
  --dns-servers <сервер1[,сервер2],...>: Задать собственные DNS сервера для разрешения доменных имён  
  --system-dns: Использовать системный DNS-преобразователь  
РАЗЛИЧНЫЕ ПРИЕМЫ СКАНИРОВАНИЯ:  
  -sS/sT/sA/sW/sM: TCP SYN/с использованием системного вызова Connect()/ACK/Window/Maimon сканирования  
  -sU: UDP сканирование  
  -sN/sF/sX: TCP Null, FIN и Xmas сканирования  
  --scanflags <флаги>: Задать собственные TCP флаги  
  -sI <зомби_хост[:порт]>: "Ленивое" (Idle) сканирование  
  -sO: Сканирование IP протокола   
  -b <FTP_хост>: FTP bounce сканирование  
  --traceroute: Трассировка пути к хосту  
  --reason: Выводить причину, почему Nmap установил порт в определенном состоянии  
ОПРЕДЕЛЕНИЕ ПОРТОВ И ПОРЯДКА СКАНИРОВАНИЯ:   
  -p <диапазон_портов>: Сканирование только определенных портов  
    Пример: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080  
  -F: Быстрое сканирование - Сканирование ограниченного количества портов  
  -r: Сканировать порты последовательно - не использовать случайный порядок портов  
  --top-ports <количество_портов>: Сканировать <количество_портов> наиболее распространенных портов  
  --port-ratio <рейтинг>: Сканировать порты с рейтингом большим, чем <рейтинг>  
ОПРЕДЕЛЕНИЕ СЛУЖБ И ИХ ВЕРСИЙ:  
  -sV: Исследовать открытые порты для определения информации о службе/версии  
  --version-intensity <уровень>: Устанавливать от 0 (легкое) до 9 (пробовать все запросы)  
  --version-light: Ограничиться наиболее легкими запросами (интенсивность 2)  
  --version-all: Использовать каждый единичный запрос (интенсивность 9)  
  --version-trace: Выводить подробную информацию о процессе сканирования (для отладки)  
СКАНИРОВАНИЕ С ИПОЛЬЗОВАНИЕМ СКРИПТОВ:  
  -sC: эквивалентно опции --script=default  
  --script=<Lua скрипты>: <Lua скрипты> - это разделенный запятыми список директорий, файлов скриптов или   
  категорий скриптов  
  --script-args=<имя1=значение1,[имя2=значение2,...]>: Передача аргументов скриптам  
  --script-trace: Выводить все полученные и отправленные данные  
  --script-updatedb: Обновить базу данных скриптов  
ОПРЕДЕЛЕНИЕ ОС:  
  -O: Активировать функцию определения ОС  
  --osscan-limit: Использовать функцию определения ОС только для "перспективных" хостов  
  --osscan-guess: Угадать результаты определения ОС  
ОПЦИИ УПРАВЛЕНИЯ ВРЕМЕНЕМ И ПРОИЗВОДИТЕЛЬНОСТЬЮ:  
  Опции, принимающие аргумент <время>, задаются в миллисекундах, пока вы не добавите 's' (секунды), 'm' (минуты),   
  или 'h' (часы) к значению (напр. 30m).  
  -T[0-5]: Установить шаблон настроек управления временем (больше - быстрее)  
  --min-hostgroup/max-hostgroup <кол_хостов>: Установить размер групп для параллельного сканирования  
  --min-parallelism/max-parallelism <количество_запросов>: Регулирует распараллеливание запросов  
  --min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <время>: Регулирует время ожидания ответа на запрос  
  --max-retries <количество_попыток>: Задает максимальное количество повторных передач запроса  
  --host-timeout <время>: Прекращает сканирование медленных целей  
  --scan-delay/--max-scan-delay <время>: Регулирует задержку между запросами  
  --min-rate <число>: Посылать запросы с интенсивностью не меньше чем <число> в секунду  
  --max-rate <число>: Посылать запросы с интенсивностью не больше чем <число> в секунду  
ОБХОД БРАНДМАУЭРОВ/IDS:  
  -f; --mtu <значение>: Фрагментировать пакеты (опционально с заданным значениме MTU)  
  -D <фикт_хост1,фикт_хост2[,ME],...>: Маскировка сканирования с помощью фиктивных хостов  
  -S <IP_адрес>: Изменить исходный адрес  
  -e <интерфейс>: Использовать конкретный интерфейс  
  -g/--source-port <номер_порта>: Использовать заданный номер порта  
  --data-length <число>: Добавить произвольные данные к посылаемым пакетам  
  --ip-options <опции>: Посылать пакет с заданным ip опциями  
  --ttl <значение>: Установить IP поле time-to-live (время жизни)  
  --spoof-mac <MAC_адрес/префикс/название производителя>: Задать собственный MAC адрес  
  --badsum: Посылать пакеты с фиктивными TCP/UDP контрольными суммами  
ВЫВОД РЕЗУЛЬТАТОВ:  
  -oN/-oX/-oS/-oG <файл>: Выводить результаты нормального, XML, s|<rIpt kIddi3,  
     и Grepable формата вывода, соответственно, в заданный файл  
  -oA <базовове_имя_файла>: Использовать сразу три основных формата вывода   
  -v: Увеличить уровень вербальности (задать дважды или более для увеличения эффекта)  
  -d[уровень]: Увеличить или установить уровень отладки (до 9)  
  --open: Показывать только открытые (или возможно открытые) порты  
  --packet-trace: Отслеживание принятых и переданных пакетов  
  --iflist: Вывести список интерфейсов и роутеров (для отладки)  
  --log-errors: Записывать ошибки/предупреждения в выходной файл нормального режима  
  --append-output: Добавлять выходные данные в конец, а не перезаписывать выходные файлы  
  --resume <имя_файла>: Продолжить прерванное сканирование  
  --stylesheet <путь/URL>: Устанавливает XSL таблицу стилей для преобразования XML вывода в HTML  
  --webxml: Загружает таблицу стилей с Nmap.Org  
  --no-stylesheet: Убрать объявление XSL таблицы стилей из XML  
РАЗЛИЧНЫЕ ОПЦИИ:  
  -6: Включить IPv6 сканирование  
  -A: Активировать функции определения ОС и версии, сканирование с использованием скриптов и трассировку  
  --datadir <имя_директории>: Определяет место расположения файлов Nmap  
  --send-eth/--send-ip: Использовать сырой уровень Ethernet/IP  
  --privileged: Подразумевать, что у пользователя есть все привилегии  
  --unprivileged: Подразумевать, что у пользователя нет привилегий для использования сырых сокетов  
  -V: Вывести номер версии  
  -h: Вывести эту страницу помощи  
ПРИМЕРЫ:  
  nmap -v -A scanme.nmap.org  
  nmap -v -sP 192.168.0.0/16 10.0.0.0/8  
  nmap -v -iR 10000 -PN -p 80  
ДЛЯ СПРАВКИ ПО ДРУГИМ ОПЦИЯМ, ОПИСАНИЙ И ПРИМЕРОВ СМОТРИТЕ MAN СТРАНИЦУ
```

`--script default,safe`
`--script "http-*"` # may contain bruteforcing
`--script "broadcast and not targets*"` # no need ip
`--script "vuln,exploit"`

`locate *ip-geolocation*.nse`
https://dev.maxmind.com/geoip/geolite2-free-geolocation-data?lang=en

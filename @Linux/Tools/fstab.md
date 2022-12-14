### Автомонтирование дисков в Archlinux (и не только в нем). fstab

Смотрим, какие диски "доступны" системе:  
  
**$ sudo blkid**  
(отсюда берем UUID диска)  
  
И далее:  
  
**$ sudo gedit /etc/fstab**  
  
Внизу добавляем строку примерно такого вида:  
  
**UUID=D45A39A15A3980F2 /home/myname/yandexDRIVE ntfs rw,notail,relatime 0 0**  
Выделенное красным заменяем на своё.  
  
ВАЖНО! Поддиректория /home/myname/yandexDRIVE должна быть _создана заранее_.

В результате обычного монтирования командой mount параметры будут сохранены до первой перезагрузки ОС. Подробнее о использовании команды mount можно прочитать статью ["Команда mount в Linux или все о монтировании разделов, дисков, образов ISO и SMB ресурсов"](http://itshaman.ru/articles/3/mount "Команда mount в Linux или все о монтировании разделов, дисков, образов ISO и SMB ресурсов"). После перезагрузки ОС все эти действия необходимо производить заново. Чтобы монтирование происходило в автоматическом режиме, при каждой загрузке операционной системы, нужно отредактировать конфигурационный файл _fstab_.

В этой статье подробно рассмотрен вопрос **автоматического монтирования** разделов жесткого диска и других накопителей при старте операционной системы **Линукс**.

## Что такое /etc/fstab и зачем он нужен?

fstab - это текстовый файл, содержащий список устройств хранения информации и параметры монтирования. Различные накопители, которые необходимо автоматически присоединить во время загрузки операционной системы, по порядку перечисляются в файле fstab. Также в этом файле содержатся информация об устройствах, которые не присоединяются автоматически, но при выполнении монтирования устройства стандартной командой mount происходит присоединение устройства с заданными параметрами Это необходимо, к примеру, для CD/DVD-приводов, которые не примонтированы постоянно, а монтируются при наличии диска в приводе.

## Содержимое /etc/fstab

### Строки конфигурационного файла fstab

fstab состоит из строк. Каждая строка это устройство. Символ решетки (#) в начале строки, как и во всех Unix системах, обозначает комментарий и поэтому значимой строкой не считается.

Здесь будут рассмотрены только строки файла fstab. Более детально каждую строчку рассмотрим ниже.

Для просмотра файла fstab:

sudo nano /etc/fstab

Пример, как может выглядеть конфигурационный файл fstab:

# /etc/fstab: static file system information.  
#  
# <file system> <mount point> <type> <options> <dump> <pass>

proc /proc proc defaults 0 0

# /dev/sda1  
UUID=b60b8731-9ff7-2238f302e592 / reiserfs notail,relatime 0 1

# /dev/sda3  
UUID=69af6982-e3c7-99d02fb3a973 /home ext3 relatime 0 2

# /dev/sda2  
UUID=b3a38495-55d7-33b9ea8d62ec none swap sw 0 0

/dev/scd1 /media/cdrom0 udf,iso9660 user,noauto,exec,utf8 0 0  
/dev/scd0 /media/cdrom1 udf,iso9660 user,noauto,exec,utf8 0 0

/dev/fd0 /media/floppy0 auto rw,user,noauto,exec,utf8 0 0

**Белый цвет.**

Белым цветом помечен стандартный заголовок файла fstab.

**Желтый цвет**.

Желтая строка монтирует виртуальную файловую систему _procfs_ к директории _/proc_. Это стандартная процедура ОС, поэтому лучше ее не трогать.

**Синий цвет**.

Синяя строка присоединяет корневой раздел с параметрами _notail,relatime_ (значение параметров будет рассмотрено ниже). Это тоже лучше не трогать.

**Зеленый цвет**.

Зеленая строка монтирует раздел _/home_ с параметром _relatime_.

**Красный цвет**.

Красная монтирует SWAP раздел.

**Серый цвет**.

Серые строки задают параметры _user,noauto,exec,utf8_ для ручного (параметр noauto) монтирования CD/DVD-приводов.

**Черный цвет**.

Черные строки задают параметры ручного монтирования floppy-диска.

### Столбцы конфигурационного файла fstab

Теперь рассмотрим более подробно из чего состоит каждая строка. Все строки обладают одинаковым числом блоков. Каждый блок в строке отделен минимум одним пробелом (корректнее отделять блоки клавишей ).

UUID=b60b8731-9ff7-2238f302e592 / reiserfs notail,relatime 0 1

**Желтое поле**.

В желтом поле находятся названия или универсальные идентификаторы устройств.

Обозначение раздела жесткого диска в Linux может представляться двумя способами: названием устройства (/dev/sda1, /dev/sdb1 и т.д.) или универсальным идентификатором (UUID). В линуксе эти оба обозначения взаимозаменяемы.

В нашем примере, устройство /dev/sda1 и устройство UUID=b60b8731-9ff7-463f-a32f-2238f302e592 одно и то же. UUID назначается операционной системой автоматически при установке. Предпочтительнее в файле fstab использовать обозначение устройств по UUID, так как при обновлениях операционной системы могут измениться названия устройств (к примеру /dev/sda1 может изменить название на /dev/sdb1).

Просмотреть присвоенные устройству UUID можно командой:

# blkid

**Синее поле**.

В синем столбике отображены точки монтирования. Точка монтирования — это директория, где нужно искать данное устройство. В нашем примере, чтобы просмотреть содержимое раздела жесткого диска /dev/sda3 нужно открыть директорию /home.

**Зеленое поле**.

В зеленом столбике описаны типы файловых систем.

#### Жесткий диск:

-   ext2, ext3, ext4;
-   raserfs;
-   xfs;
-   ntfs (возможно ntfs-3g);
-   fat32;
-   vfat (это fat16).

#### USB-накопитель:

-   auto (автоматическое распознавание файловой системы);
-   ntfs (возможно ntfs-3g);
-   fat32;
-   vfat (это fat16).

#### CD/DVD-привод:

-   auto (автоматическое распознавание файловой системы);
-   iso9660,udf.

#### Floppy-привод:

-   auto (автоматическое распознавание файловой системы);
-   vfat (это fat16);
-   fat32;
-   ext2, ext3, ext4.

**Красное поле**.

В красном столбике находятся параметры монтирования. Если параметров несколько, то они перечисляются через запятую без пробелов.

Параметр

Действие

Значение по умолчанию

exec

Разрешить запуск исполняемых файлов.

включена

noexec

Запретить запуск исполняемых файлов

–

auto

Раздел будет автоматически монтироваться при загрузке операционной системы.

включена

noauto

Раздел не будет автоматически монтироваться при загрузке операционной системы.

–

rw

Выставить права доступа на чтение и запись.

включена

ro

Выставить права доступа только на чтение.

–

nouser

Запретить простым пользователям монтировать/демонтировать устройство.

включена

user

Разрешить простым пользователям монтировать/демонтировать устройство.

–

sw или swap

Специальный параметр SWAP области

–

async

Включение опции асинхронного ввода/вывода. Любая операция (копирование файла, удаление и т.д.) будет происходить немного позже, чем дана команда. Помогает в распределении нагрузки ОС, последняя сама выбирает подходящее время.

включена

sync

Включение опции синхронного ввода/вывода. Любая операция происходит синхронно с командой.

–

suid

Разрешить работу SUID и SGID битов. Бит SUID, у исполняемого файла, повышает запустившему пользователю права до владельца этого файла. К примеру, если root создал исполняемый файл с битом SUID, то пользователь, запустивший этот файл, получает на время исполнения файла права суперпользователя. Бит SGID, у исполняемого файла, повышает запустившему пользователю права до группы владельца этого файла.

–

nosuid

Заблокировать работу SUID и SGID битов для устройства.

включена

iocharset=koi8-r codepage=866

Добавляет поддержку кодировки koi8-r в названиях файлов и директорий. Применять при необходимости.

–

errors=remount-ro

При ошибке перемонтировать с параметром только для чтения (ro).

–

notail

Запрещает хранить маленькие файлы в хвостах больших. Увеличивает быстродействие.

–

atime

Производить запись времени последнего доступа к файлу.

включена

noatime

Отключение записи времени последнего доступа к файлу. Увеличивает быстродействие файловой системы. Эта опция не рекомендуется стандартом POSIX, так как некоторые приложения требуют этой функции (к примеру, почтовые клиенты и программы нотификации о новой почте перестанут правильно работать).

–

relatime

Включение обновления времени последнего обращения к файлу только в том случае, если предыдущее время доступа было раньше, чем текущее время изменения файла. Это более лояльный подход, чем noatime.

–

defaults

Использование всех параметров по-умолчанию: exec, auto, rw, nouser, async, nosuid, atime

–

**Серое поле**.

Серое поле указывает на включение/исключение устройства хранения информации в список резервного копирования программы DUMP, если последняя используется.

**0** — не выполнять резервное копирование;

**1** — выполнять резервное копирование.

**Черное поле**.

Черное поле устанавливает порядок проверки раздела на наличие ошибок. Если установить один и тот же порядок для двух разделов, они будут проверяться одновременно.

**0** — раздел не проверяется;

**1** — раздел проверяется первым;

**2** — раздел проверяется вторым и т.д.

## Примеры использования

### Как автоматически подключить раздел NTFS в Linux

1.  Просматриваем все доступные разделы:
    
    sudo fdisk -l
    
    Результат:
    
    **user@desktop:~$** sudo fdisk -l  
    Диск /dev/sda: 160.0 ГБ, 160041885696 байт  
    255 heads, 63 sectors/track, 19457 cylinders  
    Units = цилиндры of 16065 * 512 = 8225280 bytes  
    Disk identifier: 0x815aa99a
    
    Устр-во
    
    Загр
    
    Начало
    
    Конец
    
    Блоки
    
    Id
    
    Система
    
    /dev/sda1*
    
    1
    
    4788
    
    38459578+
    
    7
    
    HPFS/NTFS
    
    /dev/sda2
    
    6668
    
    19457
    
    102735675
    
    5
    
    Расширенный
    
    /dev/sda3
    
    4789
    
    5031
    
    1951897+
    
    82
    
    Linux
    
    своп / Solaris
    
    /dev/sda4
    
    5032
    
    6667
    
    13141170
    
    83
    
    Linux
    
    /dev/sda5
    
    6668
    
    19457
    
    102735640
    
    83
    
    Linux
    
    Пункты таблицы разделов расположены не в дисковом порядке
    
    Ищем раздел, который нужно подключить. В нашем примере это /dev/sda1
2.  Просматриваем присвоенные UUID устройствам:
    
    blkid
    
    Результат:
    
    **user@desktop:~$** blkid  
    /dev/sda1: **UUID="D45A39A15A3980F2"** TYPE="ntfs"  
    /dev/sda3: TYPE="swap" UUID="cff5bb9f-22d5-44d2-a4e8-30658f83fb4e"  
    /dev/sda4: UUID="03d11ea5-2b80-4a5e-ba09-cd6909425070" LABEL="root" TYPE="reiserfs"  
    /dev/sda5: UUID="503b7434-1ced-495d-a565-a4f02634c748" TYPE="ext3" SEC_TYPE="ext2"
    
    Находим нужный UUID. В нашем примере это UUID="D45A39A15A3980F2"
3.  Открываем файл fstab для редактирования:
    
    sudo nano /etc/fstab
    
4.  Добавляем строчку к концу файла fstab. Эта строка формируется из:
    
    4.1 На первое место ставим UUID требуемого раздела жесткого диска:
    
    UUID=D45A39A15A3980F2
    
    4.2 На второе место выбираем и ставим точку монтирования, допустим будет /home/windows:
    
    UUID=D45A39A15A3980F2 /home/windows
    
    4.3 Указываем файловую систему NTFS:
    
    UUID=D45A39A15A3980F2 /home/windows ntfs
    
    4.4 Далее выбираем из таблицы параметры, с которыми хотим примонтировать раздел:
    
    UUID=D45A39A15A3980F2 /home/windows ntfs rw,notail,relatime
    
    4.5 Резервное копирование этого раздела программой dump делать нам не нужно, поэтому ставим далее 0:
    
    UUID=D45A39A15A3980F2 /home/windows ntfs rw,notail,relatime 0
    
    4.6 Проверка раздела на ошибки делать тоже не будем, поэтому тоже 0:
    
    UUID=D45A39A15A3980F2 /home/windows ntfs rw,notail,relatime 0 0
    
5.  Последнюю строку к концу файла fstab можно добавить руками или командой:
    
    echo “UUID=D45A39A15A3980F2 /home/Windows ntfs rw,notail,relatime 0 0” | sudo tee -a /etc/fstab
    

### Автоматическое подключение CD/DVD-привода

/dev/cdrom /media/cdrom iso9660,udf ro,noauto,user,exec 0 0

Устройство /dev/cdrom подключается к точке монтирования /media/cdrom. Файловая система iso9660,udf. Подключается с параметрами ro (только чтение), noauto (не подключатся автоматически при старте ОС), user (подключение может осуществить любой пользователь) и exec (разрешить запуск приложение с подключаемого носителя).
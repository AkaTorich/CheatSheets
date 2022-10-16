freebsd-update fetch сбор данных для обновления системы  
freebsd-update install установка обновлений  
portsnap fetch extract обновление портов  
portsnap fetch update   
pkg install portupgrade установка программы для установки портов  
portupgrade -af  --batch апргрейд портов  
pkg install mc установка midnight commander  
pkg install screen установка программы экранов  
screen -R scr1 создат экран  
Ctrl+a + d свернуть экран  
  
установка графической оболочки XFCE  
pkg install nano   
pkg install xorg  
pkg install slim  
pkg install xfce  
  
nano /etc/rc.conf открыть и добавить в конфиг  
moused_enable="YES"  
dbus_enable="YES"  
hald_enable="YES"  
slim_enable="YES"  
sound_load="YES"  
snd_hda_load="YES"  
  
nano /home/имя пользователя/.xintrc открыть и добавить в конфиг  
exec xfce4-session  
или  
exec startxfce4  
  
init 6 перезапуск
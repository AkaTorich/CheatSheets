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
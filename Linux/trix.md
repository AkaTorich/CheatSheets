cat error.log | grep '___IP___' | cut -d "\"" -f 2 |uniq -c  
^ выведет все запросы к серверу с этим айпи  
  
cat access.log | grep '___IP___' | grep '/admin' | sort -u  
^ выведет все обращения к файлу admin  
  
comm 1.txt 2.txt  
^ Сравнивает и ищет совпадения строк в двух файлах построчно выводя результат
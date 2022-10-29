# Download via the command line on Windows 7

If you want to test your connection or have some other reason to use the command line to download a file, this is how.

See [http://superuser.com/a/284147](http://superuser.com/a/284147) for more information.

Open `cmd.exe` and use this format:

```
bitsadmin /transfer debjob /download /priority normal http://cdimage.debian.org/debian-cd/current-live/i386/iso-hybrid/debian-live-8.7.1-i386-xfce-desktop.iso D:\Users\[Username]\Downloads\debian-live-8.7.1-i386-xfce-desktop.iso
```

You should get something like this:

[![debjob](https://camo.githubusercontent.com/782bb98c56d8948e56380ffc786fa680366b9daed9230113df5032c8760286fb/68747470733a2f2f692e696d6775722e636f6d2f7873664f51664e2e706e67)](https://camo.githubusercontent.com/782bb98c56d8948e56380ffc786fa680366b9daed9230113df5032c8760286fb/68747470733a2f2f692e696d6775722e636f6d2f7873664f51664e2e706e67)

You can view the current download rate and file size. When the download is complete see your Downloads folder for the file.
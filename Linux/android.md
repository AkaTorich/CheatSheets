```bash
sudo apt install anbox  
ls -1 /dev/{ashmem,binder}  
sudo modprobe ashmem_linux  
sudo modprobe binder_linux  
  
Android image  
Anbox indeed expect to find an Android image at /var/lib/anbox/android.img.  
Download the latest image available at https://build.anbox.io/android-images/ and move it there:  
  
$ sudo mv ~/Downloads/android_amd64.img /var/lib/anbox/android.img  
  
sudo service anbox-container-manager restart  
  
anbox launch --package=org.anbox.appmgr --component=org.anbox.appmgr.AppViewActivity  
sudo apt install android-tools-adb  
  
adb install F-Droid.apk  
  
sudo adb shell settings put global http_proxy 192.168.250.1:8080
```
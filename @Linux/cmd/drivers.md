```bash
apt update 
apt dist-upgrade -y 
lsmod |grep -i nouveau 
echo -e "blacklist nouveau options nouveau modeset=0 alias nouveau off" > /etc/modprobe.d/blacklist-nouveau.conf
update-initramfs -u && reboot
lsmod |grep -i nouveau 
apt-get install -y ocl-icd-libopencl1 nvidia-driver nvidia-cuda-toolkit
```
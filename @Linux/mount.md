`apt install cifs-utils` #kali
`yay -S cifs-utils` #arch
`mkdir /mnt/share`
`mount -t cifs //TARGET/SHARE /MNT/FOLDER`
`mount -t cifs -o 'rw,username=guest' //TARGET/SHARE /MNT/FOLDER`
`sudo pacman -S libguestfs`
`guestmount -a '/path/to/vhd/file/in/share' -m /dev/sda1 --ro /root/bastion`
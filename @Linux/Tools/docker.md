#migrate to root user  
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
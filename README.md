**In this tutorial, I will show you how to instal Arch linux on a cloud server. Instand of using a container like docker, it is installed on you physically Could Server. Ensure you can use VNC to connect you server. otherwise, you can not follow this guide.**
### 1. You should download the archlinux iso file, using torrent to download or other methods you want.
### 2.Add these contents to /boot/grub/grub.cfg, and change the UUID.
```
set timeout=600
menuentry "Arch Linux Live (UUID Method)" {
    insmod part_msdos
    insmod iso9660
    insmod search_fs_uuid
    search --no-floppy --fs-uuid --set=root UUID
    linux /arch/boot/x86_64/vmlinuz-linux \
        archisobasedir=arch \
        archisolabel=ARCH_202601
    initrd /arch/boot/x86_64/initramfs-linux.img
}
```
### 3.rezise the mainpartiton on CLI. this is because we will reboot the server through the partition. otherwise we can not delete old partitions like root nad boot and can not create new partitions. 
```
parted /dev/vda
resizepart 2 48GB
print
quit
```
### 4.Cerate a 2GB partiton and use DD tool to copy the archlinux iso file(archlinux.iso) to the new partitoin like /dev/sda4 you created 2GB partition before.
### 5.Reboot your server, and connect the server with VNC.
### 6. Now you will see Archlinux starting. If you use BOIS, you should create a 1M partition.
```
parted /dev/vda
set 1 bios_grub on
quit
```
### 7. This is my prefered mirrorlist.
```
curl https://u.lihanzhang.cn/y7I11CecOW/mirrorlist -o /etc/pacman.d/mirrorlist
```
### 8.If you use BIOS, you should use these commands. I wrote these becase I prefer to use x86_64 computer, when I install achlinux with BIOS, I need to review these.
```
grub-install --target=i386-pc /dev/vda
grub-mkconfig -o /boot/grub/grub.cfg
```


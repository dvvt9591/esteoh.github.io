reference: 

http://stackoverflow.com/questions/27112436/how-does-biosdevname-really-work

http://askubuntu.com/questions/628217/use-of-predictable-network-interface-names-with-alternate-kernels

```
root@ubuntu75: # sudo apt-get purge biosdevname

root@ubuntu75: # sudo update-initramfs -u
update-initramfs: Generating /boot/initrd.img-3.19.0-33-generic
```

edit /etc/network/interfaces

change entry for p4p1 to eth0

optional:

change /etc/default/grub entry to GRUB_CMDLINE_LINUX_DEFAULT=biosdevname=0 and update GRUB to get the expected result by,

```
sudo update-grub
```

remove rule files in /etc/udev/rules.d/

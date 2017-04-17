```
esteoh@C640linux:~$ ./anbox-installer 
Android in a Box - Installer


IMPORTANT: THIS IS ALPHA LEVEL SOFTWARE. EXPECT INSTABILITY AND
           BUGS !!!!!

IMPORTANT: ALSO PLEASE BE AWARE THAT WE DON'T PROVIDE FULL
           CONFINEMENT FOR THE SNAP YET !!!!


PLEASE NOTE: This script will require root access on your system
to install all necessary things. It will prompt you to enter your
password when required.



What do you want to do?

 1. Install Anbox
 2. Uninstall Anbox

Please enter your choice [1-2]: 
1


This is the installer for the anbox runtime environment. It will
install certain things on your system to ensure all requirements
are available for anbox to work correctly.

In summary we will install the following things:

 * Add the anbox-support ppa ppa:morphis/anbox-support to the
   host system
 * Install the anbox-modules-dkms deb package from the ppa
   which will add kernel modules for ashmem and binder which are
   required for the Android container to work.
 * Configure binder and ashmem kernel modules to be loaded
   automatically on boot.
 * Add an upstart job for the current user esteoh which will
   start the anbox runtime on login.
 * Add a X11 session configuration file to allow the system
   application launcher (Unity7, Gnome Shell, ..) to find
   available Android applications.

Please type 'I AGREE' followed by pressing ENTER to continue
or type anything else to abort:
I AGREE


Starting installation process ...

+ '[' '!' -e /etc/udev/rules.d/99-anbox.rules ']'
+ sudo apt install -y software-properties-common linux-headers-generic
[sudo] password for esteoh: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
linux-headers-generic is already the newest version (4.4.0.72.78).
software-properties-common is already the newest version (0.96.20.5).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
+ sudo add-apt-repository -y ppa:morphis/anbox-support
gpg: keyring `/tmp/tmpu8n3anka/secring.gpg' created
gpg: keyring `/tmp/tmpu8n3anka/pubring.gpg' created
gpg: requesting key 875B67B7 from hkp server keyserver.ubuntu.com
gpg: /tmp/tmpu8n3anka/trustdb.gpg: trustdb created
gpg: key 875B67B7: public key "Launchpad PPA for morphis" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)
OK
+ sudo apt update
Hit:1 http://tw.archive.ubuntu.com/ubuntu xenial InRelease
Hit:2 http://tw.archive.ubuntu.com/ubuntu xenial-updates InRelease                                                                         
Hit:3 http://tw.archive.ubuntu.com/ubuntu xenial-backports InRelease                                                                       
Ign:4 http://dl.google.com/linux/chrome/deb stable InRelease                                                                               
Hit:5 http://dl.google.com/linux/chrome/deb stable Release                                                                                 
Ign:6 http://linux.dropbox.com/ubuntu wily InRelease                                                                                       
Hit:7 http://linux.dropbox.com/ubuntu wily Release                                                                                         
Hit:8 http://repo.sinew.in stable InRelease                                                                                                
Hit:10 http://ppa.launchpad.net/danielrichter2007/grub-customizer/ubuntu xenial InRelease                                                  
Hit:11 https://packages.microsoft.com/repos/vscode stable InRelease                                                                        
Ign:13 http://repo.vivaldi.com/stable/deb stable InRelease                                                                                 
Hit:14 http://ppa.launchpad.net/morphis/anbox-support/ubuntu xenial InRelease                                                       
Hit:15 http://archive.canonical.com/ubuntu xenial InRelease                                                   
Hit:16 http://repo.vivaldi.com/stable/deb stable Release                                                      
Hit:17 http://ppa.launchpad.net/nilarimogard/webupd8/ubuntu xenial InRelease                                  
Hit:19 http://ppa.launchpad.net/quiterss/quiterss/ubuntu xenial InRelease               
Hit:20 https://s3-us-west-2.amazonaws.com/brave-apt xenial InRelease                    
Hit:21 http://ppa.launchpad.net/rebuntu16/other-stuff/ubuntu xenial InRelease           
Hit:22 https://deb.opera.com/opera-stable stable InRelease                              
Get:23 http://security.ubuntu.com/ubuntu xenial-security InRelease [102 kB]
Fetched 102 kB in 6s (16.1 kB/s)                                                                                                           
Reading package lists... Done
Building dependency tree       
Reading state information... Done
All packages are up to date.
+ sudo apt install -y anbox-modules-dkms
Reading package lists... Done
Building dependency tree       
Reading state information... Done
anbox-modules-dkms is already the newest version (4~xenial1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
+ '[' '!' -e /etc/modules-load.d/anbox.conf ']'
+ sudo modprobe binder_linux
+ sudo modprobe ashmem_linux
+ snap info anbox
+ grep -q installed:
+ sudo snap install --edge --devmode anbox
anbox (edge) 1-dev from 'morphis' installed
+ '[' '!' -e /etc/X11/Xsession.d/68anbox ']'
+ echo 'Installing application launcher detection for X11 ..'
Installing application launcher detection for X11 ..
+ sudo tee /etc/X11/Xsession.d/68anbox
+ mkdir -p /home/esteoh/.config/upstart
+ echo 'Installing upstart session job ..'
Installing upstart session job ..
+ cat
+ initctl start anbox
anbox start/running, process 6593
+ mkdir -p /home/esteoh/.config/systemd/user
+ echo 'Installing systemd user session service ..'
Installing systemd user session service ..
+ cat
+ systemctl --user daemon-reload
+ systemctl --user enable --now anbox
Created symlink from /home/esteoh/.config/systemd/user/default.target.wants/anbox.service to /home/esteoh/.config/systemd/user/anbox.service.
+ set +x

Done!

To ensure all changes made to your system you should now reboot
your system. If you don't do this no Android applications will
show up in the system application launcher.

```
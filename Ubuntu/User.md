# Initial Settings : Use root account 2019/04/27

The root Account in Ubuntu is disabled by default because his password is not set. To use root priviledges, basically it's better to use the sudo command with administrative accounts. But if you'd like to use root Account itself by some reason, it's possible to use like follows.

## [1] 	The user account added during installation is set an administrative account with Sudo, so it's easy to get root account's shell like follows.
```
sudo -s
```
[sudo] password for ubuntu:   # input own password
root@dlp:~#                   # just switched

## [2] 	Or it's possible to switch to root account with standard su command to set root account's password.
```
sudo passwd root
```
[sudo] password for ubuntu:   # input own password
Enter new UNIX password:      # set root password
Retype new UNIX password:     # confirm
passwd: password updated successfully
```
su -
```
Password:                     # input root password
root@dlp:~#                   # just switched

* 	
The examples on this site shows as a root account. If you use Sudo, add [sudo] on the head of commands.
It's better to restrict users who can su to root if you enable root account like follows. For using by Sudo, it's possible to limit to prohibit shells in sudoers config, refer to details about Sudo Settings.
## [3] 	For su command restriction, set like follows.
root@dlp:~# vi /etc/pam.d/su
line 15: uncomment and add a group which is allow to run su command

auth       required   pam_wheel.so  group=adm

root@dlp:~# usermod -G adm ubuntu 

## Find available images
```
$ multipass find
```
Image                   Aliases           Version          Description
core                    core16            20190424         Ubuntu Core 16
core18                                    20190213         Ubuntu Core 18
16.04                   xenial            20190628         Ubuntu 16.04 LTS
18.04                   bionic,lts        20190627.1       Ubuntu 18.04 LTS
18.10                   cosmic            20190628         Ubuntu 18.10
19.04                   disco             20190628         Ubuntu 19.04
daily:19.10             devel,eoan        20190623         Ubuntu 19.10


## Launch a fresh instance of the current Ubuntu LTS
```
$ multipass launch ubuntu
```
Launching dancing-chipmunk...
Downloading Ubuntu 18.04 LTS..........
Launched: dancing chipmunk

## Check out the running instances
```
$ multipass list
```
Name                    State             IPv4             Release
dancing-chipmunk        RUNNING           10.125.174.247   Ubuntu 18.04 LTS
live-naiad              RUNNING           10.125.174.243   Ubuntu 18.04 LTS
snapcraft-asciinema     STOPPED           --               Ubuntu Snapcraft builder for Core 18

## Learn more about the VM instance you just launched
```
$ multipass info dancing-chipmunk
```
Name:           dancing-chipmunk
State:          RUNNING
IPv4:           10.125.174.247
Release:        Ubuntu 18.04.1 LTS
Image hash:     19e9853d8267 (Ubuntu 18.04 LTS)
Load:           0.97 0.30 0.10
Disk usage:     1.1G out of 4.7G
Memory usage:   85.1M out of 985.4M

## Connect to a running instance
```
$ multipass shell dancing-chipmunk
```
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-42-generic x86_64)

## Run commands inside an instance from outside
```
$ multipass exec dancing-chipmunk -- lsb_release -a
```
No LSB modules are available.
Distributor ID:  Ubuntu
Description:     Ubuntu 18.04.1 LTS
Release:         18.04
Codename:        bionic

## Stop an instance to save resources
```
$ multipass stop dancing-chipmunk
```
## Delete the instance
```
$ multipass delete dancing-chipmunk
```
It will now show up as deleted:

Name                    State             IPv4             Release
snapcraft-asciinema     STOPPED           --               Ubuntu Snapcraft builder for Core 18
dancing-chipmunk        DELETED           --               Not Available

## And when you want to completely get rid of it:
```
$ multipass purge
```
Integrate into the rest of your virtualization

You might have other virtualization already based on libvirt either through using the similar older uvtool already or through the common virt-manager.

You might for example want those guests to be on the same bridge to communicate to each other or you need access to the graphical output for some reason.

## Fortunately it is possible to integrate this by using the libvirt backend of multipass
```
$ sudo multipass set local.driver=libvirt
```
## After that when you start a guest you can also access it via tools like virt-manager or virsh
```
$ multipass launch ubuntu
```
## Launched: engaged-amberjack
```
$ virsh list
```
 Id    Name                           State
----------------------------------------------------
 15    engaged-amberjack              running

## Get help
```
multipass help
```
multipass help <command>
